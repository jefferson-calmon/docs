---
title: "reset-password"
description: "Redefine senha usando token e retorna nova sessão autenticada."
---

## Endpoint

`POST /reset-password`

## Body

```json
{
  "token": "token_de_reset",
  "new_password": "NovaSenha123"
}
```

Regras de `new_password`:

- mínimo 6 caracteres
- ao menos 1 letra maiúscula
- ao menos 1 letra minúscula
- ao menos 1 número ou caractere especial

## Resposta 200

```json
{
  "user": {
    "id": "uuid",
    "email": "usuario@dominio.com"
  },
  "auth_session": {
    "access_token": "...",
    "refresh_token": "...",
    "expires_in": 3600
  }
}
```

## Erros

- `400` corpo inválido, token inválido/expirado.
- `500` erro ao atualizar senha ou autenticar usuário após reset.

## Observações

- Registra telemetria de `reset_password`.
