---
title: "sso-complete"
description: "Conclui a unificação SSO criando/atualizando usuário Auth e consolidando vínculos de app."
---

## Endpoint

`POST /sso-complete`

## Body

```json
{
  "enrollmentId": "uuid",
  "password": "NovaSenha123"
}
```

Regras de `password`:

- mínimo 6 caracteres
- ao menos 1 letra maiúscula
- ao menos 1 letra minúscula
- ao menos 1 número ou caractere especial

## Resposta 200

```json
{
  "enrollment_id": "uuid",
  "status": "completed",
  "user": {
    "id": "uuid",
    "email": "usuario@dominio.com"
  }
}
```

## Erros

- `400` enrollment não pronto para conclusão, contas não verificadas ou payload inválido.
- `409` enrollment já concluído ou conflito de usuário local por e-mail/id.
- `500` falhas ao criar/atualizar usuário Auth, vincular apps ou persistir conclusão.

## Observações

- O endpoint garante usuário no Auth e em `api.users` antes de concluir.
- Consolida vínculos em `api.user_apps` com `upsert`.
