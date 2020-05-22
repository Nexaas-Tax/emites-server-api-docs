# Lista

## Lista de NF-e  

Para obter uma lista de NF-e é necessário realizar a seguinte requisição:  


<div class="api-endpoint">
  <div class="endpoint-data">
    <i class="label label-get">GET</i>
    <h6>/api/v1/organizations/{organization_id}/nfe</h6>
  </div>
</div>

### Filtro de NF-e  

É possível obter registros específicos usando alguns filtros.

    Nome                       |  Obrigatório  |     Localização         |    Descrição         
-------------------------------|---------------|-------------------------|------------------------------
    identifier                 |  não          |  query                  |   Número ou Chave de Acesso da NF-e. <br>Se o valor enviado possuir 44 dígitos será utilizado o atributo **chave de acesso** para a busca, caso contrário será utilizado o atributo **número**          |
    status                     |  não          |  query                  |   Situação da NF-e na API.<br>Valores válidos: **proccessing, succeeded, denegated, rejected, cancelled, error, cancel_rejected, corrected, correction_rejected, not_sent**.<br> **Deixe em branco ou não envie o parâmetro para listar todas as situações**          |
    sort_type                  |  não          |  query                  |   Atributo utilizado para ordenar os resultados. <br> Valores válidos: **created_at** e **updated_at**<br>Valor padrão: **created_at**         |
    sort_direction             |  não          |  query                  |   Sentido que os resultados serão listados.<br> Valores válidos: **desc** e **asc**<br>Valor padrão: **desc**                |  
    starting_at                |  não          |  query                  |   Data inicial (utiliza data de emissão da NF-e).<br>Formato: **DD/MM/AAAA**          |  
    ending_at                  |  não          |  query                  |   Data final (utiliza data de emissão da NF-e).<br>Formato: **DD/MM/AAAA**          |
    page                       |  não          |  query                  |   Indica o número da página de registros que será retornada.<br>Valor padrão: **1**          |  
    per_page                   |  não          |  query                  |   Indica a quantidade de registros a serem retornados.<br>Valor padrão: **10**       |
    remote_id                  |  não          |  query                  |   Identificador de requisição. A responsabilidade de gerar e controlar esse identificador é exclusiva do cliente.  |

```shell
EXEMPLO DE REQUISIÇÃO

# Sem o uso dos filtros
curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/11/nfe \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'

# Utilizando os parâmetros para filtrar resultados
curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/11/nfe?identifier=123&starting_at=01/01/2019&status=succeeded \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'


EXEMPLO DE RESPOSTA:

{
  "nfe": [
    {
      "id": 10990,
        "status": "succeeded",
        "data": {...},
        "danfe_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfe/pdf_files/000/015/761/original/danfe.pdf?153719",
        "xml_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfe/xml_files/000/015/761/original/nfce.xml?15379",
        "taxrules_calculation_log": null
    }
  ]
}
```

## Lista de NFC-e  

Para obter uma lista de NFC-e é necessário realizar a seguinte requisição:  


<div class="api-endpoint">
  <div class="endpoint-data">
    <i class="label label-get">GET</i>
    <h6>/api/v1/organizations/{organization_id}/nfce</h6>
  </div>
</div>

### Filtro de NFC-e  

É possível obter registros específicos usando alguns filtros.

    Nome                       |  Obrigatório  |     Localização         |    Descrição         
-------------------------------|---------------|-------------------------|------------------------------
    identifier                 |  não          |  query                  |   Número ou Chave de Acesso da NFC-e. <br>Se o valor enviado possuir 44 dígitos será utilizado o atributo **chave de acesso** para a busca, caso contrário será utilizado o atributo **número**          |
    status                     |  não          |  query                  |   Situação da NFC-e na API.<br>Valores válidos: **proccessing, succeeded, denegated, rejected, cancelled, error, cancel_rejected, corrected, correction_rejected, not_sent**.<br> **Deixe em branco ou não envie o parâmetro para listar todas as situações**          |
    sort_type                  |  não          |  query                  |   Atributo utilizado para ordenar os resultados. <br> Valores válidos: **created_at** e **updated_at**<br>Valor padrão: **created_at**         |
    sort_direction             |  não          |  query                  |   Sentido que os resultados serão listados.<br> Valores válidos: **desc** e **asc**<br>Valor padrão: **desc**                |  
    starting_at                |  não          |  query                  |   Data inicial (utiliza data de emissão da NFC-e).<br>Formato: **DD/MM/AAAA**          |  
    ending_at                  |  não          |  query                  |   Data final (utiliza data de emissão da NFC-e).<br>Formato: **DD/MM/AAAA**          |
    page                       |  não          |  query                  |   Indica o número da página de registros que será retornada.<br>Valor padrão: **1**          |  
    per_page                   |  não          |  query                  |   Indica a quantidade de registros a serem retornados.<br>Valor padrão: **10**       |
    remote_id                  |  não          |  query                  |   Identificador de requisição. A responsabilidade de gerar e controlar esse identificador é exclusiva do cliente.  |

```shell
EXEMPLO DE REQUISIÇÃO

# Sem o uso dos filtros
curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/11/nfce \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'

# Utilizando os parâmetros para filtrar resultados
curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/11/nfce?identifier=123&starting_at=01/01/2019&status=succeeded \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'

EXEMPLO DE RESPOSTA:

{
  "nfce": [
    {
      "id": 10990,
        "status": "succeeded",
        "data": {...},
        "danfe_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfce/pdf_files/000/015/761/original/danfe.pdf?153719",
        "xml_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfce/xml_files/000/015/761/original/nfce.xml?15379",
        "taxrules_calculation_log": null
    }
  ]
}
```
