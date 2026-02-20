---
title: "sso-enrollment"
description: "Inicia (ou reutiliza) processo de unificação de contas SSO por e-mail."
---

## Endpoint

`POST /sso-enrollment`

## Headers obrigatórios

- `x-client-app`: app que iniciou a unificação.

## Body

```json
{
  "userId": "id_do_usuario_no_app_origem",
  "userEmail": "usuario@dominio.com"
}
```

## Resposta 200

```json
{
  "enrollment_id": "uuid",
  "status": "started",
  "is_single_email": false,
  "accounts": [
    {
      "id": "uuid",
      "app_id": "calcmed_eletro",
      "app_name": "Calcmed Eletro",
      "user_id": "...",
      "user_email": "usuario@dominio.com",
      "is_verified": false,
      "is_primary": true
    }
  ]
}
```

## Erros

- `400` payload inválido ou ausência de `x-client-app`.
- `405` método diferente de `POST`.
- `500` falhas internas no processo.

## Observações

- Se já existir enrollment para o `userId`, o endpoint retorna o enrollment atual.
