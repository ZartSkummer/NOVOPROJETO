# Documentação do projeto — Serviço Perto

Este pacote reúne análise multidisciplinar para um **marketplace de serviços locais** (mobile-first): conexão entre **contratantes** e **prestadores** com **geolocalização**, **perfil rico** (fotos, categorias), **assinatura** para visibilidade do prestador e **confiança** via avaliações e depoimentos. O material cobre alternativas de UX (descoberta por proximidade vs catálogo), implicações de **transação e disputa** e requisitos técnicos de **arquitetura**, **dados**, **segurança**, **qualidade** e **precificação** com software house.

## Índice dos documentos

| # | Documento | Conteúdo principal |
|---|-----------|---------------------|
| 01 | [01-visao-executiva.md](./01-visao-executiva.md) | Proposta em uma frase, escopo implícito do cliente, opções de pagamento pós-serviço |
| 02 | [02-dificuldade-prazo-loc.md](./02-dificuldade-prazo-loc.md) | Grau de dificuldade (incl. uso de IA), prazos MVP/MMP, estimativa de linhas de código |
| 03 | [03-arquitetura.md](./03-arquitetura.md) | Diagramas, stack sugerida, integrações, componentes da plataforma |
| 04 | [04-inventario-telas-ux-ui.md](./04-inventario-telas-ux-ui.md) | Inventário de telas, fluxos, notas de UX/UI |
| 05 | [05-seguranca-informacao.md](./05-seguranca-informacao.md) | Ameaças, LGPD, autenticação, APIs, checklist |
| 06 | [06-dba-dados.md](./06-dba-dados.md) | Modelo de dados, índices, geo, performance e retenção |
| 07 | [07-qualidade-codigo-entrega.md](./07-qualidade-codigo-entrega.md) | Padrões, testes, CI/CD, definition of done |
| 08 | [08-precificacao-software-house.md](./08-precificacao-software-house.md) | Faixas BRL, composição de squad, o que encarece o projeto |
| 09 | [09-backlog-epico.md](./09-backlog-epico.md) | Lista épica do que precisa ser feito (discovery até go-to-market) |

## Premissas gerais (a validar com o cliente)

- O **core de descoberta** (feed por proximidade vs catálogo com busca) define custo e tempo; **ambos** duplicam complexidade de produto e engenharia se forem primeira classe no MVP.
- **“Redondo”** significa produto utilizável em produção com sustentação: observabilidade, moderação mínima, termos/LGPD operacionais e caminho claro para **disputas** se houver transação pela plataforma.
- **IA** acelera código repetitivo, testes e documentação; **não** substitui alinhamento jurídico-operacional (pagamento, KYC, lojas) nem qualidade de dados e liquidez do marketplace.

## Glossário rápido

- **MVP**: primeira versão com fluxo core (perfis, geo, listagem, contato/chat mínimo, avaliações básicas conforme escopo fechado).
- **MMP**: produto minimamente *marketetable* com qualidade de marca, métricas e operação suportável.

---

*Documento vivo — revisar após workshop de descoberta com o cliente.*
