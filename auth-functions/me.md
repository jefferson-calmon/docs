---
title: "me"
description: "Retorna dados do usuário autenticado combinando Auth e perfil local."
---

## Endpoint

`GET /me`

## Headers obrigatórios

- `x-client-app`: id do app cliente.
- `Authorization: Bearer <access_token>`.

## Resposta 200

```json
{
  "user": {
    "id": "uuid",
    "email": "usuario@dominio.com",
    "email_confirmed_at": "2026-01-01T10:00:00.000Z",
    "last_sign_in_at": "2026-01-10T12:30:00.000Z",
    "name": "Nome do Usuário",
    "phone": "+55...",
    "document": "12345678901",
    "document_type": "cpf"
  }
}
```

## Erros

- `400` header `x-client-app` ausente.
- `401` token ausente/inválido/expirado.
- `404` perfil do usuário não encontrado em `api.users`.
- `405` método diferente de `GET`.
- `500` erro inesperado.
