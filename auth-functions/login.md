---
title: "login"
description: "Autentica usuário por e-mail/CPF e emite sessão do Auth + token por app."
---

## Endpoint

`POST /login`

## Headers obrigatórios

- `x-client-app`: id do app (tabela `api.apps`).

## Body

```json
{
  "identifier": "usuario@dominio.com",
  "password": "SuaSenha123"
}
```

`identifier` pode ser e-mail ou CPF.

## Resposta 200

```json
{
  "user": {
    "id": "uuid",
    "email": "usuario@dominio.com"
  },
  "auth": {
    "access_token": "...",
    "refresh_token": "...",
    "expires_in": 3600
  },
  "app_session": {
    "type": "supabase",
    "app_id": "calcmed_eletro",
    "access_token": "...",
    "expires_in": 3600
  }
}
```

Para apps Firebase, `app_session` retorna `custom_token`.

## Erros

- `400` campos obrigatórios ausentes, app inválido, e-mail/CPF inválidos.
- `401` usuário não encontrado ou credenciais inválidas.
- `429` usuário bloqueado por excesso de tentativas.
- `500` erro inesperado.

## Observações

- Atualiza `api.users`, `api.user_apps`, `api.audit_events` e `login_attempts`.
- O controle de lockout é aplicado antes da autenticação.
