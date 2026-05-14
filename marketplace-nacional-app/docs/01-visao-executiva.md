# Visão executiva — decisão go/no-go

## O que o cliente pediu (síntese)

Aplicativo **móvel nativo ou multiplataforma** para **iOS e Android** (distribuição pelas lojas), com **listagens de venda**, **filtros por localização** e por **modelo** (ou atributo equivalente do nicho), **abrangência nacional**, posicionado como referência de um segmento — **análogo ao Webmotors**, porém **outro nicho**.

## Respostas diretas (ordem de grandeza)

| Dimensão | Avaliação |
|----------|-----------|
| **Dificuldade técnica** | **Média a alta** para produto nacional “redondo”: backend escalável, busca, geolocalização, moderação, publicação nas lojas, observabilidade e segurança. |
| **Dificuldade com uso de IA** | **Média**: IA reduz tempo em código repetitivo, testes e docs; **não** elimina risco regulatório (LGPD), revisão Apple/Google, integrações reais (maps, push, analytics) e qualidade de dados. |
| **Prazo até “redondo”** | **6 a 12 meses** calendário com time pequeno/médio (2–6 pessoas), dependendo de pagamentos no app, nível de moderação e volume de integrações. **MVP utilizável**: **3 a 5 meses**. |
| **Linhas de código (LOC)** | **~80k a 250k LOC** no conjunto app(s) + backend + infra como código + testes — varia muito com monorepo, % de código gerado e escopo de pagamento/chat. |
| **Software house (Brasil, 2026)** | **R$ 350k a R$ 1,5M+** para MVP→MMP com time dedicado; valores **acima de R$ 2M** se houver marketplace financeiro pesado, anti-fraude avançado ou time maior/long tail de features. |

> Valores e prazos assumem equipe experiente e cliente com decisões rápidas. Atrasos típicos vêm de escopo flutuante, fila de revisão das lojas e integrações com terceiros.

## Riscos que mais impactam prazo e custo

1. Políticas **Apple/Google** (pagamentos digitais, conteúdo gerado por usuário, classificação etária).
2. **LGPD** e base legal para dados de localização e perfil.
3. **Fraude** e qualidade de anúncios (bots, duplicatas, golpes).
4. **Performance de busca** nacional (índices, cache, CDN).
5. Dependência de **APIs externas** (mapas, SMS, e-mail transacional) sem fallbacks.

## Recomendação estratégica

1. Fechar **nicho**, **monetização** (assinatura anunciante, comissão, destaque pago) e **MVP** em workshop de 1–2 dias.
2. Entregar **MVP** com métricas e painel mínimo; iterar com dados reais.
3. Tratar **moderação e segurança** desde o MVP (mesmo que simples), não como “fase 2”.

## Próximos passos sugeridos

- Ler [02-dificuldade-prazo-estimativas.md](./02-dificuldade-prazo-estimativas.md) e [09-precificacao-comercial-software-house.md](./09-precificacao-comercial-software-house.md).
- Validar inventário de telas em [04-especificacao-funcional-telas.md](./04-especificacao-funcional-telas.md).
