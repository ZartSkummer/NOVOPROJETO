# Documento 6 — DBA / dados (visão)

## Entidades centrais (conceitual)

- `User`
- `ProviderProfile`
- `ServiceOffering`
- `Category`
- `Location` (PostGIS)
- `Subscription`
- `Conversation`
- `Message`
- `Job` / `Request`
- `Review`
- `Testimonial`
- `Report`
- `PaymentIntent` (se houver transação pela plataforma)

## Técnico

- Índices geo (GIST), índices para busca textual (pg_trgm ou OpenSearch).
- Estratégia de **soft delete** e auditoria em tabelas críticas.
- Backup, PITR, política de restore testada.
