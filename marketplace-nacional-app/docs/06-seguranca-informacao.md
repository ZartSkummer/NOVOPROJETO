# Segurança da informação — ameaças, controles e compliance

## 1. Classificação de dados (exemplos)

| Dado | Sensibilidade | Observações |
|------|---------------|-------------|
| Nome, e-mail, telefone | Média | LGPD; telefone pode ser vetor de spam. |
| Localização precisa (GPS) | Alta | Consentimento explícito e finalidade. |
| Fotos de anúncio | Baixa–média | Podem conter metadados EXIF (remover no upload). |
| Logs de acesso | Média | Sem PII; retenção definida. |
| Tokens de sessão | Alta | Armazenamento seguro no app (Keychain/Keystore). |

## 2. Modelo de ameaças (STRIDE — resumo)

| Ameaça | Exemplo no app | Controle |
|--------|----------------|----------|
| Spoofing | Conta fake para golpe | Verificação de e-mail/telefone, rate limit cadastro, device integrity básica |
| Tampering | Alteração de preço via API | Autorização server-side, validação de schema, idempotência |
| Repudiation | Negar publicação de anúncio | Logs auditáveis, IDs de correlação |
| Information disclosure | Enumeração de usuários | Respostas genéricas em login, paginação sem vazamento |
| DoS | Scraping agressivo | WAF, rate limit, CAPTCHA em pontos sensíveis |
| Elevation of privilege | Usuário acessa admin | RBAC, separação de deploy/roles, MFA para staff |

## 3. Autenticação e autorização

- **OAuth2/OIDC** com tokens de curta duração + refresh rotacionado.
- **Escopos** por recurso: `listings:write`, `listings:read`, `admin:*`.
- Política de senha alinhada a NIST/OWASP (comprimento > complexidade frágil).
- Opcional MMP: **MFA** para vendedores com alto volume.

## 4. API e backend

- TLS 1.2+ obrigatório; **HSTS** no domínio público.
- Validação estrita de entrada (tamanho, tipo, enums).
- **CORS** restritivo no admin web.
- **Idempotency-Key** em operações de escrita críticas (ex.: publicação paga, se houver; criação de anúncio com upload).
- Segredos em vault (AWS Secrets Manager, etc.); nunca em repositório.

## 5. Armazenamento de mídia

- URLs **pré-assinadas** com TTL curto para upload.
- Antivírus/clamav em bucket (worker) para arquivos suspeitos — conforme risco do nicho.
- Remoção de **EXIF** (GPS da câmera) ao processar imagens públicas.

## 6. App móvel

- Pinning de certificado: avaliar trade-off (manutenção vs ameaça).
- Ofuscação não substitui segurança server-side.
- Deep links validados; evitar abrir URLs arbitrárias sem allowlist.

## 7. LGPD (Brasil)

- Base legal para cada tratamento (execução de contrato, legítimo interesse com teste de balanceamento, consentimento quando necessário).
- **Política de privacidade** e **termos** acessíveis no app.
- Fluxos: visualizar dados, corrigir, excluir conta, portabilidade (MMP formalizado).
- **DPO**: definir responsável e canal de contato.
- Acordos com subprocessadores (cloud, e-mail, analytics).

## 8. Lojas (Apple / Google)

- Declarar coleta de localização com strings claras (`Info.plist`, Play Data Safety).
- Revisar guidelines para **UGC** (conteúdo gerado por usuário): moderação e denúncia.
- **Escopo atual (compra fora do app):** o app funciona como **classificado** — em geral **não** há IAP para o **bem anunciado**; ainda assim, evitar fluxos que **contornem** as regras das lojas (ex.: vender acesso digital ao item **dentro** do app sem o modelo de compra permitido). Se no futuro existir **assinatura/plano do anunciante** vendido pelo app, revisar o capítulo de **compras digitais** das guidelines e o jurídico.

## 9. Resposta a incidentes

- Runbook: revogação de tokens, rotação de chaves, comunicação ao usuário se risco relevante.
- Backup com **teste de restore** trimestral.

## 10. Checklist pré-go-live

- [ ] Pentest ou análise OWASP ASVS (nível proporcional ao risco).
- [ ] Dependências escaneadas (SCA) no CI.
- [ ] DAST básico em staging.
- [ ] Política de retenção de logs e backups documentada.
- [ ] Gestão de vulnerabilidades (SLA de patch).
