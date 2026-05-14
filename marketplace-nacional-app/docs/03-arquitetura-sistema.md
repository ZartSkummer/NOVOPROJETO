# Arquitetura do sistema — tecnologias, componentes e diagramas

## 1. Objetivos arquiteturais

- **Disponibilidade** para picos de leitura (listagens e busca).
- **Baixa latência** percebida no app (cache, CDN, imagens otimizadas).
- **Segurança** em profundidade (auth, autorização, rate limiting, auditoria).
- **Evolução** sem rewrite: módulos claros (catálogo, identidade, mídia, notificações).

## 2. Stack sugerida (referência — ajustar ao nicho e time)

| Camada | Opção A (alto ecossistema JS) | Opção B (performance UI) |
|--------|------------------------------|----------------------------|
| App móvel | **React Native** + TypeScript | **Flutter** + Dart |
| Backend API | **Node.js (NestJS)** ou **.NET 8** | **Go** (chi/echo) ou **.NET** |
| Banco transacional | **PostgreSQL 16+** + **PostGIS** (geo) | Idem |
| Busca / facets | **OpenSearch** ou **Meilisearch** (MVP) | Evoluir conforme volume |
| Cache | **Redis** | Idem |
| Filas / jobs | **SQS** ou **RabbitMQ** / **Redis Streams** | Conforme cloud |
| Object storage | **S3-compatível** (AWS / MinIO dev) | Idem |
| CDN | **CloudFront** / **Cloudflare** | Idem |
| IdP | **Cognito**, **Auth0**, **Keycloak** (self-host) | Decisão por custo/compliance |
| Observabilidade | **OpenTelemetry** + **Grafana** + **Loki** ou Datadog | — |
| CI/CD | **GitHub Actions** + deploy em **ECS/Kubernetes** ou **Cloud Run** | — |

## 3. Diagrama de contexto (C4 — nível 1)

```mermaid
flowchart TB
  subgraph Usuarios["Usuários"]
    C[Comprador]
    V[Vendedor / Anunciante]
    ADM[Operador / Suporte]
  end

  subgraph Mobile["Apps móveis"]
    IOS[iOS App Store]
    AND[Google Play]
  end

  subgraph Plataforma["Plataforma"]
    API[API Gateway + BFF]
    SVC[Serviços de domínio]
    SRCH[Mecanismo de busca]
    DB[(PostgreSQL + PostGIS)]
    R[Redis]
    Q[Filas]
    OBJ[Object Storage + CDN]
  end

  subgraph Externos["Serviços externos"]
    MAP[Mapas / geocoding]
    PUSH[Push APNs + FCM]
    MAIL[E-mail / SMS]
    PAY[Gateway pagamento - opcional]
    ANLY[Analytics / Crash]
  end

  C --> IOS
  C --> AND
  V --> IOS
  V --> AND
  IOS --> API
  AND --> API
  ADM --> API
  API --> SVC
  SVC --> DB
  SVC --> SRCH
  SVC --> R
  SVC --> Q
  SVC --> OBJ
  SVC --> MAP
  SVC --> PUSH
  SVC --> MAIL
  SVC --> PAY
  IOS --> ANLY
  AND --> ANLY
```

## 4. Diagrama de containers (C4 — nível 2, simplificado)

```mermaid
flowchart LR
  APP[App RN/Flutter]
  GW[API Gateway]
  AUTH[Serviço Identidade]
  CAT[Serviço Catálogo / Anúncios]
  MED[Serviço Mídia]
  NOT[Serviço Notificações]
  ADMWEB[Admin Web opcional]

  APP --> GW
  ADMWEB --> GW
  GW --> AUTH
  GW --> CAT
  CAT --> MED
  CAT --> NOT
```

## 5. Fluxo resumido: publicação de anúncio com mídia

```mermaid
sequenceDiagram
  participant U as Usuário
  participant A as App
  participant G as API
  participant O as Object Storage
  participant Q as Fila
  participant W as Worker

  U->>A: Preenche formulário + fotos
  A->>G: Solicita URLs pré-assinadas
  G-->>A: URLs pré-assinadas
  A->>O: Upload direto multipart
  A->>G: POST /listings com metadados + keys
  G->>Q: Job processar imagens / thumbnails
  Q->>W: Mensagem
  W->>O: Gera versões otimizadas
  W->>G: Atualiza status listing
```

## 6. Estratégia de API

- **REST** ou **GraphQL** (REST costuma ser mais simples para apps com cache HTTP).
- Versionamento: `/v1/...`.
- **OpenAPI** publicado internamente; contratos testados em CI.
- **BFF** (Backend for Frontend) opcional: útil se app e admin divergirem muito.

## 7. Multi-tenant e escopo nacional

- Particionamento lógico por **estado/município** e coordenadas para raio.
- **CDN** com política de cache apenas para assets públicos (imagens publicadas).
- Dados pessoais: minimização; logs sem PII.

## 8. Ambientes

- `dev` → `staging` (espelho de prod com dados mascarados) → `prod`.
- Feature flags para liberar gradualmente (ex.: novo filtro, novo nicho).

## 9. Telas no contexto da arquitetura

Cada tela consome principalmente:

- **Catálogo**: listagens, filtros, detalhe.
- **Identidade**: login, perfil, favoritos.
- **Mídia**: galeria, upload.
- **Notificações**: alertas de preço, novos itens na região (fase posterior com consentimento).

Detalhamento de telas: ver [04-especificacao-funcional-telas.md](./04-especificacao-funcional-telas.md).

## 10. Decisões a registrar (ADR)

Recomenda-se pasta `docs/adr/` com decisões curtas, por exemplo:

- ADR-001: PostGIS vs busca apenas por cidade.
- ADR-002: OpenSearch vs Meilisearch no MVP.
- ADR-003: React Native vs Flutter (critérios: time, performance, libs do nicho).
