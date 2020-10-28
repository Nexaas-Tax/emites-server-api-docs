# Inutilização

## Inutilização de NF-e

Para inutilizar um número de NF-e, envie a seguinte requisição:  

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">POST</i>
        <h6>/api/v1/organizations/{organization_id}/nfe/disable</h6>
    </div>
</div>

Regras de Validação:

* O campo "serie" é obrigatório;
* O motivo é opcional e deve possuir entre 15 e 255 caracteres;
* Não é permitido inutilizar numeros de notas emitidas, canceladas, corrigidas ou denegadas;
* Em caso de inutilização de apenas um número, os campos "numero_inicial" e "numero_final" devem ser ignorados;
* Em caso de inutilização de um intervalo, o campo "numero" deve ser ignorado;
* Em caso de inutilização de um intervalo, o "numero_final" deve ser maior que o "numero_inicial";

<aside class="notice">
    Atenção: somente podem ser inutilizados números de notas fiscais que não tenham sido utilizadas em NF-e emitidas, canceladas ou denegadas. A inutilização tem o objetivo de comunicar a quebra na sequência numérica de NF-e e esta quebra não deve ser fruto de fraude ou dolo intencional.
</aside>

```shell
EXEMPLO DE REQUISIÇÃO

# Inutilização de apenas um número com motivo padrão: "Erro na emissão da nota fiscal"
curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/nfe/disable \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -H 'content-type: application/json' \
    -d '{
          "serie": "1",
          "numero": "9999999999"
        }'

# Inutilização de apenas um número com motivo personalizado
curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/nfe/disable \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -H 'content-type: application/json' \
    -d '{
          "serie": "1",
          "numero": "9999999999",
          "motivo": "Quebra na sequencia de numeracao"
        }'

# Inutilização de um intervalo de numeros com motivo padrão: "Erro na emissão da nota fiscal"
curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/nfe/disable \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -H 'content-type: application/json' \
    -d '{
          "serie": "1",
          "numero_inicial": "1500",
          "numero_final": "1550"
        }'

# Inutilização de um intervalo de numeros com motivo personalizado
curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/nfe/disable \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -H 'content-type: application/json' \
    -d '{
          "serie": "1",
          "numero_inicial": "1500",
          "numero_final": "1550",
          "motivo": "Quebra na sequencia de numeracao"
        }'

EXEMPLO DE RESPOSTA

# Inutilização de apenas um número
{
  "nfe_disablement": {
    "id": 16,
    "status": "processing",
    "data": {
      "uf": "35",
      "cnpj_emitente": "58521175000124",
      "serie": "1",
      "motivo": "Erro na emissão da nota fiscal",
      "numero_inicial": 9999999999,
      "numero_final": 9999999999
    }
  }
}

# Inutilização de um intervalo de numeros
{
  "nfe_disablement": {
    "id": 16,
    "status": "processing",
    "data": {
      "uf": "35",
      "cnpj_emitente": "58521175000124",
      "serie": "1",
      "motivo": "Erro na emissão da nota fiscal",
      "numero_inicial": 1500,
      "numero_final": 1550
    }
  }
}
```

## Consulta de inutilização de NF-e  

Para consultar uma inutilização de  NF-e é necessário realizar a seguinte requisição:  


<div class="api-endpoint">
  <div class="endpoint-data">
    <i class="label label-get">GET</i>
    <h6>/api/v1/organizations/{:organization_id}/nfe/disable/{:nfe_disablement_id}</h6>
  </div>
</div>


```shell
EXEMPLO DE REQUISIÇÃO

curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/11/nfe/disable/16 \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'


EXEMPLO DE RESPOSTA:

# Solicitação rejeitada pela SEFAZ

{
  "nfe_disablement": {
    "id": 16,
      "status": "rejected",
      "data": {
        "uf": "35",
        "cnpj_emitente": "58521175000124",
        "serie": 1,
        "motivo": "Erro na emissão da nota fiscal",
        "numero_inicial": 1500,
        "numero_final": 1550,
        "resposta_inutilizacao": {
          "erros": [
            "241 - Rejeicao: Um numero da faixa ja foi utilizado"
          ]
        }
      }
  }
}

# Solicitação autorizada pela SEFAZ

{
  "nfe_disablement": {
    "id": 17,
      "status": "authorized",
      "data": {
        "uf": "35",
        "cnpj_emitente": "58521175000124",
        "serie": 1,
        "motivo": "Erro na emissão da nota fiscal",
        "numero_inicial": 1500,
        "numero_final": 1550,
        "resposta_inutilizacao": {
          "numero_protocolo": "135190000301748"
        }
      }
  }
}
```

