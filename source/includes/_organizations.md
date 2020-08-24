# Organizações

## Criação de Organizações

Para emissão de NF-e ou NFC-e, é necessário possuir ao menos uma organização criada no Emites. Para realizar a criação de uma organização via API, o processo consiste em dois passos:

### 1º Passo: Criação da Organização

Para criar uma organização, é necessário realizar uma requisição POST para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">POST</i>
        <h6>/api/v1/organizations</h6>
    </div>
</div>

Veja a seguir um exemplo do corpo da requisição:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/ \
  -H 'authorization: Bearer c3b1164e8ae17f6d9712730ec75be6da' \
  -H 'content-type: application/json' \
  -d '{
      "organization": {
        "address": {
            "address": "Rua do Rocio",
            "city": "Sao Paulo",
            "city_code": "812938",
            "complement": "Conj. 91",
            "district": "Vila Olimpia",
            "number": "199",
            "phone": "1133333333",
            "state": "SP",
            "zipcode": "04552000"
        },
        "codigo_regime_tributario": 1,
        "company_name": "The String",
        "document": "58521175000124",
        "email": "foo@bar.com",
        "inscricao_estadual": "787811920",
        "inscricao_municipal": "13213213",
        "name": "MyString"
      }
    }'


EXEMPLO DE RESPOSTA

{
  "organization": {
    "id": 5,
      "document": "58521175000124",
      "name": "Foo",
      "inscricao_municipal": "13213213",
      "inscricao_suframa": null,
      "company_name": "The String",
      "email": "foo@bar.com",
      "logo_file_name": null,
      "logo_url": "",
      "address": {
        "zipcode": "04552000",
        "address": "Rua do Rocio",
        "number": "199",
        "complement": "Conj. 91",
        "district": "Vila Olimpia",
        "city": "Sao Paulo",
        "state": "SP",
        "phone": "1133333333",
        "city_code": "812938"
      },
      "inscricao_estadual": "787811920",
      "codigo_regime_tributario": "simples_nacional",
      "cnae": null,
      "certificate": null
  }
}

EXEMPLO DE RETORNO DE ERROS

{
    "errors": { "document": ["não é válido"] },
    "error_details": [
        {
            "document": [
                { "error": "invalid" }
            ]
        }
    ]
}
```

    Campo                       |  Obrigatório  |     Tipo                |    Formato e tamanho         |   Observações
--------------------------------|---------------|-------------------------|------------------------------|-----------------------------------------------------------
    codigo_regime_tributario    |  Não          |     Numérico            |   1 dígito                   |  1 = Simples Nacional;<br>2 = Simples Nacional, excesso sublimite de receita bruta;<br>3 = Regime Normal.
    razao_social                |  Sim          |     Texto               |   Até 60 caracteres          |
    document                    |  Sim          |     Numérico            |   14 dígitos                 |  CNPJ da empresa emitente, somente números.
    email                       |  Sim          |     Texto               |   Até 60 caracteres          |
    inscricao_estadual          |  sim          |     Texto               |   Até 14 caracteres          |  Informar somente os algarismos, sem ponto, hífen, barra, etc. Na emissão de NF-e avulsa pode ser informado o texto ISENTO para os contribuintes do ICMS isentos de inscrição no cadastro de contribuintes do ICMS.
    inscricao_municipal         |  Não          |     Texto               |   Até 15 caracteres          |
    nome_fantasia               |  Não          |     Texto               |   Até 60 caracteres          |
    inscricao_suframa           |  Não          |     Texto               |   Até 60 caracteres          | Número de cadastro do SUFRAMA (Superintendência da Zona Franca de Manaus)

#### address

Grupo de informações relacionadas ao endereço da organização. Seus atributos são:

    Campo                       |  Obrigatório  |     Tipo                |    Formato e tamanho         |   Observações
--------------------------------|---------------|-------------------------|------------------------------|-----------------------------------------------------------
    address                     |  Sim          |  Texto                  |   Até 60 caracteres          |
    city                        |  Sim          |  Texto                  |   Até 60 caracteres          |
    city_code                   |  Sim          |  Numérico               |   7 dígitos                  |
    complement                  |  Não          |  Texto                  |   Até 60 caracteres          |
    district                    |  Sim          |  Texto                  |   Até 60 caracteres          |
    number                      |  Sim          |  Texto                  |   Até 60 caracteres          |
    phone                       |  Não          |  Numérico               |   De 6 a 14 carateres        |
    state                       |  Sim          |  Texto                  |   2 caracteres               |
    zipcode                     |  Sim          |  Numérico               |   8 dígitos                  |

### 2º Passo: Atualização/Upload do Certificado da Organização

A inclusão de certificado digital vigente da organização é obrigatório para a emissão da nota. Para criar ou atualizar um certificado, é necessário realizar uma requisição POST para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">POST</i>
        <h6>/api/v1/organizations/{:organization_id}/certificate</h6>
    </div>
</div>

<aside class="notice">
    <b>Atenção</b>: O parâmetro <b>:organization_id</b> também pode ser substituído pela notação <b>CNPJ{CNPJ da organização (somente números)}IE{ Inscrição Estadual da Organização (Somente Números OU ISENTO) }</b> em qualquer requisição.<br><br>
    Ex: <b>/api/v1/organizations/CNPJ58521175000124IE787811920</b>
</aside>

Veja a seguir um exemplo do corpo da requisição:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/8/certificate \
  -H 'authorization: Bearer c3b1164e8ae17f6d9712730ec75be6da' \
  -H 'content-type: application/json' \
  -d '{
        "password": "senhadocertificado",
        "file": "código em Base64 do arquivo PFX"
    }'


EXEMPLO DE RESPOSTA

{
  "certificate": {
    "pfx_certificate_file_name": "certificate.pfx",
      "password": "JKeDKzdvZWtLS2lxcmNBRTVQK2foob9mdFF6SW5uVllzVkNTTTB0Mjhmdz0tLWx6UXJFNUp4NWp2cG5mSWh4NmRDb3c9PQ-eao925ca6870661ed52c5b6577e6a56feb9f09d744",
      "expires_at": "2019-07-04",
      "pfx_certificate_url": "/system/certificates/pfx_certificates/000/000/019/original/certificate.pfx?1550754636"
  }
}
```

