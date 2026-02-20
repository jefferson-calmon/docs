---
title: "sso-account"
description: "Adiciona conta ao enrollment SSO ou inicia a fase de verificação das contas vinculadas."
---

## Endpoint

`POST /sso-account`

## Headers obrigatórios

- `x-client-app`: app cliente atual.

## Body

### Ação `add_account`

```json
{
  "action": "add_account",
  "enrollmentId": "uuid",
  "email": "usuario@dominio.com"
}
```

### Ação `start_verification`

```json
{
  "action": "start_verification",
  "enrollmentId": "uuid"
}
```

## Respostas

- `200` para `start_verification`:

```json
{
  "status": "verification_started"
}
```

- `201` para `add_account` com conta criada:

```json
{
  "account_id": "uuid"
}
```

- `404` quando não houver conta legada para o e-mail informado:

```json
{
  "message": "Nenhuma conta encontrada para o email fornecido."
}
```

## Erros

- `400` payload inválido ou ausência de `x-client-app`.
- `405` método diferente de `POST`.
- `500` erro interno.
