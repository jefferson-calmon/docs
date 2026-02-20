---
title: "check-email"
description: "Verifica em quais apps legados existe conta para um e-mail."
---

## Endpoint

`POST /check-email`

## Body

```json
{
  "email": "usuario@dominio.com"
}
```

## Resposta 200

```json
{
  "email": "usuario@dominio.com",
  "apps": [
    {
      "id": "calcmed_eletro",
      "name": "Calcmed Eletro",
      "user_id": "...",
      "registered_at": "2026-01-01T10:00:00.000Z"
    }
  ]
}
```

## Erros

- `400` corpo inválido (validação do `email`).
- `500` erro interno ao consultar apps legados.

## Observações

- O endpoint normaliza o e-mail para minúsculas e remove espaços.
- O retorno `apps` contém somente aplicativos em que a conta foi encontrada.
