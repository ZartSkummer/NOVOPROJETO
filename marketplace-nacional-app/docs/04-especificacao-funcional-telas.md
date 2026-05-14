# Especificação funcional — escopo, fluxos e inventário de telas

## 1. Personas

| Persona | Objetivo principal |
|---------|---------------------|
| Comprador | Encontrar itens por **local** e **modelo/atributo**, comparar, contatar. |
| Vendedor | Publicar anúncio com fotos e dados, gerenciar status e leads. |
| Operador | Moderar denúncias, suspender fraudes, suporte. |

## 2. Épicos de produto

1. **Descoberta e busca**: home, busca, filtros (localização + modelo), ordenação.
2. **Detalhe e confiança**: galeria, descrição, vendedor, denúncia, compartilhar.
3. **Conta e identidade**: cadastro, login, recuperação de senha, perfil.
4. **Publicação**: fluxo guiado de criação/edição de anúncio, rascunhos.
5. **Engajamento**: favoritos, alertas (fase 1 opcional: só favoritos).
6. **Operação**: painel admin web (recomendado desde MMP).

## 3. Regras de negócio (baseline — validar com cliente)

- Anúncio possui: título, descrição, preço, **localização** (cidade/UF e/ou coordenadas), **modelo** (ou SKU/atributo do nicho), fotos, categoria.
- Filtros combinados com paginação estável (evitar “pular” itens ao paginar).
- Geolocalização: opções comuns:
  - **A)** filtro por UF/município (mais simples);
  - **B)** raio em km a partir do CEP ou GPS do usuário (mais valor, mais complexidade/LGPD).
- Limite de fotos por anúncio e tamanho máximo por arquivo (ex.: 10 fotos, 8 MB cada — ajustar).

### 3.1 Decisão confirmada — pagamento da compra

- **Não** haverá checkout, PIX, cartão nem carteira **dentro do app** para o comprador pagar o **item anunciado**.
- O app oferece **contato** com o anunciante; **negociação, entrega e pagamento** são **100% fora** da plataforma.
- Métricas de produto devem refletir isso (ex.: “detalhe → contato” em vez de “detalhe → pagamento confirmado no app”).

## 4. Fluxos principais (user journeys)

### 4.1 Comprador — busca até contato (compra fora do app)

1. Abre app → home com destaques e atalhos de categoria.
2. Aplica filtros (estado, cidade, modelo).
3. Abre detalhe → vê fotos e dados → toca em **Contatar** (telefone, WhatsApp, e-mail ou link — definir política e LGPD).
4. **Fora do app:** combina com o anunciante, paga e recebe o bem/serviço pelos canais combinados.
5. Opcional no app: salva em favoritos.

> **Não** incluir telas de checkout, carrinho ou “pagar agora” para o item, salvo mudança formal de escopo.

### 4.2 Vendedor — publicar anúncio

1. Login/cadastro.
2. “Anunciar” → wizard (categoria → modelo → local → preço → fotos → revisão).
3. Envio → status “em análise” ou “publicado” (política de moderação).
4. Lista “meus anúncios” → editar, pausar, excluir.

## 5. Inventário de telas (app móvel)

Legenda: **MVP** = primeira entrega; **MMP** = produto comercializável.

### 5.1 Onboarding e autenticação

| # | Tela | MVP | Notas |
|---|------|-----|--------|
| T01 | Splash / checagem de sessão | Sim | Deep links para anúncio. |
| T02 | Onboarding (3–4 slides) | Sim | Foco em valor do nicho. |
| T03 | Login (e-mail/senha ou social) | Sim | Social depende de política do nicho. |
| T04 | Cadastro | Sim | Validação de e-mail/telefone. |
| T05 | Esqueci senha | Sim | — |
| T06 | Verificação OTP (se telefone) | Opcional | Aumenta confiança em C2C. |

### 5.2 Navegação principal

| # | Tela | MVP | Notas |
|---|------|-----|--------|
| T10 | Home (destaques, categorias, busca) | Sim | Entrada para filtros. |
| T11 | Lista de resultados (cards) | Sim | Estados: vazio, erro, loading skeleton. |
| T12 | Detalhe do anúncio | Sim | Galeria fullscreen. |
| T13 | Filtros (bottom sheet ou tela dedicada) | Sim | **Localização + modelo** obrigatórios no escopo. |
| T14 | Ordenação (relevância, preço, mais recente) | Sim | — |
| T15 | Mapa (pins próximos) | MMP | Nice-to-have forte em alguns nichos. |

### 5.3 Conta e favoritos

| # | Tela | MVP | Notas |
|---|------|-----|--------|
| T20 | Perfil do usuário | Sim | — |
| T21 | Editar perfil | Sim | LGPD: exportar/excluir conta (MMP). |
| T22 | Favoritos | Sim | — |
| T23 | Notificações (lista) | MMP | Depende de push + preferências. |
| T24 | Configurações (idioma, tema, privacidade) | MMP | Tema claro/escuro. |

### 5.4 Publicação (vendedor)

| # | Tela | MVP | Notas |
|---|------|-----|--------|
| T30 | Meus anúncios (lista + status) | Sim | — |
| T31 | Criar anúncio — passo 1 (categoria/modelo) | Sim | — |
| T32 | Criar anúncio — passo 2 (localização) | Sim | CEP/autocomplete cidade. |
| T33 | Criar anúncio — passo 3 (preço, atributos) | Sim | Atributos dinâmicos por categoria. |
| T34 | Criar anúncio — passo 4 (fotos) | Sim | Crop leve, ordem das fotos. |
| T35 | Revisão e publicar | Sim | Termos de uso. |
| T36 | Editar anúncio | Sim | Reprocessamento de mídia. |

### 5.5 Confiança e segurança

| # | Tela | MVP | Notas |
|---|------|-----|--------|
| T40 | Denunciar anúncio | Sim | Motivos pré-definidos. |
| T41 | Central de ajuda / FAQ | MMP | Reduz suporte. |
| T42 | Termos e política de privacidade | Sim | WebView ou nativo. |

### 5.6 Admin (web — fora do app, recomendado MMP)

| # | Tela | MVP | Notas |
|---|------|-----|--------|
| A01 | Login admin | Não | Role separada. |
| A02 | Fila de moderação | Não | Ações: aprovar, suspender. |
| A03 | Busca de usuários/anúncios | Não | Auditoria. |
| A04 | Dashboard métricas | Não | Funil publicação, DAU. |

## 6. Critérios de aceite (exemplos)

- **CA-B01**: Dado filtros válidos, a listagem retorna em **< 2s** em rede 4G mediana para página 1 (meta; medir em testes de campo).
- **CA-B02**: Ao mudar cidade, a URL interna/deep link reflete estado para compartilhamento (se aplicável).
- **CA-L01**: Usuário consegue salvar rascunho e retomar publicação após fechar o app.
- **CA-S01**: Denúncia registra evidência mínima e retorna confirmação ao usuário.

## 7. Fora de escopo inicial (explícito)

- **Checkout / pagamento da compra no app** (PIX, cartão, carteira, escrow na plataforma) — **decisão atual: fora do escopo**; compra é por **contato externo**.
- Leilão em tempo real.
- Motor de crédito/score (depende de parceiros e compliance).

## 8. Métricas de sucesso (produto)

- Taxa de conversão busca → detalhe → **contato iniciado** (clique ligação/WhatsApp etc.).
- Tempo médio até primeiro anúncio publicado (vendedor).
- NPS ou CSAT pós-contato (MMP).
