# Cancelamento

## Cancelamento de NF-e

Para cancelar uma NF-e, envie a seguinte requisição:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">PATCH </i>
        <h6>/api/v1/organizations/{organization_id}/nfe/{nfe_id}/cancel </h6>
    </div>
</div>

<aside class="notice">
    Atenção: somente poderá ser cancelada uma NF-e cujo uso tenha sido previamente autorizado pelo Fisco (protocolo "Autorização de Uso") e desde que não tenha ainda ocorrido a saída da mercadoria do estabelecimento. Atualmente o prazo máximo para cancelamento de uma NF-e é de 24 horas após a emissão. O cancelamento não pode ser desfeito.<br><br>
    <b>O motivo (opcional) deve possuir entre 15 e 255 caracteres.</b>
</aside>

```shell
EXEMPLO DE REQUISIÇÃO

# Motivo padrão: "Cancelamento NF-e"
curl -X PATCH \
    https://app.production.emites.com.br/api/v1/organizations/11/nfe/10990/cancel \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -H 'content-type: application/json' \

# Motivo personalizado
curl -X PATCH \
    https://app.production.emites.com.br/api/v1/organizations/11/nfe/10990/cancel \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -d '{
          "motivo": "Desistência do cliente"
        }'

# Enviando Remote ID
curl -X PATCH \
    https://app.production.emites.com.br/api/v1/organizations/11/nfe/10990/cancel \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -d '{
          "motivo": "Desistência do cliente",
          "remote_id": "abc123"
        }'

# Usando a chave de acesso
curl -X PATCH \
    https://app.emites.com.br/api/v1/organizations/11/nfe/53190222769530000131556110000002041100341123/cancel \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \

EXEMPLO DE RESPOSTA

{
  "nfe": {
    "id": 1,
    "status": "processing",
    "request_id": "6e2e172d-038e-4172-8dfd-434b632b1c8d",
    "remote_id": "abc123"
  }
}
```

Após o processamento da solicitação de cancelamento da NF-e, o XML do evento estará disponível via consulta da NF-e no campo "cancel_xml_url". Exemplo:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">GET</i>
        <h6>/api/v1/organizations/{organization_id}/nfe/{nfe_id}  </h6>
    </div>
</div>

```
{
  "nfe": {
    "access_key": "53190222769530000131556110000002041100341123",
    "id": 10990,
    "request_id": "6e2e172d-038e-4172-8dfd-434b632b1c8d",
    "remote_id": "abc123",
    "organization_id": 1,
    "status": "cancelled",
    "data": {
      ...
      "resposta_cancelamento": {
        "numero_protocolo": "353190000049440",
        "chave_acesso": "53190222769530000131556110000002041100341123"
      },
      "data_cancelamento": "2019-02-22T14:53:25.521-03:00",
      "motivo": "Desistência do cliente"
    },
    "danfe_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfe/pdf_files/000/015/761/original/danfe.pdf?153719",
    "xml_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfe/xml_files/000/015/761/original/nfe.xml?15379",
    "cancel_xml_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfe/cancel_xml_files/000/010/598/original/cancel_nfe.xml?15781",
    "taxrules_calculation_log": null
  }
}
```

## Cancelamento de NFC-e

Para cancelar uma NFC-e, envie a seguinte requisição:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">PATCH </i>
        <h6>/api/v1/organizations/{organization_id}/nfce/{nfce_id}/cancel </h6>
    </div>
</div>

<aside class="notice">
    Atenção: somente poderá ser cancelada uma NFC-e cujo uso tenha sido previamente autorizado pelo Fisco (protocolo "Autorização de Uso") e desde que não tenha ainda ocorrido a saída da mercadoria do estabelecimento. Atualmente o prazo máximo para cancelamento de uma NFC-e é de 24 horas após a emissão. O cancelamento não pode ser desfeito.<br><br>
    <b>O motivo (opcional) deve possuir entre 15 e 255 caracteres.</b>
</aside>

