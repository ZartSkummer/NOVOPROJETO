# Documento 2 — Grau de dificuldade com IA, prazo e linhas de código

## Uso de IA no desenvolvimento

| Aspecto | Avaliação |
|--------|-----------|
| **CRUD, telas, APIs REST, modelagem inicial** | IA acelera bastante |
| **Mapas, geolocalização, performance mobile** | IA ajuda; **ajuste fino e edge cases** ainda são humanos |
| **Antifraude, disputas, pagamentos, LGPD** | IA gera esboço; **decisão de negócio + jurídico + auditoria** são críticos |
| **Qualidade “redondo”** (observabilidade, testes, acessibilidade, lojas Apple/Google) | IA não substitui **processo** nem **homologação** |

**Conclusão:** dificuldade **alta** como produto; com IA a **velocidade do MVP sobe**, mas o **tempo até “redondo”** continua dominado por **negócio, compliance, UX real com usuários e estabilidade**.

## Prazo estimado (equipe pequena competente)

Interpretação de “redondo” = **produção estável**, pagamentos (se houver), moderação, painel admin, políticas, métricas, submissão nas lojas e primeira rodada de feedback corrigida.

| Fase | Conteúdo | Indicativo |
|------|-----------|------------|
| **MVP credível** | Cadastro, perfil, listagem/geo básica, chat ou contato controlado, avaliações simples, assinatura prestador | **4 a 7 meses** |
| **V1 “mercado”** | Disputas, antifraude básico, busca/filtros fortes, notificações, admin, relatórios, hardening | **+4 a 8 meses** |
| **Polimento contínuo** | Escala, A/B, otimização de conversão, novas categorias, integrações | **contínuo** |

**Total para “bem redondo”:** em geral **10 a 18 meses** calendário com time enxuto; com **time maior e escopo congelado**, dá para comprimir, mas raramente abaixo de **~8 meses** para algo sério com marketplace.

## Linhas de código — o que é LOC?

**LOC** significa **Lines of Code** (linhas de código): métrica que conta **linhas de código-fonte** de um programa ou projeto (às vezes incluindo comentários e testes, às vezes só código “executável”, dependendo da convenção).

- Serve como **ordem de grandeza** de tamanho do sistema, não como medida de qualidade.
- Projetos diferentes contam de formas diferentes (gerados por framework, testes, config).

## Estimativa de LOC para este tipo de produto

Depende de linguagem, monólito vs microserviços, testes, código gerado por framework, etc.

| Escopo | LOC (aprox., tudo incluído: app, API, admin, scripts, testes) |
|--------|------------------------------------------------------------------|
| MVP enxuto | **~40.000 – 90.000** |
| V1 robusta | **~100.000 – 250.000** |
| Grande escala / múltiplos apps | **250.000+** |

Isso é **estimativa de mercado**, não promessa: projetos “pequenos” no papel viram grandes por **logs, permissões, edge cases e refatoração**.
