# Usuários

## Criação de Usuário

Para criar um usuário, é necessário realizar uma requisição POST para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">POST</i>
        <h6>/api/v1/users</h6>
    </div>
</div>

Veja a seguir um exemplo do corpo da requisição:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  http://localhost:3000/api/v1/users/ \
  -H 'authorization: Token token=c3b1164e8ae17f6d9712730ec75be6da' \
  -H 'content-type: application/json' \
  -d '{
      "user": {
        "email": "foo@bar.com",
        "name": "Arthur Dent"
      }
    }'


EXEMPLO DE RESPOSTA

{
  "user": {
    "id": 2,
    "name": "Arthur Dent",
    "email": "foo@bar.com",
    "auth_provider": "nexaas_id",
    "uuid": "4dc677bd-c23e-4618-911c-a6c80d5797b4",
    "created_at": "2019-06-17T09:51:51.558-03:00",
    "updated_at": "2019-06-17T09:51:51.558-03:00"
  }
}

EXEMPLO DE RETORNO DE ERROS

{
    "errors": "E-mail para convite não é válido",
    "error_details": [
        {
            "email": [
                { "error":  "invalid" }
            ]
        }
    ]
}


```

    Campo                       |  Obrigatório  |     Tipo                |    Formato e tamanho         |   Observações
--------------------------------|---------------|-------------------------|------------------------------|-----------------------------------------------------------
    email                       |  Sim          |     Texto               |   Até 60 caracteres          |
    name                        |  Não          |     Texto               |   Até 60 caracteres          |

## Exclusão de Usuário

Para excluir um usuário da conta, é necessário realizar uma requisição DELETE para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-warning">DELETE</i>
        <h6>/api/v1/users/{:user_id}</h6>
    </div>
</div>


Veja a seguir um exemplo do corpo da requisição:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X DELETE \
  http://localhost:3000/api/v1/users/1 \
  -H 'authorization: Token token=c3b1164e8ae17f6d9712730ec75be6da' \
  -H 'content-type: application/json' \
```
