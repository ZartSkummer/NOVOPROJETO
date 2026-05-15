# Handbook — Padrões de desenvolvimento (Cursor e equipa)

Este documento é a **referência normativa** para construir e evoluir o software com **consistência**, **segurança**, **manutenibilidade** e **rastreabilidade**. Complementa os documentos [03-arquitetura.md](./03-arquitetura.md), [06-dba-dados.md](./06-dba-dados.md), [07-qualidade-codigo-entrega.md](./07-qualidade-codigo-entrega.md) e [05-seguranca-informacao.md](./05-seguranca-informacao.md).

---

## 1. Princípios gerais

- **Explicitar contratos**: APIs, modelos de dados e limites de entrada documentados ou expressos em código tipado/validado (schemas).
- **Menor surpresa**: pastas, nomes e fluxos previsíveis; decisões não óbvias registadas em ADR ou nota curta em `/docs`.
- **Segurança e privacidade por defeito**: validar todas as entradas, princípio do menor privilégio, dados sensíveis nunca em logs nem em repositório.
- **Evolução sem medo**: mudanças de esquema via migrações controladas; comportamento coberto por testes onde o risco for médio ou alto.

---

## 2. Base de dados e DBA

### 2.1 Índices (obrigatório para tabelas em produção)

- **Toda tabela** com expectativa de crescimento e consultas frequentes deve ter **estratégia de indexação** definida no desenho, não “adivinhada” depois.
- Criar índices para:
  - **chaves estrangeiras** e colunas usadas em `JOIN`, `WHERE`, `ORDER BY` e agregações recorrentes;
  - **unicidade** de negócio (constraints `UNIQUE` + índice implícito ou explícito);
  - **consultas geo/texto** conforme stack (ex.: GIST, `pg_trgm`) — alinhar com [06-dba-dados.md](./06-dba-dados.md).
- Evitar índices redundantes; rever planos de execução em queries críticas após mudanças de volume.
- Documentar em nota de migração ou em `/docs` quando um índice existir **só** por motivo de performance (contexto + query alvo).

### 2.2 Integridade e modelo

- Uso consistente de **FKs**, tipos adequados, **NOT NULL** onde o domínio o exija, defaults explícitos quando fizer sentido.
- **Soft delete** e auditoria em entidades críticas, alinhado ao modelo acordado.

### 2.3 Migrações SQL

- Quando uma atualização do sistema **alterar persistência**, deve existir **script SQL idempotente** (pode executar mais de uma vez sem corromper estado), corrigindo ou alinhando a versão anterior do esquema.
- **Convenção de nome**: `yyyy-mm-dd_hh-mm_nomedoscript.sql` (data/hora UTC ou timezone acordado pela equipa, **uma** convenção para todo o projeto).
- Ordem de deploy: compatibilidade **expand–contract** quando possível (adicionar coluna → backfill → tornar obrigatório → remover antigo), documentado se for multi-passos.

---

## 3. Qualidade de código e padronização

### 3.1 Ausência de code smells e código morto

- **Code smells** (métodos longos demais, classes com demasiadas responsabilidades, duplicação descontrolada, acoplamento forte a implementações, números mágicos sem constante, APIs genéricas demais) devem ser **refactorados** quando tocados ou quando o risco for baixo; não acumular “dívida consciente” sem ticket ou ADR.
- **Dead code** (funções, imports, branches, flags, ficheiros não referenciados) **não** permanece no repositório: remover ou reativar com teste e propósito documentado.
- Ferramentas de análise estática (linters, regras de complexidade, deteção de unused) fazem parte do **fluxo obrigatório** (local + CI), alinhado a [07-qualidade-codigo-entrega.md](./07-qualidade-codigo-entrega.md).

### 3.2 Melhores práticas de implementação