## Atualização de Organizações

Para atualizar uma organização, é necessário realizar uma requisição PATCH para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">PATCH</i>
        <h6>/api/v1/organizations/{:organization_id}</h6>
    </div>
</div>

Veja a seguir um exemplo do corpo da requisição:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X PATCH \
  https://app.production.emites.com.br/api/v1/organizations/5 \
  -H 'authorization: Bearer c3b1164e8ae17f6d9712730ec75be6da' \
  -H 'content-type: application/json' \
  -d '{
      "organization": {
        "company_name": "Update company_name",
        "email": "foo2@bar.com"
      }
    }'


EXEMPLO DE RESPOSTA

{
  "organization": {
    "id": 5,
      "document": "58521175000124",
      "name": "Foo",
      "inscricao_municipal": "13213213",
      "inscricao_suframa": null,
      "company_name": "Update company_name",
      "email": "foo2@bar.com",
      "logo_file_name": null,
      "logo_url": "",
      "address": {
        "zipcode": "04552000",
        "address": "Rua do Rocio",
        "number": "199",
        "complement": "Conj. 91",
        "district": "Vila Olimpia",
        "city": "Sao Paulo",
        "state": "SP",
        "phone": "1133333333",
        "city_code": "812938"
      },
      "inscricao_estadual": "787811920",
      "codigo_regime_tributario": "simples_nacional",
      "cnae": null,
      "certificate": null
  }
}

EXEMPLO DE RETORNO DE ERROS

{
    "errors": { "document": ["não é válido"] },
    "error_details": [
        {
            "document": [
                { "error": "invalid" }
            ]
        }
    ]
}
```

    Campo                       |  Obrigatório  |     Tipo                |    Formato e tamanho         |   Observações
--------------------------------|---------------|-------------------------|------------------------------|-----------------------------------------------------------
    codigo_regime_tributario    |  Não          |     Numérico            |   1 dígito                   |  1 = Simples Nacional;<br>2 = Simples Nacional, excesso sublimite de receita bruta;<br>3 = Regime Normal.
    razao_social                |  Sim          |     Texto               |   Até 60 caracteres          |
    document                    |  Sim          |     Numérico            |   14 dígitos                 |  CNPJ da empresa emitente, somente números.
    email                       |  Sim          |     Texto               |   Até 60 caracteres          |
    inscricao_estadual          |  sim          |     Texto               |   Até 14 caracteres          |  Informar somente os algarismos, sem ponto, hífen, barra, etc. Na emissão de NF-e avulsa pode ser informado o texto ISENTO para os contribuintes do ICMS isentos de inscrição no cadastro de contribuintes do ICMS.
    inscricao_municipal         |  Não          |     Texto               |   Até 15 caracteres          |
    nome_fantasia               |  Não          |     Texto               |   Até 60 caracteres          |
    inscricao_suframa           |  Não          |     Texto               |   Até 60 caracteres          | Número de cadastro do SUFRAMA (Superintendência da Zona Franca de Manaus)

#### address

Grupo de informações relacionadas ao endereço da organização. Seus atributos são:

    Campo                       |  Obrigatório  |     Tipo                |    Formato e tamanho         |   Observações
--------------------------------|---------------|-------------------------|------------------------------|-----------------------------------------------------------
    address                     |  Sim          |  Texto                  |   Até 60 caracteres          |
    city                        |  Sim          |  Texto                  |   Até 60 caracteres          |
    city_code                   |  Sim          |  Numérico               |   7 dígitos                  |
    complement                  |  Não          |  Texto                  |   Até 60 caracteres          |
    district                    |  Sim          |  Texto                  |   Até 60 caracteres          |
    number                      |  Sim          |  Texto                  |   Até 60 caracteres          |
    phone                       |  Não          |  Numérico               |   De 6 a 14 carateres        |
    state                       |  Sim          |  Texto                  |   2 caracteres               |
    zipcode                     |  Sim          |  Numérico               |   8 dígitos                  |


## Exclusão de Organizações

Para excluir uma organização da conta, é necessário realizar uma requisição DELETE para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-warning">DELETE</i>
        <h6>/api/v1/organizations/{:organization_id}</h6>
    </div>
</div>

Veja a seguir um exemplo do corpo da requisição:

```shell
EXEMPLO DE REQUISIÇÃO
curl -X DELETE \
  https://app.production.emites.com.br/api/v1/organizations/1 \
  -H 'authorization: Bearer c3b1164e8ae17f6d9712730ec75be6da' \
  -H 'content-type: application/json' \


