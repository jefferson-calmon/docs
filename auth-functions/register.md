---
title: "register"
description: "Cria usuário no Auth, espelha em api.users e já retorna sessão para login imediato."
---

## Endpoint

`POST /register`

## Headers obrigatórios

- `x-client-app`: id do app (tabela `api.apps`).

## Body

```json
{
  "name": "Nome Sobrenome",
  "email": "usuario@dominio.com",
  "document": "12345678901",
  "document_type": "cpf",
  "phone": "+5511999999999",
  "password": "Senha123"
}
```

Campos obrigatórios: `name`, `email`, `document`, `password`.

## Resposta 201

```json
{
  "user": {
    "id": "uuid",
    "email": "usuario@dominio.com",
    "name": "Nome Sobrenome"
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

Para provider Firebase, `app_session` retorna `custom_token`.

## Erros

- `400` método inválido, payload inválido, app inválido, CPF/e-mail inválidos, senha curta.
- `409` usuário já existe (por e-mail ou documento).
- `500` falha ao criar perfil local ou erro inesperado.

## Observações

- Cria registros em `api.users`, `api.user_apps` e `api.audit_events`.
- `document_type` padrão é `cpf` quando não enviado.