```shell
EXEMPLO DE REQUISIÇÃO

# Motivo padrão: "Cancelamento NFC-e"
curl -X PATCH \
    https://app.production.emites.com.br/api/v1/organizations/11/nfce/10990/cancel \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -H 'content-type: application/json' \

# Motivo personalizado
curl -X PATCH \
    https://app.production.emites.com.br/api/v1/organizations/11/nfce/10990/cancel \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -d '{
          "motivo": "Desistência do cliente"
        }'

# Enviando Remote ID
curl -X PATCH \
    https://app.production.emites.com.br/api/v1/organizations/11/nfe/10990/cancel \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -d '{
          "motivo": "Desistência do cliente",
          "remote_id": "123abc"
        }'

# Usando a chave de acesso
curl -X PATCH \
    https://app.emites.com.br/api/v1/organizations/11/nfce/53190222769530000131657170000000551642238289/cancel \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \


EXEMPLO DE RESPOSTA

{
  "nfce": {
    "id": 1,
    "status": "processing",
    "request_id": "54a291e4-ddbb-4076-a784-6d1f89c17049",
    "remote_id": "123abc"
  }
}
```

Após o processamento da solicitação de cancelamento da NFC-e, o XML do evento estará disponível via consulta da NFC-e no campo "cancel_xml_url". Exemplo:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">GET</i>
        <h6>/api/v1/organizations/{organization_id}/nfce/{nfce_id}  </h6>
    </div>
</div>

```
{
  "nfce": {
    "access_key": "53190222769530000131556110000002041100341123",
    "id": 5,
    "request_id": "6e2e172d-038e-4172-8dfd-434b632b1c8d",
    "remote_id": "123abc",
    "organization_id": 1,
    "status": "cancelled",
    "data": {
      ...
      "resposta_cancelamento": {
        "numero_protocolo": "353190000027203",
        "chave_acesso": "53190222769530000131657170000000551642238289"
      },
      "data_cancelamento": "2019-02-22T15:04:19.311-03:00",
      "motivo": "Desistência do cliente"
    },
    "danfe_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfce/pdf_files/000/015/761/original/danfe.pdf?153719",
    "xml_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfce/xml_files/000/015/761/original/nfce.xml?15379",
    "cancel_xml_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfce/cancel_xml_files/000/010/598/original/cancel_nfce.xml?15781",
    "taxrules_calculation_log": null
  }
}
```

## Cancelamento por Substituição de NFC-e

Para cancelar por substituição uma NFC-e, envie a seguinte requisição:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">PATCH </i>
        <h6>/api/v1/organizations/{organization_id}/nfce/{nfce_id}/replacement_cancel </h6>
    </div>
</div>

<aside class="notice">
    Atenção: Um documento fiscal eletrônico só pode ser cancelado se (i) tiver sido previamente autorizado pelo Fisco e (ii) desde que ainda não tenha ocorrido a saída da mercadoria do estabelecimento. O cancelamento pode ser do tipo "normal" (NF-e, CF-e e NF-e) ou por "substituição" (NFC-e). Atualmente, o prazo máximo para cancelamento do tipo "normal" é de 30 minutos (NFC-e, CF-e) e de 24 horas (NF-e) e o prazo máximo para cancelamento do tipo "substituição" é de 168 horas (NFC-e). O cancelamento, quando realizado, não pode ser desfeito.<br><br>
    <b>O motivo (opcional) deve possuir entre 15 e 255 caracteres.</b></br><br>
    O campo <b>ch_nfe_ref</b> é obrigatório, preencha com a chave de acesso a
    ser substituida
</aside>

```shell
EXEMPLO DE REQUISIÇÃO

# Motivo padrão: "Cancelamento por substituição devido duplicidade de emissão para a mesma operação fiscal"
curl -X PATCH \
    https://app.production.emites.com.br/api/v1/organizations/11/nfe/53190222769530000131556110000002041100341123/replacement_cancel \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -H 'content-type: application/json' \
    -d '{
          "ch_nfe_ref": "35191135402759007600551130000205421006450377"
        }'

# Motivo personalizado
curl -X PATCH \
    https://app.production.emites.com.br/api/v1/organizations/53190222769530000131556110000002041100341123/nfe/10990/replacement_cancel \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -d '{
          "motivo": "Cancelamento por substituição",
          "ch_nfe_ref": "35191135402759007600551130000205421006450377"
        }'

EXEMPLO DE RESPOSTA

{
  "nfe": {
    "id": 10990,
    "status": "processing",
    "data": {...},
    "danfe_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfe/pdf_files/000/015/761/original/danfe.pdf?153719",
    "xml_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfe/xml_files/000/015/761/original/nfe.xml?15379",
    "taxrules_calculation_log": null
  }
}
```
