---
title: "sso-account-verification"
description: "Envia e valida OTP de verificação para contas vinculadas no enrollment SSO."
---

## Endpoint

`POST /sso-account-verification`

## Body

### Ação `send`

```json
{
  "action": "send",
  "accountId": "uuid"
}
```

### Ação `verify`

```json
{
  "action": "verify",
  "accountId": "uuid",
  "code": "123456"
}
```

## Respostas

- `200` na ação `send`:

```json
{
  "message": "Código de verificação gerado com sucesso. Envio está em modo simulado."
}
```

- `200` na ação `verify`:

```json
{
  "account_id": "uuid",
  "verified_at": "2026-01-10T12:00:00.000Z"
}
```

## Erros

- `400` payload inválido, conta inexistente ou código OTP inválido/expirado.
- `405` método diferente de `POST`.
- `500` erro interno.

## Observações

- OTP possui 6 dígitos e expira em 10 minutos.
- Quando todas as contas ficam verificadas, o enrollment avança para `waiting_password_set`.