- **SOLID** e **separação de camadas**: regras de negócio isoladas de framework, UI e detalhes de persistência onde a stack o permitir.
- **DRY com critério**: abstrair só após repetição estável; evitar utilitários prematuros que obscurecem o fluxo.
- **Nomes claros** (domínio do negócio em português ou inglês, **uma** língua por módulo acordada); funções pequenas; early return para reduzir aninhamento.
- **Formatação única** (Prettier, Black, gofmt, etc.) e **estilo** acordado; commits não debatem espaços — a ferramenta decide.
- **Tipagem** forte onde disponível; evitar `any`/casts desnecessários que escondem erros.
- **Imutabilidade preferida** para dados partilhados; efeitos colaterais localizados e explícitos.
- **Assíncrono**: cancelamento/timeouts onde houver I/O; tratamento de corrida e idempotência em operações críticas.

### 3.3 Revisão e consistência

- Pull requests **pequenos** e com descrição do impacto (API, DB, UX).
- **Definition of Done** alinhada à secção 7 deste handbook.

---

## 4. Segurança e vulnerabilidades

- Minimizar superfície de ataque: dependências atualizadas, scan automatizado, segredos só em cofre/variáveis de ambiente.
- Checklist OWASP adaptado à stack (injeção, XSS, CSRF quando aplicável, controlo de acesso por recurso, uploads seguros).
- Detalhes operacionais em [05-seguranca-informacao.md](./05-seguranca-informacao.md).

---

## 5. Testes

- **Cada funcionalidade e ação** com impacto em negócio ou dados deve ter **teste automatizado** associado: preferencialmente **unitário** para regras puras; **integração** para persistência, filas e serviços externos (com doubles); **E2E** para um conjunto **reduzido** de jornadas críticas.
- Correção de bug grave ou regressão: incluir **teste que falhava antes** da correção.
- CI: lint, typecheck, testes e build antes de merge — ver [07-qualidade-codigo-entrega.md](./07-qualidade-codigo-entrega.md).

---

## 6. UX, validação e erros

- **Campos de entrada**: limites máximos (e mínimos quando aplicável) de caracteres alinhados ao modelo de dados e à UX; máscaras/formatos onde fizer sentido; validação no cliente **e** no servidor.
- **Mensagens de erro**: linguagem clara para o utilizador; **nunca** expor stack traces nem detalhes internos. Em paralelo, registo técnico com **correlação** (ex.: request id) para suporte.
- Estados de UI: carregamento, vazio, sucesso, erro, sem permissão — ver [04-inventario-telas-ux-ui.md](./04-inventario-telas-ux-ui.md).

---

## 7. Bugs e robustez

- Evitar classes de falha sistémica: estados inconsistentes, duplo envio, falta de transação onde a atomicidade é obrigatória, N+1 em listagens, ausência de paginação em coleções grandes.
- Comportamento indefinido deve ser **tratado** (erro controlado ou valor por defeito documentado), não ignorado.

---

## 8. Documentação em `/docs`

- Documentação **nasce e evolui** com o produto: ficheiros **pequenos**, **focados** e **padronizados**.
- Abrangência desde **visão e padrões de arquitetura** até **detalhe da tarefa** (critérios de aceitação, impacto em API/DB).
- Índice central: [00-INDEX.md](./00-INDEX.md). Novos temas: novo ficheiro numerado ou ADR, com ligação no índice.

---

## 9. Definition of Done (síntese)

- [ ] Requisitos e critérios de aceitação claros (ou doc atualizado).
- [ ] Código sem dead code introduzido; linters e typecheck verdes.
- [ ] Testes adequados ao risco da alteração.
- [ ] Migração SQL idempotente e nomeada se houver mudança de persistência.
- [ ] Índices e constraints revistos para novas colunas/consultas.
- [ ] Erros tratados de forma amigável; logs técnicos sem dados sensíveis.
- [ ] Documentação em `/docs` atualizada quando a mudança alterar contrato, fluxo ou operação.

---

## 10. Uso com o Cursor

Ao pedir implementação, referenciar **secções** deste handbook e o **doc de feature** correspondente. O agente deve priorizar segurança, testes, migrações idempotentes, índices e mensagens de erro conforme acima.

---

*Documento vivo — revisões devem manter compatibilidade com o índice e com os documentos 03–07.*
