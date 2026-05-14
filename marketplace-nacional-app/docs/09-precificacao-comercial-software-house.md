# Precificação comercial — software house (Brasil, referência 2026)

> Valores **indicativos** para briefing de marketplace móvel nacional com filtros por localização e modelo, apps iOS/Android e backend cloud. **Premissa atual:** **sem** checkout in-app para a **compra do item** — vitrine + contato; pagamento **fora** do app. Ajustar por cidade da software house, porte da marca, SLAs e modelo de contrato (fixo vs time & material).

## 1. Como as casas costumam precificar

1. **Discovery/workshop** (1–3 semanas) faturado separadamente ou embutido.
2. **MVP fixo** com escopo fechado + cláusula de mudança (change request).
3. **Pós-MVP** em **time & material** (T&M) com squad mensal.
4. **Suporte e evolução** em retainer (10–30% do custo de desenvolvimento/ano).

## 2. Composição de squad (referência)

| Papel | Alocação MVP típica |
|-------|---------------------|
| PM/PO | 0,25–0,5 |
| UX/UI | 0,25–0,5 |
| Mobile (2 devs ou 1 sênior forte) | 1–1,5 |
| Backend | 0,75–1,25 |
| QA automação + manual | 0,25–0,5 |
| DevOps (parcial) | 0,15–0,3 |

**FTE** ≈ 2,5–4 pessoas-equivalente em picos.

## 3. Faixas de investimento (BRL)

### 3.1 MVP (10–14 semanas de build + buffer lojas)

- **R$ 250k – R$ 550k** — MVP enxuto, filtros cidade/UF + modelo, **sem** gateway de compra no app, admin mínimo ou apenas scripts internos.
- **R$ 450k – R$ 900k** — MVP “forte”: PostGIS/raio, moderação básica, painel admin simples, analytics, testes integração sólidos.

> A ausência de **pagamento C2C in-app** tende a **reduzir** risco e esforço (menos integrações financeiras, conciliação e chargeback no produto). **Não** elimina custo de moderação, busca e mídia.

### 3.2 Produto redondo / MMP (6–12 meses total incluindo MVP)

- **R$ 700k – R$ 1,5M** — hardening, anti-fraude básico, E2E estável, LGPD operacional, observabilidade madura, melhorias UX.
- **> R$ 1,5M até R$ 2,5M+** — cenários **não** exigidos pelo escopo atual de compra externa, exceto se o roadmap incluir **chat in-app** pesado, recomendação, múltiplos perfis PJ, integrações volumosas **ou** **futura** monetização transacional in-app (comissão, split, conciliação).

### 3.3 Custos recorrentes (não são “lucro da house”, mas entram no TCO do cliente)

- Cloud (compute, DB, busca, CDN, storage): ordem **R$ 3k–30k/mês** no primeiro ano conforme tráfego.
- Licenças (monitoramento, Auth enterprise, SCA): variável.
- Apple Developer + Google Play: taxas de programa de desenvolvedor (baixo vs projeto).

## 4. O que eleva o preço rapidamente

- **Se no futuro** houver **pagamento in-app** da compra: políticas das lojas + conciliação financeira + chargeback.
- **Anti-fraude** e moderação em tempo real.
- **Mapa** com clusters nacionais e performance.
- **Chat** com moderação e mídia.
- **Integrações** com ERPs de varejo ou APIs de terceiros instáveis.

## 5. Modelos de contrato sugeridos

- **MVP**: escopo fechado + cronograma + 2–3 rodadas de CR inclusas.
- **Roadmap**: T&M com teto mensal ou sprint fechado (2 semanas).
- **Garantia**: 30–90 dias de correção de defeito sem custo (não confundir com nova feature).

## 6. Comparativo de precificação por porte de fornecedor

| Porte | Percepção de risco | Faixa típica MVP |
|-------|--------------------|------------------|
| Boutique especializada | Baixa média | Mais cara por hora, menos retrabalho |
| Média software house | Média | Melhor custo/benefício |
| Grande integradora | Baixa para cliente enterprise | Caro; exige governança |

## 7. Proposta comercial — estrutura de documentos

1. Carta de intenção / NDA.
2. Proposta técnica (arquitetura resumida + stack).
3. Proposta comercial (fases, valores, premissas, exclusões).
4. Cronograma macro em marcos (MVP, beta, MMP).

## 8. Premissas para validação antes de assinar valor

- Nicho e taxonomia de “modelo” definidos.
- Política de exposição de dados de contato (e confirmação de que **não** há checkout no app).
- Decisão sobre mapa e GPS.
- Metas de carga (usuários simultâneos, anúncios/mês).

---

**Disclaimer**: não constitui proposta formal nem assessoria fiscal/jurídica; use com assessor comercial e contábil do seu negócio.
