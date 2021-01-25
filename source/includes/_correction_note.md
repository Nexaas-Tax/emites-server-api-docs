# Carta de Correção

## Carta de Correção de NF-e

A carta de correção de nota fiscal eletrônica (CC-e) é um documento fiscal com o objetivo de corrigir informações da nota fiscal eletrônica (NF-e).
Se você emitir uma NF-e com um erro, pode corrigi-lá com uma CC-e, mas nem todos os erros são passíveis de correção, é preciso seguir algumas regras.

Ela é utilizada para a regularização de algum erro ocorrido na emissão, desde que não seja:

* o valor do imposto (base de cálculo, alíquota, diferença de preço, quantidade, valor de operação ou prestação),
* os dados cadastrais (mudanças do remetente ou destinatário)
* data de emissão ou de saída da mercadoria.

Regras:

* Permitido em até 30 dias, após a emissão da nota.
* Pode ter até 20 cartas em uma nota

O que pode ser corrigido?

* A natureza de operação (CFOP): sob a condição de não mudar a natureza dos impostos;
* Os códigos ficais: desde que não altere os valores fiscais;
* Data de emissão ou de saída: contanto que não altere o período de apuração do ICMS;
* Peso, volume etc.;
* Endereço do destinatário;
* Razão social do destinatário: se não alterar por completo;
* Dados adicionais.

Não há um padrão de texto, mas o emissor tem a obrigação de descrever de forma clara e objetiva a correção que deve ser considerada.

**Obs.: Após o processamento da solicitação da carta de correção da NF, o XML do evento estará disponível via consulta da NF, no último item do node "corrections".**

Para requisitar uma correção, envie a seguinte requisição:


<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">PATCH</i>
        <h6>/api/v1/organizations/{organization_id}/nfe/{nfe_id}/correction </h6>
    </div>
</div>

```shell
EXEMPLO DE REQUISIÇÃO

curl -X PATCH \
  https://app.production.emites.com.br/api/v1/organizations/11/nfe/10990/correction \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -H 'content-type: application/json' \
    -d '{
          "correcao": "Carta correcao teste",
          "remote_id": "abc123"
        }'

# Usando a chave de acesso
curl -X PATCH \
  https://app.emites.com.br/api/v1/organizations/11/nfe/35181160619202003910551010000000321613631381/correction \
    -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
    -H 'content-type: application/json' \
    -d '{
          "correcao": "Carta correcao teste"
        }'

EXEMPLO DE RESPOSTA

{
  "nfe": {
    "id": 10990,
    "request_id": "34bc244b-cd15-4dcb-884e-b513896e995c",
    "remote_id": "abc123",
    "status": "corrected",
    "data": {...},
    "danfe_url": "/system/nfe/pdf_files/000/010/953/original/danfe.pdf?1539874106",
    "xml_url": "/system/nfe/xml_files/000/010/953/original/nfe.xml?1539874106",
    "corrections": [
      {
        "id": 34,
        "data": {
          "numero_evento": 3,
          "correcao": "Carta correcao teste",
          "resposta_correcao": {
            "numero_protocolo": "135180016104757",
            "chave_acesso": "35181160619202003910551010000000321613631381"
          }
        },
        "status": "authorized",
        "xml_url": "/system/corrections/files/000/000/024/original/correction_nfe.xml?1543402657"
      },
      {
        "id": 33,
        "data": {
          "numero_evento": 2,
          "correcao": "Corrige o nome o nome do fornecedor",
          "resposta_correcao": {
            "numero_protocolo": "135180016098939",
            "chave_acesso": "35181160619202003910551010000000321613631381"
          }
        },
        "status": "authorized",
        "xml_url": "/system/corrections/files/000/000/003/original/correction_nfe.xml?1543345161"
      },
      {
        "id": 32,
        "data": {
          "numero_evento": 1,
          "correcao": "Altera-se a descrição do produto para NITROGENIO 50L 10M3",
          "resposta_correcao": {
            "numero_protocolo": "135180016098422",
            "chave_acesso": "35181160619202003910551010000000321613631381"
          }
        },
        "status": "authorized",
        "xml_url": "/system/corrections/files/000/000/001/original/correction_nfe.xml?1543343189"
      }
    ]
  }
}
```

## Carta de Correção de NFC-e

A carta de correção eletrônica é utilizada, exclusivamente, para correções de NF-e, modelo 55.
