---
title: "forgot-password"
description: "Inicia recuperação de senha por e-mail ou CPF, sem expor existência de usuário."
---

## Endpoint

`POST /forgot-password`

## Body

```json
{
  "identifier": "usuario@dominio.com"
}
```

Também aceita CPF no campo `identifier`.

## Resposta 200

```json
{
  "message": "Se o identificador informado estiver cadastrado, você receberá um e-mail com instruções para redefinir sua senha."
}
```

## Erros

- `400` corpo inválido (identifier ausente/inválido).
- `500` falha interna (ex.: URL de redirecionamento inválida, erro ao enviar e-mail).

## Observações

- Sempre retorna sucesso para evitar enumeração de usuários.
- Requer variável de ambiente `FORGOT_PASSWORD_REDIRECT_URL`.