## Inutilização de NFC-e

Para inutilizar um número de NFC-e, envie a seguinte requisição:  

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">POST</i>
        <h6>/api/v1/organizations/{organization_id}/nfce/disable</h6>
    </div>
</div>

Regras de Validação:

* O campo "serie" é obrigatório;
* O motivo é opcional e deve possuir entre 15 e 255 caracteres;
* Não é permitido inutilizar numeros de notas emitidas, canceladas, corrigidas ou denegadas;
* Em caso de inutilização de apenas um número, os campos "numero_inicial" e "numero_final" devem ser ignorados;
* Em caso de inutilização de um intervalo, o campo "numero" deve ser ignorado;
* Em caso de inutilização de um intervalo, o "numero_final" deve ser maior que o "numero_inicial";

<aside class="notice">
    Atenção: somente podem ser inutilizados números de notas fiscais que não tenham sido utilizadas em NF-e emitidas, canceladas ou denegadas. A inutilização tem o objetivo de comunicar a quebra na sequência numérica de NF-e e esta quebra não deve ser fruto de fraude ou dolo intencional.
</aside>

```shell
EXEMPLO DE REQUISIÇÃO

# Inutilização de apenas um número com motivo padrão: "Erro na emissão da nota fiscal"
curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/nfce/disable \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -H 'content-type: application/json' \
    -d '{
          "serie": "1",
          "numero": "9999999999"
        }'

# Inutilização de apenas um número com motivo personalizado
curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/nfce/disable \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -H 'content-type: application/json' \
    -d '{
          "serie": "1",
          "numero": "9999999999",
          "motivo": "Quebra na sequencia de numeracao"
        }'

# Inutilização de um intervalo de numeros com motivo padrão: "Erro na emissão da nota fiscal"
curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/nfce/disable \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -H 'content-type: application/json' \
    -d '{
          "serie": "1",
          "numero_inicial": "1500",
          "numero_final": "1550"
        }'

# Inutilização de um intervalo de numeros com motivo personalizado
curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/nfce/disable \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -H 'content-type: application/json' \
    -d '{
          "serie": "1",
          "numero_inicial": "1500",
          "numero_final": "1550",
          "motivo": "Quebra na sequencia de numeracao"
        }'

EXEMPLO DE RESPOSTA

# Inutilização de apenas um número
{
  "nfce_disablement": {
    "id": 16,
    "status": "processing",
    "data": {
      "uf": "35",
      "cnpj_emitente": "58521175000124",
      "serie": "1",
      "motivo": "Erro na emissão da nota fiscal",
      "numero_inicial": 9999999999,
      "numero_final": 9999999999
    }
  }
}

# Inutilização de um intervalo de numeros
{
  "nfce_disablement": {
    "id": 16,
    "status": "processing",
    "data": {
      "uf": "35",
      "cnpj_emitente": "58521175000124",
      "serie": "1",
      "motivo": "Erro na emissão da nota fiscal",
      "numero_inicial": 1500,
      "numero_final": 1550
    }
  }
}
```

## Consulta de inutilização de NFC-e  

Para consultar uma inutilização de  NFC-e é necessário realizar a seguinte requisição:  


<div class="api-endpoint">
  <div class="endpoint-data">
    <i class="label label-get">GET</i>
    <h6>/api/v1/organizations/{organization_id}/nfce/disable/{nfce_disablement_id}</h6>
  </div>
</div>


```shell
EXEMPLO DE REQUISIÇÃO

curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/11/nfce/disable/16 \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'


EXEMPLO DE RESPOSTA:

# Solicitação rejeitada pela SEFAZ

{
  "nfce_disablement": {
    "id": 16,
      "status": "rejected",
      "data": {
        "uf": "35",
        "cnpj_emitente": "58521175000124",
        "serie": 1,
        "motivo": "Erro na emissão da nota fiscal",
        "numero_inicial": 1500,
        "numero_final": 1550,
        "resposta_inutilizacao": {
          "erros": [
            "241 - Rejeicao: Um numero da faixa ja foi utilizado"
          ]
        }
      }
  }
}

# Solicitação autorizada pela SEFAZ

{
  "nfce_disablement": {
    "id": 17,
      "status": "authorized",
      "data": {
        "uf": "35",
        "cnpj_emitente": "58521175000124",
        "serie": 1,
        "motivo": "Erro na emissão da nota fiscal",
        "numero_inicial": 1500,
        "numero_final": 1550,
        "resposta_inutilizacao": {
          "numero_protocolo": "135190000301748"
        }
      }
  }
}
```
