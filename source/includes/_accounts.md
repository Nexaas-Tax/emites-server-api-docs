# Contas

## Criação de conta

É possível criar uma conta via API do Emites já com um usuário administrador.

<aside class="notice">
  É necessário que a conta autenticada (dona do Token enviado na requisição) tenha permissão para criar outras contas.
</aside>

Uma vez que a conta esteja autorizada, é necessário realizar uma requisição POST para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">POST</i>
        <h6>/api/v1/accounts</h6>
    </div>
</div>

Veja a seguir um exemplo do corpo da requisição:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  https://app.production.emites.com.br/api/v1/accounts/ \
  -H 'authorization: Bearer c3b1164e8ae17f6d9712730ec75be6da' \
  -H 'content-type: application/json' \
  -d '{
      "account": {
        "name": "Nome da conta",
        "admin_email": "foo@bar.com"
      }
    }'


EXEMPLO DE RESPOSTA

{
  "account": {
    "id": 8,
    "name": "Nome da conta",
    "user_id": 6,
    "user_ids": [],
    "api_token": "552a0d7d67d2f77b6b6908a3070b5a06",
    "created_at": "2019-06-24T15:58:51.866-03:00",
    "updated_at": "2019-06-24T15:58:51.866-03:00",
    "account_creator": false,
    "account_id": 1,
    "admin": {
      "id": 6,
      "name": "foo@bar.com",
      "email": "foo@bar.com",
      "auth_provider": "nexaas_id",
      "created_at": "2019-06-24T15:58:51.855-03:00",
      "updated_at": "2019-06-24T15:58:51.855-03:00",
      "uuid": "47d4738f-db19-46e9-a305-7bfbbb964f77"
    }
  }
}

EXEMPLO DE RETORNO DE ERROS

{
    "errors": [
        {
            "name": ["não pode ficar em branco"]
        }
    ],
    "error_details": [
        {
            "name": [
                { "error": "blank" }
            ]
        }
    ]
}
```


    Campo                       |  Obrigatório  |     Tipo                |    Formato e tamanho         |   Observações
--------------------------------|---------------|-------------------------|------------------------------|-----------------------------------------------------------
    name                        |  Sim          |     Texto               |                              |   Nome para identificação da conta.
    admin_email                 |  Não          |     Texto               |                              |   E-mail válido do primeiro usuário que será criado ou vinculado à nova conta.
