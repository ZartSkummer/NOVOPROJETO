# Documentação do projeto — Marketplace Nacional (app móvel)

Este pacote reúne análise multidisciplinar para um **aplicativo de vendas/listagens** com escopo nacional, **filtros por localização e por modelo** (ou equivalente do nicho), disponível na **App Store** e **Google Play**, inspirado conceitualmente no modelo **Webmotors**, porém para **outro segmento**.

## Decisão de produto (confirmada)

- **Pagamento da compra**: **fora do aplicativo**. O usuário **não** finaliza a transação do bem/serviço anunciado por checkout, PIX ou cartão dentro do app.
- **Papel do app**: descoberta, filtros, detalhe do anúncio e **contato com o anunciante** (telefone, WhatsApp, e-mail ou equivalente); o **fechamento comercial e o pagamento** ocorrem nos canais acordados entre as partes, fora da plataforma.

## Índice dos documentos

| # | Documento | Conteúdo principal |
|---|-----------|---------------------|
| 01 | [01-visao-executiva.md](./01-visao-executiva.md) | Resumo para decisão: dificuldade, prazo, ordem de grandeza de código, faixa de investimento |
| 02 | [02-dificuldade-prazo-estimativas.md](./02-dificuldade-prazo-estimativas.md) | Grau de dificuldade com IA, cronograma fases, linhas de código (ordem de grandeza) |
| 03 | [03-arquitetura-sistema.md](./03-arquitetura-sistema.md) | Diagramas (C4 simplificado), stack sugerida, integrações, observabilidade |
| 04 | [04-especificacao-funcional-telas.md](./04-especificacao-funcional-telas.md) | Épicos, fluxos, inventário de telas, critérios de aceite |
| 05 | [05-ux-ui-design-system.md](./05-ux-ui-design-system.md) | Princípios de UX, componentes, acessibilidade, padrões de listagem e filtros |
| 06 | [06-seguranca-informacao.md](./06-seguranca-informacao.md) | Ameaças, LGPD, autenticação, APIs, lojas, checklist |
| 07 | [07-modelo-dados-dba.md](./07-modelo-dados-dba.md) | Entidades, índices, busca geográfica, performance e retenção |
| 08 | [08-qualidade-codigo-testes.md](./08-qualidade-codigo-testes.md) | Padrões, testes, CI/CD, definition of done |
| 09 | [09-precificacao-comercial-software-house.md](./09-precificacao-comercial-software-house.md) | Como precificar, faixas BRL, o que entra no escopo MVP vs produto redondo |

## Premissas gerais (a validar com o cliente)

- **Nicho** não especificado: exemplos de “modelo” podem ser SKU, versão, ano, categoria técnica etc., conforme o segmento.
- **“Redondo”** aqui significa: MVP estável em produção + hardening, métricas, moderação básica e suporte inicial — **sem** obrigatoriedade de checkout in-app para a compra (fechamento **fora** do app).
- Uso de **IA** acelera boilerplate, testes e documentação; **não** substitui decisões de produto, homologação nas lojas, compliance e operação.

## Glossário rápido

- **MVP**: primeira versão utilizável com fluxo core (busca, detalhe, **contato** com anunciante, cadastro/publicação mínimos) — **sem** checkout da compra no app.
- **MMP**: produto minimamente *marketável* com qualidade de marca e sustentação.

---

*Última atualização: maio/2026 — documento vivo; revisar após workshop de descoberta com o cliente.*
