# Documento 7 — Qualidade de código e entrega

A **referência normativa** (padrões de implementação, code smells, código morto, índices, migrações SQL idempotentes, pirâmide de testes, erros e logs, Definition of Done completa) está no **[10-handbook-padroes-desenvolvimento.md](./10-handbook-padroes-desenvolvimento.md)**. Este ficheiro resume o que importa no **fluxo de entrega** do Serviço Perto, sem duplicar o handbook.

## Prioridades de teste

- **Unitários** em regras de negócio.
- **Contrato** de API (schemas / OpenAPI / equivalente alinhado à stack).
- **E2E** nas jornadas críticas do produto (ex.: login, assinatura, criar pedido), em linha com a secção de testes do handbook.

## CI/CD

- Lint, typecheck, testes e build antes de integrar na linha principal.
- Scan de dependências (Snyk, Dependabot ou equivalente).

## Observabilidade

- Tracing ou correlação em fluxos de maior risco (ex.: pagamento, chat), conforme detalhe de logs e erros no handbook e em [05-seguranca-informacao.md](./05-seguranca-informacao.md).

## Definition of Done

- Aplicar a checklist do handbook (incluindo extensões **mobile-first** quando relevante).
- Qualquer excepção temporária (dívida técnica) deve ficar explícita num ticket ou nota curta em `/docs`, com plano de remoção.
