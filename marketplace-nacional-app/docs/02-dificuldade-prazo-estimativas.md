# Dificuldade, prazo e estimativa de linhas de código

## 1. Grau de dificuldade (visão multidisciplinar)

### 1.1 Fullstack / engenharia de produto

- **Complexidade core**: CRUD de anúncios, mídia, autenticação, favoritos e filtros é **moderada**.
- **Complexidade que eleva o projeto**: busca textual + filtros compostos + **geo** (raio, estado, CEP), paginação estável, consistência eventual de índices, upload de muitas imagens, notificações push, **painel administrativo** e (opcional) chat ou leads rastreados — **sem** checkout in-app para a compra do item (decisão atual).
- **Classificação**: **Média–Alta** para produto nacional com SLA percebido de “app grande”.

### 1.2 UX/UI

- **Moderada**: padrões de marketplace são conhecidos (grade, filtros, detalhe, galeria).
- **Picos de esforço**: onboarding de anunciante, fluxo de filtros sem sobrecarregar, estados vazios e erro, acessibilidade (VoiceOver/TalkBack).

### 1.3 Arquitetura

- **Moderada–Alta** se objetivo for escala e evolução (microserviços só quando necessário; monólito modular costuma bastar no MVP).
- Decisões críticas: modelo de **dados de localização**, estratégia de **busca** (Postgres full-text vs OpenSearch/Elastic), **CDN** para imagens, **filas** para processamento assíncrono.

### 1.4 Segurança

- **Alta relevância**, dificuldade **média** no MVP com boas práticas (OAuth2, rate limit, WAF, secrets).
- Sobe para **alta** com **KYC** pesado, anti-fraude agressivo e armazenamento sensível além do usual — ou se no futuro houver **pagamento in-app** da compra.

### 1.5 DBA / dados

- **Média**: modelagem relacional + índices geográficos (PostGIS) ou estratégia híbrida.
- **Alta** se houver necessidade de **recomendação**, ranking complexo e big data de cliques.

### 1.6 Qualidade de código

- **Média**: testes automatizados e CI são factíveis; custo está em manter **contratos de API** e dados de teste realistas.

### 1.7 Empreendedor / produto

- **Alta incerteza de negócio**: liquidez do marketplace (oferta x demanda), CAC, moderação e confiança da marca importam mais que “linhas de código”.

---

## 2. Papel da IA no desenvolvimento

| Ajuda a IA | Limites reais |
|------------|----------------|
| Geração de telas, hooks, serviços, testes unitários | Homologação humana, design system consistente |
| Documentação, OpenAPI, migrações | Dados reais e edge cases de negócio |
| Refatoração e revisão estática | Segurança em runtime, config de nuvem |
| Scripts de E2E iniciais | Flake em CI, manutenção de seletores |

**Conclusão**: expectativa realista é **20–40% de ganho de velocidade** em times que já sabem arquitetar; **ganho menor** se o time for júnior e depender da IA para decisões de arquitetura.

---

## 3. Prazo estimado

### 3.1 MVP (primeira versão nas lojas, fluxo feliz sólido)

- **10 a 14 semanas** (2,5–3,5 meses) com squad pequeno focado:
  - App: listagem, busca básica, filtros localização + modelo, detalhe, cadastro/login, criar anúncio simples, favoritos.
  - Backend: APIs, auth, storage de imagens, moderação mínima (report).
  - Infra: staging + produção, CI, monitoramento básico.

### 3.2 Produto “redondo” (MMP + hardening)

Inclui, entre outros: performance de busca, **painel admin** útil, **LGPD** end-to-end, anti-fraude básico, analytics, crash reporting, melhorias de UX, testes E2E estáveis, runbooks, backups testados.

- **6 a 9 meses** (time 3–5 FTE) como referência, alinhado ao escopo **sem** gateway de compra no app.
- **Até ~12 meses** se houver **chat in-app** maduro, requisitos regulatórios extras ou long tail de integrações — **não** é necessário alongar o prazo só por “pagamento in-app”, pois está **fora** do escopo atual.

### 3.3 Marcos sugeridos

1. Descoberta + arquitetura + design (3–5 semanas)
2. MVP backend + app em paralelo (8–10 semanas)
3. Beta fechado + ajustes lojas (2–4 semanas)
4. Hardening e escala (contínuo, 2–4 meses)

---

## 4. Estimativa de linhas de código (LOC)

LOC é **métrica fraca** sozinha; serve como **ordem de grandeza** para orçamento mental e complexidade.

### 4.1 Faixas típicas (inclui testes e scripts de infra, exclui `node_modules`/vendor)

| Componente | LOC aproximadas |
|------------|-----------------|
| App React Native / Flutter (UI + estado + integrações) | 25k – 70k |
| Backend (API + domínio + workers) | 35k – 100k |
| Admin web (opcional mas comum) | 15k – 45k |
| Infra como código (Terraform/Pulumi) + CI | 3k – 12k |
| Testes (unit + integração + alguns E2E) | 15k – 50k |
| **Total** | **~80k – 250k** |

Fatores que **empurram para cima**:

- Chat in-app, negociação, lances, **ou** futuro pagamento split / checkout no app.
- Motor de recomendação próprio.
- Múltiplos perfis (PF/PJ) com fluxos distintos.

---

## 5. Comparativo Webmotors (referência conceitual)

O Webmotors consolidou **anos** de produto, integrações (financiamento, seguros, avaliação), conteúdo e confiança de marca. Um nicho novo deve planejar **liquidez** e **confiança**, não apenas paridade de features na V1.
