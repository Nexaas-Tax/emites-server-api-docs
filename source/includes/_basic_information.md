# Informações básicas

## Autenticação

Todo acesso à API é feito do ponto de vista de uma conta existente no Emites. Assim sendo, toda requisição à API deverá ser autenticada. A autenticação é feita via token, que deve ser informado no header de cada requisição efetuada.

Para todas as requisições são necessários os seguintes Headers:

<div class="api-endpoint">
  <div class="endpoint-data authentication">
    "Authorization": "Bearer 6f42433270bc61d746556b17605db1s4",<br>
    "Content-Type": "application/json"
  </div>
</div>  

  ```shell
  Formato JSON

  EXEMPLO DE REQUISIÇÃO

    curl -X GET \
      https://app.production.emites.com.br/api/v1/organizations \
      -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
      -H 'content-type: application/json' 

  EXEMPLO DE RESPOSTA

  {
    "chave": "valor"
  }

  ```

