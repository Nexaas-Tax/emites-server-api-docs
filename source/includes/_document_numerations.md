# Série de notas fiscais

Para criar séries de notas fiscais você precisa ter ao menos uma organização cadastrada.
<p>Você pode verificar como criar organizações em [Criação de organizações](#cria-o-de-organiza-es)</p>


## Listar séries NF-e

Para listar séries de NF-e, é necessário realizar uma requisição GET para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">GET</i>
        <h6>/api/v1/organizations/{organization_id}/nfe_numerations</h6>
    </div>
</div>

Veja a seguir um exemplo do corpo da requisição:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/1/nfe_numerations \
  -H 'authorization: Bearer c3b1164e8ae17f6d9712730ec75be6da' \
  -H 'content-type: application/json'

EXEMPLO DE RESPOSTA

{
  "nfe_numeration": [
    {
      "id": 1,
      "serie": 1,
      "last_number": 10,
      "created_at": "2019-01-31T14:05:11.733-03:00",
      "updated_at": "2019-01-31T14:05:11.733-03:00"
    },
    {
      "id": 2,
      "serie": 2,
      "last_number": 20,
      "created_at": "2019-01-31T14:05:11.733-03:00",
      "updated_at": "2019-01-31T14:05:11.733-03:00"
    }
  ]
}
```

## Criar série NF-e

Para criar uma série de NF-e, é necessário realizar uma requisição POST para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">POST</i>
        <h6>/api/v1/organizations/{organization_id}/nfe_numerations</h6>
    </div>
</div>

Veja a seguir um exemplo do corpo da requisição:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/1/nfe_numerations \
  -H 'authorization: Bearer c3b1164e8ae17f6d9712730ec75be6da' \
  -H 'content-type: application/json' \
  -d '{
      "nfe_numeration": {
        "serie": 1,
        "last_number": "100",
      }
    }'

EXEMPLO DE RESPOSTA

{
  "nfe_numeration": {
    "id": 1,
    "serie": 1,
    "last_number": 100,
    "created_at": "2019-01-31T14:05:11.733-03:00",
    "updated_at": "2019-01-31T14:05:11.733-03:00"
  }
}


EXEMPLO DE RETORNO DE ERROS

{
    "errors": [
        {
            "serie": [
                "não pode ficar em branco"
            ],
            "last_number": [
                "não pode ficar em branco"
            ]
        }
    ],
    "error_details": [
        {
            "serie": [
                { "error": "blank" }
            ],
            "last_number": [
                { "error": "blank" }
            ]
        }
    ]
}
```

    Campo                       |  Obrigatório  |     Tipo                |    Formato e tamanho         |   Observações
--------------------------------|---------------|-------------------------|------------------------------|-----------------------------------------------------------
    serie                       |  Sim          |     Numérico            |                              |
    last_number                 |  Sim          |     Numérico            |                              |

## Exibir série NF-e

Para exibir uma série de NF-e, é necessário realizar uma requisição GET para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">GET</i>
        <h6>/api/v1/organizations/{organization_id}/nfe_numerations/:id</h6>
    </div>
</div>

Veja a seguir um exemplo do corpo da requisição:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/1/nfe_numerations/1 \
  -H 'authorization: Bearer c3b1164e8ae17f6d9712730ec75be6da' \
  -H 'content-type: application/json'

EXEMPLO DE RESPOSTA

{
  "nfe_numeration": {
    "id": 1,
    "serie": 1,
    "last_number": 100,
    "created_at": "2019-01-31T14:05:11.733-03:00",
    "updated_at": "2019-01-31T14:05:11.733-03:00"
  }
}
```

## Excluir série NF-e

Para excluir uma série de NF-e, é necessário realizar uma requisição DELETE para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-warning">DELETE</i>
        <h6>/api/v1/organizations/{organization_id}/nfe_numerations/{id}</h6>
    </div>
</div>

Veja a seguir um exemplo do corpo da requisição:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X DELETE \
  https://app.production.emites.com.br/api/v1/organizations/1/nfe_numerations/1 \
  -H 'authorization: Bearer c3b1164e8ae17f6d9712730ec75be6da' \
  -H 'content-type: application/json' \
```
<aside class="notice">
  Não é possível remover uma <strong>série</strong> caso a mesma esteja vinculada a um <strong>documento</strong>.
</aside>

```
{
  "errors": [
      {
          "base": [
              "Não foi possível excluir essa série de notas pois ela está vinculada a um documento"
          ]
      }
  ],
  "error_details": [
      {
          "base": [
              { "error": "default" }
          ]
      }
  ]
}
```

## Listar séries NFC-e

Para listar séries de NFC-e, é necessário realizar uma requisição GET para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">GET</i>
        <h6>/api/v1/organizations/{organization_id}/nfce_numerations</h6>
    </div>
</div>

Veja a seguir um exemplo do corpo da requisição:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/1/nfce_numerations \
  -H 'authorization: Bearer c3b1164e8ae17f6d9712730ec75be6da' \
  -H 'content-type: application/json'

EXEMPLO DE RESPOSTA

{
  "nfce_numeration": [
    {
      "id": 1,
      "serie": 1,
      "emission_type": "standard",
      "last_number": 10,
      "created_at": "2019-01-31T14:05:11.733-03:00",
      "updated_at": "2019-01-31T14:05:11.733-03:00"
    },
    {
      "id": 2,
      "serie": 2,
      "emission_type": "offline_contingency",
      "last_number": 20,
      "created_at": "2019-01-31T14:05:11.733-03:00",
      "updated_at": "2019-01-31T14:05:11.733-03:00"
    }
  ]
}
```

## Criar série NFC-e

Para criar uma série de NFC-e, é necessário realizar uma requisição POST para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">POST</i>
        <h6>/api/v1/organizations/{organization_id}/nfce_numerations</h6>
    </div>
</div>

Veja a seguir um exemplo do corpo da requisição:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/1/nfce_numerations \
  -H 'authorization: Bearer c3b1164e8ae17f6d9712730ec75be6da' \
  -H 'content-type: application/json' \
  -d '{
      "nfce_numeration": {
        "serie": 1,
        "emission_type": "standard",
        "last_number": "100"
      }
    }'

EXEMPLO DE RESPOSTA

{
  "nfce_numeration": {
    "id": 1,
    "serie": 1,
    "last_number": 100,
    "emission_type": "standard",
    "created_at": "2019-01-31T14:05:11.733-03:00",
    "updated_at": "2019-01-31T14:05:11.733-03:00"
  }
}

EXEMPLO DE RETORNO DE ERROS

{
    "errors": [
        {
            "serie": [
                "não pode ficar em branco"
            ],
            "last_number": [
                "não pode ficar em branco"
            ],
            "emission_type": [
                "não pode ficar em branco"
            ]
        }
    ],
    "error_details": [
        {
            "serie": [
                { "error": "blank" }
            ],
            "last_number": [
                { "error": "blank" }
            ]
        }
    ]
}
```

    Campo                       |  Obrigatório  |     Tipo                |    Formato e tamanho                  |   Observações
--------------------------------|---------------|-------------------------|---------------------------------------|-----------------------------------------------------------
    serie                       |  Sim          |     Numérico            |                                       |
    last_number                 |  Sim          |     Numérico            |                                       |
    emission_type               |  Sim          |     Texto               |  'standard' ou 'offline_contingency'  |   Indica o tipo de emissão:<br> standard = Emissão Normal;<br>  offline_contingency = Emissão em Contingência Offline.
## Exibir série NFC-e

Para exibir uma série de NFC-e, é necessário realizar uma requisição GET para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">GET</i>
        <h6>/api/v1/organizations/{organization_id}/nfce_numerations/:id</h6>
    </div>
</div>

Veja a seguir um exemplo do corpo da requisição:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/1/nfce_numerations/1 \
  -H 'authorization: Bearer c3b1164e8ae17f6d9712730ec75be6da' \
  -H 'content-type: application/json'

EXEMPLO DE RESPOSTA

{
  "nfce_numeration": {
    "id": 1,
    "serie": 1,
    "emission_type": "standard",
    "last_number": 100,
    "created_at": "2019-01-31T14:05:11.733-03:00",
    "updated_at": "2019-01-31T14:05:11.733-03:00"
  }
}
```

## Excluir série NFC-e

Para excluir uma série de NFC-e, é necessário realizar uma requisição DELETE para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-warning">DELETE</i>
        <h6>/api/v1/organizations/{organization_id}/nfce_numerations/{id}</h6>
    </div>
</div>

Veja a seguir um exemplo do corpo da requisição:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X DELETE \
  https://app.production.emites.com.br/api/v1/organizations/1/nfce_numerations/1 \
  -H 'authorization: Bearer c3b1164e8ae17f6d9712730ec75be6da' \
  -H 'content-type: application/json' \
```

<aside class="notice">
  Não é possível remover uma <strong>série</strong> caso a mesma esteja vinculada a um <strong>documento</strong>.
</aside>

```
{
  "errors": [
      {
          "base": [
              "Não foi possível excluir essa série de notas pois ela está vinculada a um documento"
          ]
      }
  ],
  "error_details": [
      {
          "base": [
              { "error": "default" }
          ]
      }
  ]
}