EXEMPLO DE RETORNO DE ERROS

{
    "errors": ["A conta deve possuir ao menos uma organização"],
    "error_details": [
        {
            "base": [
                { "error": "last_organization" }
            ]
        }
    ]
}
```

## Listagem de Organizações

Para listar todas as organizações da conta, é necessário realizar uma requisição GET para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">GET</i>
        <h6>api/v1/organizations</h6>
    </div>
</div>

Veja a seguir um exemplo do corpo da requisição:

```shell
EXEMPLO DE REQUISIÇÃO
curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations \
  -H 'authorization: Bearer c3b1164e8ae17f6d9712730ec75be6da' \
  -H 'content-type: application/json' \
```

```shell
EXEMPLO DE RESPOSTA
{
    "organizations": [
        {
            "id": 1,
            "document": "12345678000000",
            "name": "Fulano de tal",
            "inscricao_municipal": "123456",
            "inscricao_suframa": null,
            "company_name": "F Comp",
            "email": "fulano.de.tal@nexaas.com",
            "logo_file_name": null,
            "logo_url": "",
            "address": {
                "address": "Rua 1",
                "city": "Rio de Janeiro",
                "city_code": "3301009",
                "complement": "-",
                "district": "Parque 2",
                "number": "119",
                "phone": "21999999999",
                "state": "RJ",
                "zipcode": "28000200"
            },
            "inscricao_estadual": "123456",
            "codigo_regime_tributario": "simples_nacional",
            "regime_tributario_diferenciado": "LFEM",
            "cnae": "14.02/951180002",
            "csc_id": "120",
            "csc_token": "Lorem Ipsum",
            "certificate_expires_at": null,
            "certificate": null
        }
    ]
}
```

## Consulta de Organizações

Para listar uma organização da conta, é necessário realizar uma requisição GET para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">GET</i>
        <h6>api/v1/organizations/{:organization_id}</h6>
    </div>
</div>

Veja a seguir um exemplo do corpo da requisição:

```shell
EXEMPLO DE REQUISIÇÃO
curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations \
  -H 'authorization: Bearer c3b1164e8ae17f6d9712730ec75be6da' \
  -H 'content-type: application/json' \
```

```shell
EXEMPLO DE RESPOSTA
{
    "organization": {
        "id": 1,
        "document": "12345678000000",
        "name": "Fulano de tal",
        "inscricao_municipal": "123456",
        "inscricao_suframa": null,
        "company_name": "F Comp",
        "email": "fulano.de.tal@nexaas.com",
        "logo_file_name": null,
        "logo_url": "",
        "address": {
            "address": "Rua 1",
            "city": "Rio de Janeiro",
            "city_code": "3301009",
            "complement": "-",
            "district": "Parque 2",
            "number": "119",
            "phone": "21999999999",
            "state": "RJ",
            "zipcode": "28000200"
        },
        "inscricao_estadual": "123456",
        "codigo_regime_tributario": "simples_nacional",
        "regime_tributario_diferenciado": "LFEM",
        "cnae": "14.02/951180002",
        "csc_id": "120",
        "csc_token": "Lorem Ipsum",
        "certificate_expires_at": null,
        "certificate": null
    }
}
```
