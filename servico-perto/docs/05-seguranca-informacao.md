# Documento 5 — Segurança da informação (mínimo aceitável)

## LGPD

- Bases legais, DPA com fornecedores, política de retenção, exportação/exclusão, registro de tratamento.

## Dados sensíveis

- Minimizar coleta; criptografia em trânsito (TLS) e em repouso; segredos em vault.

## Conta e sessão

- MFA opcional; rate limit; proteção a enumeração de usuários.

## Upload de mídia

- Antivírus/validação, limite de tamanho, stripping de metadados EXIF se necessário.

## Pagamentos

- PCI via PSP (não armazenar PAN); webhooks assinados e idempotentes.

## Moderação

- Pipeline para denúncias; logs de ações admin.

## App mobile

- Certificate pinning (avaliar custo); jailbreak/root warnings para fluxos críticos.
