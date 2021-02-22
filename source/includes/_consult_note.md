# Consulta

### Para consultar uma NF-e é necessário realizar a seguinte requisição:

<div class="api-endpoint">
  <div class="endpoint-data">
    <i class="label label-get">GET</i>
    <h6>/api/v1/organizations/{organization_id}/nfe/{id}  </h6>
  </div>
</div>

Obs: O "id" pode ser preenchido com o nfe_id, chave de acesso da nota, request_id ou remote_id.

### E para consultar uma NFC-e, a seguinte:

<div class="api-endpoint">
  <div class="endpoint-data">
    <i class="label label-get">GET</i>
    <h6>/api/v1/organizations/{organization_id}/nfce/{id}  </h6>
  </div>
</div>

Obs: O "id" pode ser preenchido com o nfce_id, chave de acesso, request_id ou remote_id.

### Para consultar o Valor Total por código de operação (CFOP) em um determinado período fixo:

<div class="api-endpoint">
  <div class="endpoint-data">
    <i class="label label-get">GET</i>
    <h6>/api/v1/organizations/{organization_id}/document_totals</h6>
  </div>
</div>

```shell
{
  "cfop": "5000",
  "date": "20/08/2019",
  "date_type": "day"
}
```

## Consulta NF-e Emitida

Segue abaixo um exemplo de requisição de emissão em lote com sucesso que será utilizado para posterior consulta:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/nfe_batch \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json' \
  -d '{
        "nfe_batch": {
          "lote": 1,
          "sincronicidade": 0,
          "serie": 611,
          "uf": 53,
          "remote_id": "abc123",
          "nfes": [
            {
              "dados_gerais": {
                "uf": 53,
                "codigo_mun_ocorrencia": "5300108",
                "natureza_operacao": "saida",
                "tipo_operacao": 1,
                "indicador_consumidor_final": 0,
                "indicador_presenca": 0,
                "forma_contingencia": "",
                "finalidade_nfe": 1,
                "destino_operacao": "1"
              },
              "cliente": {
                "cpf_cnpj": "68763591669",
                "nome": "NF-E EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                "pessoa_fisica_juridica": "person",
                "telefone": "21988766743",
                "inscricao_estadual": "0736913700156",
                "inscricao_municipal": "",
                "inscricao_suframa": "",
                "indicador_inscricao_estadual": 1,
                "email": "teste@teste.com",
                "endereco": {
                  "logradouro": "Rua do Consultor",
                  "complemento": "BL A",
                  "numero": "14",
                  "bairro": "Bairro teste",
                  "codigo_municipio": "5300108",
                  "nome_municipio": "Brasilia",
                  "codigo_pais": "1058",
                  "nome_pais": "Brasil",
                  "uf": "DF",
                  "cep": "05685040"
                }
              },
              "produtos": [
                {
                  "codigo_produto": 14589,
                  "codigo_ean": 7891125063000,
                  "descricao": "VODKA NATASHA 1L UN 1X1000ML",
                  "cfop": 5403,
                  "valor_unitario_comercial": 10.38,
                  "valor_unitario_tributario": 10.38,
                  "valor_total_produto": "62.28",
                  "valor_desconto": 10.90,
                  "quantidade_comercial": 6,
                  "quantidade_tributaria": 6,
                  "unidade_comercial": "UN",
                  "unidade_tributaria": "UN",
                  "num_pedido": 5100003910,
                  "num_item_pedido": 1,
                  "ean_unidade_trib": 7891125063000,
                  "extipi": 22,
                  "ncm": 22086000,
                  "cest": 1300402,
                  "producao_escala": "s",
                  "valor_frete": 10,
                  "valor_seguro": 11.50,
                  "outras_despesas": 20,
                  "tributacao": {
                    "valor_aproximado_total": 50.21,
                    "icms": {
                      "situacao_tributaria": "10",
                      "modalidade_base_calculo": 3,
                      "codigo_origem_produto": 0,
                      "valor_base_calculo": 62.32,
                      "aliquota_icms": 29,
                      "valor_icms": 18.07,
                      "modalidade_base_calculo_st": 4,
                      "valor_base_calculo_st": 80.41,
                      "perc_mva_icms_st": 29.0400,
                      "aliquota_icms_st": 31,
                      "valor_icms_st": 6.86,
                      "valor_fcp_interestadual": 19.61
                    },
                    "ipi": {
                      "situacao_tributaria": "99",
                      "codigo_enquadramento": 999,
                      "valor_ipi": 14.4
                    },
                    "pis": {
                      "situacao_tributaria": "01",
                      "valor_base_calculo": 62.32,
                      "aliquota_pis": 1.65,
                      "valor_pis": 1.03
                    },
                    "cofins": {
                      "situacao_tributaria": "01",
                      "valor_base_calculo": "129.62",
                      "aliquota_cofins": "7.60",
                      "valor_cofins": "9.85"
                    }
                  }
                }
              ],
              "forma_de_pagamento": [
                {
                  "tipo_de_pagamento": "01",
                  "valor_do_pagamento": 114.14
                }
              ],
              "transporte": {
                "valor_total_frete": 0,
                "codigo_modalidade": 9,
                "codigo_transportadora": 1,
                "transportadora": {
                  "cnpj_cpf": 81043396000156,
                  "razao_social": "teste",
                  "inscricao_estadual": "",
                  "insencao_icms": "",
                  "endereco_completo": "rua teste, 111",
                  "municipio": "Brasilia",
                  "uf": "DF"
                },
                "volume_transportado": [
                  {
                    "quantidade_volumes": 5,
                    "numeracao_volumes": 333,
                    "marca": "teste",
                    "especie": "pacote",
                    "peso_liquido": "3000",
                    "peso_bruto": "4050"
                  }
                ]
              }
            }
          ]
        }
      }'


EXEMPLO DE RESPOSTA

{
  "nfe_batch": {
    "id": 1,
    "key": null,
    "request_id": "7d391761-1681-4e9c-ac6e-d47389f211f0",
    "remote_id": "abc123",
    "nfes": [
      {
        "access_key": null,
        "id": 350,
        "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
        "remote_id": null,
        "organization_id": 1,
        "status": "processing"
      }
    ]
  }
}
```

A resposta conterá os mesmos campos que foram enviados na requisição, e adicionalmente campos exclusivos específicos sobre o status da NF-e:

Para consultar a NF-e criada, é necessário realizar a seguinte requisição utilizando o identificador da NF-e contido na resposta:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/11/nfe/350 \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'


EXEMPLO DE RESPOSTA:

{
  "nfe": {
    "access_key": "53190222769530000131556110000002001616311935",
    "id": 350,
    "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
    "remote_id": "abc123",
    "organization_id": 1,
    "status": "succeeded",
    "data": {
      ...
      "resposta_emissao": {
        "data_emissao": "2019-02-21T16:30:12.000-03:00",
        "codigo_verificacao": "d0X2SUrxM6IDrmJnIA36/D5LKrE=",
        "numero_protocolo": "3531900003011886",
        "chave_acesso": "53190222769530000131556110000002001616311935"
      }
    },
    "danfe_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfe/pdf_files/000/015/350/original/danfe.pdf?153719",
    "xml_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfe/xml_files/000/015/350/original/nfe.xml?15379",
    "taxrules_calculation_log": null
  }
}

EXEMPLO DE REQUISIÇÃO USANDO A CHAVE DE ACESSO

curl -X GET \
  https://app.emites.com.br/api/v1/organizations/11/nfe/53190222769530000131556110000002001616311935 \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'


EXEMPLO DE RESPOSTA:

{
  "nfe": {
    "access_key": "53190222769530000131556110000002001616311935",
    "id": 350,
    "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
    "remote_id": "abc123",
    "organization_id": 1,
    "status": "succeeded",
    "data": {
      ...
      "resposta_emissao": {
        "data_emissao": "2019-02-21T16:30:12.000-03:00",
        "codigo_verificacao": "d0X2SUrxM6IDrmJnIA36/D5LKrE=",
        "numero_protocolo": "3531900003011886",
        "chave_acesso": "53190222769530000131556110000002001616311935"
      }
    },
    "danfe_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfe/pdf_files/000/015/350/original/danfe.pdf?153719",
    "xml_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfe/xml_files/000/015/350/original/nfe.xml?15379",
    "taxrules_calculation_log": null
  }
}
```

## Consulta NF-e Rejeitada (SEFAZ)

Segue abaixo um exemplo de requisição de emissão em lote com rejeição da SEFAZ que será utilizado para posterior consulta:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/nfe_batch \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json' \
  -d '{
        "nfe_batch": {
          "lote": 1,
          "sincronicidade": 0,
          "serie": 611,
          "uf": 53,
          "nfes": [
            {
              "dados_gerais": {
                "uf": 53,
                "codigo_mun_ocorrencia": "5300108",
                "natureza_operacao": "saida",
                "tipo_operacao": 0, # Alterado para NF-e de Entrada
                "indicador_consumidor_final": 0,
                "indicador_presenca": 0,
                "finalidade_nfe": 1,
                "destino_operacao": "1"
              },
              "cliente": {
                "cpf_cnpj": "68763591669",
                "nome": "NF-E EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                "pessoa_fisica_juridica": "person",
                "telefone": "21988766743",
                "inscricao_estadual": "0736913700156",
                "inscricao_municipal": "",
                "inscricao_suframa": "",
                "indicador_inscricao_estadual": 1,
                "email": "teste@teste.com",
                "endereco": {
                  "logradouro": "Rua do Consultor",
                  "complemento": "BL A",
                  "numero": "14",
                  "bairro": "Bairro teste",
                  "codigo_municipio": "5300108",
                  "nome_municipio": "Brasilia",
                  "codigo_pais": "1058",
                  "nome_pais": "Brasil",
                  "uf": "DF",
                  "cep": "05685040"
                }
              },
              "produtos": [
                {
                  "codigo_produto": 14589,
                  "codigo_ean": 7891125063000,
                  "descricao": "VODKA NATASHA 1L UN 1X1000ML",
                  "cfop": 5403, # CFOP de Saída
                  "valor_unitario_comercial": 10.38,
                  "valor_unitario_tributario": 10.38,
                  "valor_total_produto": "62.28",
                  "valor_desconto": 10.90,
                  "quantidade_comercial": 6,
                  "quantidade_tributaria": 6,
                  "unidade_comercial": "UN",
                  "unidade_tributaria": "UN",
                  "num_pedido": 5100003910,
                  "num_item_pedido": 1,
                  "ean_unidade_trib": 7891125063000,
                  "extipi": 22,
                  "ncm": 22086000,
                  "cest": 1300402,
                  "producao_escala": "s",
                  "valor_frete": 10,
                  "valor_seguro": 11.50,
                  "outras_despesas": 20,
                  "tributacao": {
                    "valor_aproximado_total": 50.21,
                    "icms": {
                      "situacao_tributaria": "10",
                      "modalidade_base_calculo": 3,
                      "codigo_origem_produto": 0,
                      "valor_base_calculo": 62.32,
                      "aliquota_icms": 29,
                      "valor_icms": 18.07,
                      "modalidade_base_calculo_st": 4,
                      "valor_base_calculo_st": 80.41,
                      "perc_mva_icms_st": 29.0400,
                      "aliquota_icms_st": 31,
                      "valor_icms_st": 6.86,
                      "valor_fcp_interestadual": 19.61
                    },
                    "ipi": {
                      "situacao_tributaria": "99",
                      "codigo_enquadramento": 999,
                      "valor_ipi": 14.4
                    },
                    "pis": {
                      "situacao_tributaria": "01",
                      "valor_base_calculo": 62.32,
                      "aliquota_pis": 1.65,
                      "valor_pis": 1.03
                    },
                    "cofins": {
                      "situacao_tributaria": "01",
                      "valor_base_calculo": "129.62",
                      "aliquota_cofins": "7.60",
                      "valor_cofins": "9.85"
                    }
                  }
                }
              ],
              "forma_de_pagamento": [
                {
                  "tipo_de_pagamento": "01",
                  "valor_do_pagamento": 114.14
                }
              ],
              "transporte": {
                "valor_total_frete": 0,
                "codigo_modalidade": 9,
                "codigo_transportadora": 1,
                "transportadora": {
                  "cnpj_cpf": 81043396000156,
                  "razao_social": "teste",
                  "inscricao_estadual": "",
                  "insencao_icms": "",
                  "endereco_completo": "rua teste, 111",
                  "municipio": "Brasilia",
                  "uf": "DF"
                },
                "volume_transportado": [
                  {
                    "quantidade_volumes": 5,
                    "numeracao_volumes": 333,
                    "marca": "teste",
                    "especie": "pacote",
                    "peso_liquido": "3000",
                    "peso_bruto": "4050"
                  }
                ]
              }
            }
          ]
        }
      }'


EXEMPLO DE RESPOSTA

{
  "nfe_batch": {
    "id": 1,
    "key": null,
    "request_id": "7d391761-1681-4e9c-ac6e-d47389f211f0",
    "remote_id": null,
    "nfes": [
      {
        "access_key": null,
        "id": 351, # Identificador da NF-e
        "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
        "remote_id": null,
        "organization_id": 1,
        "status": "processing"
      }
    ]
  }
}
```

A resposta conterá os mesmos campos que foram enviados na requisição, e adicionalmente campos exclusivos específicos sobre o status de rejeição da NF-e:

Para consultar a NF-e criada, é necessário realizar a seguinte requisição utilizando o identificador da NF-e contido na resposta:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/11/nfe/351 \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'


EXEMPLO DE RESPOSTA:

{
  "nfe": {
    "access_key": null,
    "id": 351,
    "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
    "remote_id": null,
    "organization_id": 1,
    "status": "rejected",
    "data": {
      ...
      "resposta_emissao": {
        "erros": [
          "519 = Rejeicao: CFOP de saida para NF-e de entrada"
        ]
      }
    },
    "danfe_url": "",
    "xml_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfe/xml_files/000/015/351/original/nfe.xml?15379",
    "taxrules_calculation_log": null
  }
}
```

## Consulta NF-e Denegada (SEFAZ)

Segue abaixo um exemplo de requisição de emissão em lote com uma NF-e denegada na SEFAZ que será utilizado para posterior consulta (Só será denegada se houverem irregularidades na SEFAZ com as partes envolvidas na emissão, no caso, emitente ou destinatário):

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/nfe_batch \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json' \
  -d '{
        "nfe_batch": {
          "lote": 1,
          "sincronicidade": 0,
          "serie": 611,
          "uf": 53,
          "nfes": [
            {
              "dados_gerais": {
                "uf": 53,
                "codigo_mun_ocorrencia": "5300108",
                "natureza_operacao": "saida",
                "tipo_operacao": 0, # Alterado para NF-e de Entrada
                "indicador_consumidor_final": 0,
                "indicador_presenca": 0,
                "finalidade_nfe": 1,
                "destino_operacao": "1"
              },
              "cliente": {
                "cpf_cnpj": "68763591669",
                "nome": "NF-E EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                "pessoa_fisica_juridica": "person",
                "telefone": "21988766743",
                "inscricao_estadual": "0736913700156",
                "inscricao_municipal": "",
                "inscricao_suframa": "",
                "indicador_inscricao_estadual": 1,
                "email": "teste@teste.com",
                "endereco": {
                  "logradouro": "Rua do Consultor",
                  "complemento": "BL A",
                  "numero": "14",
                  "bairro": "Bairro teste",
                  "codigo_municipio": "5300108",
                  "nome_municipio": "Brasilia",
                  "codigo_pais": "1058",
                  "nome_pais": "Brasil",
                  "uf": "DF",
                  "cep": "05685040"
                }
              },
              "produtos": [
                {
                  "codigo_produto": 14589,
                  "codigo_ean": 7891125063000,
                  "descricao": "VODKA NATASHA 1L UN 1X1000ML",
                  "cfop": 5403, # CFOP de Saída
                  "valor_unitario_comercial": 10.38,
                  "valor_unitario_tributario": 10.38,
                  "valor_total_produto": "62.28",
                  "valor_desconto": 10.90,
                  "quantidade_comercial": 6,
                  "quantidade_tributaria": 6,
                  "unidade_comercial": "UN",
                  "unidade_tributaria": "UN",
                  "num_pedido": 5100003910,
                  "num_item_pedido": 1,
                  "ean_unidade_trib": 7891125063000,
                  "extipi": 22,
                  "ncm": 22086000,
                  "cest": 1300402,
                  "producao_escala": "s",
                  "valor_frete": 10,
                  "valor_seguro": 11.50,
                  "outras_despesas": 20,
                  "tributacao": {
                    "valor_aproximado_total": 50.21,
                    "icms": {
                      "situacao_tributaria": "10",
                      "modalidade_base_calculo": 3,
                      "codigo_origem_produto": 0,
                      "valor_base_calculo": 62.32,
                      "aliquota_icms": 29,
                      "valor_icms": 18.07,
                      "modalidade_base_calculo_st": 4,
                      "valor_base_calculo_st": 80.41,
                      "perc_mva_icms_st": 29.0400,
                      "aliquota_icms_st": 31,
                      "valor_icms_st": 6.86,
                      "valor_fcp_interestadual": 19.61
                    },
                    "ipi": {
                      "situacao_tributaria": "99",
                      "codigo_enquadramento": 999,
                      "valor_ipi": 14.4
                    },
                    "pis": {
                      "situacao_tributaria": "01",
                      "valor_base_calculo": 62.32,
                      "aliquota_pis": 1.65,
                      "valor_pis": 1.03
                    },
                    "cofins": {
                      "situacao_tributaria": "01",
                      "valor_base_calculo": "129.62",
                      "aliquota_cofins": "7.60",
                      "valor_cofins": "9.85"
                    }
                  }
                }
              ],
              "forma_de_pagamento": [
                {
                  "tipo_de_pagamento": "01",
                  "valor_do_pagamento": 114.14
                }
              ],
              "transporte": {
                "valor_total_frete": 0,
                "codigo_modalidade": 9,
                "codigo_transportadora": 1,
                "transportadora": {
                  "cnpj_cpf": 81043396000156,
                  "razao_social": "teste",
                  "inscricao_estadual": "",
                  "insencao_icms": "",
                  "endereco_completo": "rua teste, 111",
                  "municipio": "Brasilia",
                  "uf": "DF"
                },
                "volume_transportado": [
                  {
                    "quantidade_volumes": 5,
                    "numeracao_volumes": 333,
                    "marca": "teste",
                    "especie": "pacote",
                    "peso_liquido": "3000",
                    "peso_bruto": "4050"
                  }
                ]
              }
            }
          ]
        }
      }'


EXEMPLO DE RESPOSTA

{
  "nfe_batch": {
    "id": 170,
    "key": null,
    "request_id": "7d391761-1681-4e9c-ac6e-d47389f211f0",
    "remote_id": null,
    "nfes": [
      {
        "access_key": null,
        "id": 351,
        "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
        "remote_id": null,
        "organization_id": 1,
        "status": "processing"
      }
    ]
  }
}
```

A resposta conterá os mesmos campos que foram enviados na requisição, e adicionalmente campos exclusivos específicos sobre o status de rejeição da NF-e:

Para consultar a NF-e criada, é necessário realizar a seguinte requisição utilizando o identificador da NF-e contido na resposta:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/11/nfe/351 \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'


EXEMPLO DE RESPOSTA:

{
  "nfe": {
    "access_key": null,
    "id": 351,
    "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
    "remote_id": null,
    "organization_id": 1,
    "status": "denegated",
    "data": {
      ...
      "resposta_emissao": {
        "erros": [
          "303 = Uso Denegado: Destinatário não habilitado a operar na UF"
        ]
      }
    },
    "danfe_url": "",
    "xml_url": "",
    "taxrules_calculation_log": null
  }
}
```

## Consulta NF-e Rejeitada (Validação)

Segue abaixo um exemplo de requisição de emissão em lote com rejeição por erro de validação de Schema que será utilizado para posterior consulta:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/nfe_batch \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json' \
  -d '{
        "nfe_batch": {
          "lote": 1,
          "sincronicidade": 0,
          "serie": 611,
          "uf": 53,
          "nfes": [
            {
              "dados_gerais": {
                "uf": 53,
                "codigo_mun_ocorrencia": "5300108",
                "natureza_operacao": "saida",
                "tipo_operacao": 3, # Alterado para valor que não existe
                "indicador_consumidor_final": 0,
                "indicador_presenca": 0,
                "finalidade_nfe": 1,
                "destino_operacao": "1"
              },
              "cliente": {
                "cpf_cnpj": "68763591669",
                "nome": "NF-E EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                "pessoa_fisica_juridica": "person",
                "telefone": "21988766743",
                "inscricao_estadual": "0736913700156",
                "inscricao_municipal": "",
                "inscricao_suframa": "",
                "indicador_inscricao_estadual": 1,
                "email": "teste@teste.com",
                "endereco": {
                  "logradouro": "Rua do Consultor",
                  "complemento": "BL A",
                  "numero": "14",
                  "bairro": "Bairro teste",
                  "codigo_municipio": "5300108",
                  "nome_municipio": "Brasilia",
                  "codigo_pais": "1058",
                  "nome_pais": "Brasil",
                  "uf": "DF",
                  "cep": "05685040"
                }
              },
              "produtos": [
                {
                  "codigo_produto": 14589,
                  "codigo_ean": 7891125063000,
                  "descricao": "VODKA NATASHA 1L UN 1X1000ML",
                  "cfop": 5403,
                  "valor_unitario_comercial": 10.38,
                  "valor_unitario_tributario": 10.38,
                  "valor_total_produto": "62.28",
                  "valor_desconto": 10.90,
                  "quantidade_comercial": 6,
                  "quantidade_tributaria": 6,
                  "unidade_comercial": "UN",
                  "unidade_tributaria": "UN",
                  "num_pedido": 5100003910,
                  "num_item_pedido": 1,
                  "ean_unidade_trib": 7891125063000,
                  "extipi": 22,
                  "ncm": 22086000,
                  "cest": 1300402,
                  "producao_escala": "s",
                  "valor_frete": 10,
                  "valor_seguro": 11.50,
                  "outras_despesas": 20,
                  "tributacao": {
                    "valor_aproximado_total": 50.21,
                    "icms": {
                      "situacao_tributaria": "10",
                      "modalidade_base_calculo": 3,
                      "codigo_origem_produto": 0,
                      "valor_base_calculo": 62.32,
                      "aliquota_icms": 29,
                      "valor_icms": 18.07,
                      "modalidade_base_calculo_st": 4,
                      "valor_base_calculo_st": 80.41,
                      "perc_mva_icms_st": 29.0400,
                      "aliquota_icms_st": 31,
                      "valor_icms_st": 6.86,
                      "valor_fcp_interestadual": 19.61
                    },
                    "ipi": {
                      "situacao_tributaria": "99",
                      "codigo_enquadramento": 999,
                      "valor_ipi": 14.4
                    },
                    "pis": {
                      "situacao_tributaria": "01",
                      "valor_base_calculo": 62.32,
                      "aliquota_pis": 1.65,
                      "valor_pis": 1.03
                    },
                    "cofins": {
                      "situacao_tributaria": "01",
                      "valor_base_calculo": "129.62",
                      "aliquota_cofins": "7.60",
                      "valor_cofins": "9.85"
                    }
                  }
                }
              ],
              "forma_de_pagamento": [
                {
                  "tipo_de_pagamento": "01",
                  "valor_do_pagamento": 114.14
                }
              ],
              "transporte": {
                "valor_total_frete": 0,
                "codigo_modalidade": 9,
                "codigo_transportadora": 1,
                "transportadora": {
                  "cnpj_cpf": 81043396000156,
                  "razao_social": "teste",
                  "inscricao_estadual": "",
                  "insencao_icms": "",
                  "endereco_completo": "rua teste, 111",
                  "municipio": "Brasilia",
                  "uf": "DF"
                },
                "volume_transportado": [
                  {
                    "quantidade_volumes": 5,
                    "numeracao_volumes": 333,
                    "marca": "teste",
                    "especie": "pacote",
                    "peso_liquido": "3000",
                    "peso_bruto": "4050"
                  }
                ]
              }
            }
          ]
        }
      }'


EXEMPLO DE RESPOSTA

{
  "nfe_batch": {
    "id": 171,
    "key": null,
    "request_id": "7d391761-1681-4e9c-ac6e-d47389f211f0",
    "remote_id": null,
    "nfes": [
      {
        "access_key": null,
        "id": 352, # Identificador da NF-e
        "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
        "remote_id": null,
        "organization_id": 1,
        "status": "processing"
      }
    ]
  }
}
```

A resposta conterá os mesmos campos que foram enviados na requisição, e adicionalmente campos exclusivos específicos sobre o status de rejeição causada por erro de validação de Schema da NF-e:

Para consultar a NF-e criada, é necessário realizar a seguinte requisição utilizando o identificador da NF-e contido na resposta:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/11/nfe/352 \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'


EXEMPLO DE RESPOSTA:

{
  "nfe": {
    "access_key": null,
    "id": 352,
    "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
    "remote_id": null,
    "organization_id": 1,
    "status": "rejected",
    "data": {
      ...
      "resposta_emissao": {
        "erros": [
          "O campo 'tpNF' contém o valor '3' mas não está entre: '{'0', '1'}'. Verifique o node: dados_gerais.tipo_operacao",
          "O valor '3' do campo 'tpNF' não é válido. Verifique o node: dados_gerais.tipo_operacao"
        ]
      }
    },
    "danfe_url": "",
    "xml_url": "",
    "taxrules_calculation_log": null
  }
}
```

## Consulta NFC-e Emitida

Segue abaixo um exemplo de requisição de emissão em lote com sucesso que será utilizado para posterior consulta:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/nfce_batch \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json' \
  -d '{
        "nfce_batch": {
          "lote": 1,
          "sincronicidade": 0,
          "uf": "53",
          "serie": 717,
          "remote_id": "123abc",
          "nfces": [
            {
              "dados_gerais": {
                "uf": "53",
                "serie": 717,
                "codigo_mun_ocorrencia": "5300108",
                "natureza_operacao": "saida",
                "csc": "000009",
                "id_token": "A16A5A2DD8FA443FV6710F5AB8EB5432",
                "tipo_operacao": "1",
                "destino_operacao": "1",
                "finalidade_nfe": "1",
                "indicador_presenca": "1"
              },
              "produtos": [
                {
                  "informacoes_adicionais": "teste",
                  "codigo_produto": "14600",
                  "codigo_ean": "7891000315507",
                  "descricao": "NOTA FISCAL EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                  "ncm": "22086000",
                  "cest": "1300402",
                  "extipi": "22",
                  "cfop": "5103",
                  "unidade_comercial": "UN",
                  "ean_unidade_trib": "7891000315507",
                  "unidade_tributaria": "UN",
                  "num_pedido": "5100003910",
                  "num_item_pedido": "1",
                  "quantidade_comercial": 739,
                  "valor_unitario_comercial": 0.4086,
                  "quantidade_tributaria": 739,
                  "valor_unitario_tributario": 0.4086,
                  "valor_frete": 0,
                  "valor_seguro": 0,
                  "valor_desconto": 0,
                  "valor_total_produto": 301.96,
                  "outras_despesas": 0,
                  "tributacao": {
                    "valor_aproximado_total": 82.28,
                    "icms": {
                      "aliquota_icms": 18,
                      "valor_base_calculo": 301.96,
                      "valor_icms": 54.35,
                      "modalidade_base_calculo": "1",
                      "codigo_origem_produto": 0,
                      "situacao_tributaria": "00"
                    },
                    "pis": {
                      "valor_base_calculo": 301.96,
                      "situacao_tributaria": "01",
                      "aliquota_pis": 1.65,
                      "valor_pis": 4.98
                    },
                    "cofins": {
                      "valor_base_calculo": 301.96,
                      "situacao_tributaria": "01",
                      "aliquota_cofins": 7.6,
                      "valor_cofins": 22.95
                    }
                  }
                }
              ],
              "forma_de_pagamento": [
                {
                  "tipo_de_pagamento": "03",
                  "valor_do_pagamento": 301.96,
                  "tipo_de_integracao": 1,
                  "cnpj_credenciadora": "64187888000104",
                  "bandeira_operadora": "01",
                  "numero_autorizacao_operacao": "1"
                }
              ]
            }
          ]
        }
      }'


EXEMPLO DE RESPOSTA

{
  "nfce_batch": {
    "id": 53,
    "key": null,
    "request_id": "7d391761-1681-4e9c-ac6e-d47389f211f0",
    "remote_id": "123abc",
    "nfces": [
      {
        "access_key": null,
        "id": 109, # Identificador da NFC-e
        "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
        "remote_id": null,
        "organization_id": 1,
        "status": "processing"
      }
    ]
  }
}
```

A resposta conterá os mesmos campos que foram enviados na requisição, e adicionalmente campos exclusivos específicos sobre o status da NFC-e:

Para consultar a NFC-e criada, é necessário realizar a seguinte requisição utilizando o identificador da NFC-e contido na resposta:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/11/nfce/109 \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'


EXEMPLO DE RESPOSTA:

{
  "nfce": {
    "access_key": "53190222769530000131657170000000501127125918",
    "id": 109,
    "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
    "remote_id": null,
    "organization_id": 1,
    "status": "succeeded",
    "data": {
      ...
      "resposta_emissao": {
        "data_emissao": "2019-02-21T12:04:39.000-03:00",
        "codigo_verificacao": "blHtjEXhgCfW8LknVU9QKfbBM4o=",
        "numero_protocolo": "353190000052272",
        "chave_acesso": "53190222769530000131657170000000501127125918"
      }
    },
    "danfe_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfce/pdf_files/000/015/109/original/danfe.pdf?153719",
    "xml_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfce/xml_files/000/015/109/original/nfce.xml?15379",
    "taxrules_calculation_log": null
  }
}

EXEMPLO DE REQUISIÇÃO USANDO CHAVE DE ACESSO

curl -X GET \
  https://app.emites.com.br/api/v1/organizations/11/nfce/53190222769530000131657170000000501127125918 \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'


EXEMPLO DE RESPOSTA:

{
  "nfce": {
    "access_key": "53190222769530000131657170000000501127125918",
    "id": 109,
    "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
    "remote_id": null,
    "organization_id": 1,
    "status": "succeeded",
    "data": {
      ...
      "resposta_emissao": {
        "data_emissao": "2019-02-21T12:04:39.000-03:00",
        "codigo_verificacao": "blHtjEXhgCfW8LknVU9QKfbBM4o=",
        "numero_protocolo": "353190000052272",
        "chave_acesso": "53190222769530000131657170000000501127125918"
      }
    },
    "danfe_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfce/pdf_files/000/015/109/original/danfe.pdf?153719",
    "xml_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfce/xml_files/000/015/109/original/nfce.xml?15379",
    "taxrules_calculation_log": null
  }
}
```

## Consulta NFC-e Rejeitada (SEFAZ)

Segue abaixo um exemplo de requisição de emissão em lote com rejeição da SEFAZ que será utilizado para posterior consulta:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/nfce_batch \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json' \
  -d '{
        "nfce_batch": {
          "lote": 1,
          "sincronicidade": 0,
          "uf": "53",
          "serie": 717,
          "nfces": [
            {
              "dados_gerais": {
                "uf": "53",
                "serie": 717,
                "codigo_mun_ocorrencia": "5300108",
                "natureza_operacao": "saida",
                "csc": "000009",
                "id_token": "A16A5A2DD8FA443FV6710F5AB8EB5432",
                "tipo_operacao": 0, # Alterado para NFC-e de Entrada
                "destino_operacao": "1",
                "finalidade_nfe": "1",
                "indicador_presenca": "1"
              },
              "produtos": [
                {
                  "informacoes_adicionais": "teste",
                  "codigo_produto": "14600",
                  "codigo_ean": "7891000315507",
                  "descricao": "NOTA FISCAL EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                  "ncm": "22086000",
                  "cest": "1300402",
                  "extipi": "22",
                  "cfop": "5103",
                  "unidade_comercial": "UN",
                  "ean_unidade_trib": "7891000315507",
                  "unidade_tributaria": "UN",
                  "num_pedido": "5100003910",
                  "num_item_pedido": "1",
                  "quantidade_comercial": 739,
                  "valor_unitario_comercial": 0.4086,
                  "quantidade_tributaria": 739,
                  "valor_unitario_tributario": 0.4086,
                  "valor_frete": 0,
                  "valor_seguro": 0,
                  "valor_desconto": 0,
                  "valor_total_produto": 301.96,
                  "outras_despesas": 0,
                  "tributacao": {
                    "valor_aproximado_total": 82.28,
                    "icms": {
                      "aliquota_icms": 18,
                      "valor_base_calculo": 301.96,
                      "valor_icms": 54.35,
                      "modalidade_base_calculo": "1",
                      "codigo_origem_produto": 0,
                      "situacao_tributaria": "00"
                    },
                    "pis": {
                      "valor_base_calculo": 301.96,
                      "situacao_tributaria": "01",
                      "aliquota_pis": 1.65,
                      "valor_pis": 4.98
                    },
                    "cofins": {
                      "valor_base_calculo": 301.96,
                      "situacao_tributaria": "01",
                      "aliquota_cofins": 7.6,
                      "valor_cofins": 22.95
                    }
                  }
                }
              ],
              "forma_de_pagamento": [
                {
                  "tipo_de_pagamento": "03",
                  "valor_do_pagamento": 301.96,
                  "tipo_de_integracao": 1,
                  "cnpj_credenciadora": "64187888000104",
                  "bandeira_operadora": "01",
                  "numero_autorizacao_operacao": "1"
                }
              ]
            }
          ]
        }
      }'


EXEMPLO DE RESPOSTA

{
  "nfce_batch": {
    "id": 53,
    "key": null,
    "request_id": "7d391761-1681-4e9c-ac6e-d47389f211f0",
    "remote_id": null,
    "nfces": [
      {
        "access_key": null,
        "id": 110, # Identificador da NFC-e
        "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
        "remote_id": null,
        "organization_id": 1,
        "status": "processing"
      }
    ]
  }
}
```

A resposta conterá os mesmos campos que foram enviados na requisição, e adicionalmente campos exclusivos específicos sobre o status de rejeição da NFC-e:

Para consultar a NFC-e criada, é necessário realizar a seguinte requisição utilizando o identificador da NFC-e contido na resposta:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/11/nfce/110 \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'


EXEMPLO DE RESPOSTA:

{
  "nfce": {
    "access_key": null,
    "id": 110,
    "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
    "remote_id": null,
    "organization_id": 1,
    "status": "rejected",
    "data": {
      ...
      "resposta_emissao": {
        "erros": [
          "706 = Rejeicao: NFC-e para operacao de entrada"
        ]
      }
    },
    "danfe_url": "",
    "xml_url": "http://emites-ruby-sandbox.s3.amazonaws.com/nfce/xml_files/000/015/110/original/nfce.xml?15379",
    "taxrules_calculation_log": null
  }
}
```

## Consulta NFC-e Denegada (SEFAZ)

Segue abaixo um exemplo de requisição de emissão em lote com uma NFC-e denegada na SEFAZ que será utilizado para posterior consulta (Só será denegada se houverem irregularidades na SEFAZ com as partes envolvidas na emissão, no caso, emitente ou destinatário):

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/nfce_batch \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json' \
  -d '{
        "nfce_batch": {
          "lote": 1,
          "sincronicidade": 0,
          "uf": "53",
          "serie": 717,
          "nfces": [
            {
              "dados_gerais": {
                "uf": "53",
                "serie": 717,
                "codigo_mun_ocorrencia": "5300108",
                "natureza_operacao": "saida",
                "csc": "000009",
                "id_token": "A16A5A2DD8FA443FV6710F5AB8EB5432",
                "tipo_operacao": 0, # Alterado para NFC-e de Entrada
                "destino_operacao": "1",
                "finalidade_nfe": "1",
                "indicador_presenca": "1"
              },
              "produtos": [
                {
                  "informacoes_adicionais": "teste",
                  "codigo_produto": "14600",
                  "codigo_ean": "7891000315507",
                  "descricao": "NOTA FISCAL EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                  "ncm": "22086000",
                  "cest": "1300402",
                  "extipi": "22",
                  "cfop": "5103",
                  "unidade_comercial": "UN",
                  "ean_unidade_trib": "7891000315507",
                  "unidade_tributaria": "UN",
                  "num_pedido": "5100003910",
                  "num_item_pedido": "1",
                  "quantidade_comercial": 739,
                  "valor_unitario_comercial": 0.4086,
                  "quantidade_tributaria": 739,
                  "valor_unitario_tributario": 0.4086,
                  "valor_frete": 0,
                  "valor_seguro": 0,
                  "valor_desconto": 0,
                  "valor_total_produto": 301.96,
                  "outras_despesas": 0,
                  "tributacao": {
                    "valor_aproximado_total": 82.28,
                    "icms": {
                      "aliquota_icms": 18,
                      "valor_base_calculo": 301.96,
                      "valor_icms": 54.35,
                      "modalidade_base_calculo": "1",
                      "codigo_origem_produto": 0,
                      "situacao_tributaria": "00"
                    },
                    "pis": {
                      "valor_base_calculo": 301.96,
                      "situacao_tributaria": "01",
                      "aliquota_pis": 1.65,
                      "valor_pis": 4.98
                    },
                    "cofins": {
                      "valor_base_calculo": 301.96,
                      "situacao_tributaria": "01",
                      "aliquota_cofins": 7.6,
                      "valor_cofins": 22.95
                    }
                  }
                }
              ],
              "forma_de_pagamento": [
                {
                  "tipo_de_pagamento": "03",
                  "valor_do_pagamento": 301.96,
                  "tipo_de_integracao": 1,
                  "cnpj_credenciadora": "64187888000104",
                  "bandeira_operadora": "01",
                  "numero_autorizacao_operacao": "1"
                }
              ]
            }
          ]
        }
      }'


EXEMPLO DE RESPOSTA

{
  "nfce_batch": {
    "id": 53,
    "key": null,
    "request_id": "7d391761-1681-4e9c-ac6e-d47389f211f0",
    "remote_id": null,
    "nfces": [
      {
        "access_key": null,
        "id": 110, # Identificador da NFC-e
        "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
        "remote_id": null,
        "organization_id": 1,
        "status": "processing"
      }
    ]
  }
}
```

A resposta conterá os mesmos campos que foram enviados na requisição, e adicionalmente campos exclusivos específicos sobre o status de rejeição da NFC-e:

Para consultar a NFC-e criada, é necessário realizar a seguinte requisição utilizando o identificador da NFC-e contido na resposta:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/11/nfce/110 \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'


EXEMPLO DE RESPOSTA:

{
  "nfce": {
    "access_key": null,
    "id": 110,
    "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
    "remote_id": null,
    "organization_id": 1,
    "status": "denegated",
    "data": {
      ...
      "resposta_emissao": {
        "erros": [
          "303 = Uso Denegado: Destinatário não habilitado a operar na UF"
        ]
      }
    },
    "danfe_url": "",
    "xml_url": "",
    "taxrules_calculation_log": null
  }
}
```

## Consulta NFC-e Rejeitada (Validação)

Segue abaixo um exemplo de requisição de emissão em lote com rejeição por erro de validação de Schema que será utilizado para posterior consulta:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/nfce_batch \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json' \
  -d '{
        "nfce_batch": {
          "lote": 1,
          "sincronicidade": 0,
          "uf": "53",
          "serie": 717,
          "nfces": [
            {
              "dados_gerais": {
                "uf": "53",
                "serie": 717,
                "codigo_mun_ocorrencia": "5300108",
                "natureza_operacao": "saida",
                "csc": "000009",
                "id_token": "A16A5A2DD8FA443FV6710F5AB8EB5432",
                "tipo_operacao": "1",
                "destino_operacao": "5",
                "finalidade_nfe": "1",
                "indicador_presenca": "1"
              },
              "produtos": [
                {
                  "informacoes_adicionais": "teste",
                  "codigo_produto": "14600",
                  "codigo_ean": "7891000315507",
                  "descricao": "NOTA FISCAL EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                  "ncm": "22086000",
                  "cest": "1300402",
                  "extipi": "22",
                  "cfop": "5103",
                  "unidade_comercial": "UN",
                  "ean_unidade_trib": "7891000315507",
                  "unidade_tributaria": "UN",
                  "num_pedido": "5100003910",
                  "num_item_pedido": "1",
                  "quantidade_comercial": 739,
                  "valor_unitario_comercial": 0.4086,
                  "quantidade_tributaria": 739,
                  "valor_unitario_tributario": 0.4086,
                  "valor_frete": 0,
                  "valor_seguro": 0,
                  "valor_desconto": 0,
                  "valor_total_produto": 301.96,
                  "outras_despesas": 0,
                  "tributacao": {
                    "valor_aproximado_total": 82.28,
                    "icms": {
                      "aliquota_icms": 18,
                      "valor_base_calculo": 301.96,
                      "valor_icms": 54.35,
                      "modalidade_base_calculo": "1",
                      "codigo_origem_produto": 0,
                      "situacao_tributaria": "00"
                    },
                    "pis": {
                      "valor_base_calculo": 301.96,
                      "situacao_tributaria": "01",
                      "aliquota_pis": 1.65,
                      "valor_pis": 4.98
                    },
                    "cofins": {
                      "valor_base_calculo": 301.96,
                      "situacao_tributaria": "01",
                      "aliquota_cofins": 7.6,
                      "valor_cofins": 22.95
                    }
                  }
                }
              ],
              "forma_de_pagamento": [
                {
                  "tipo_de_pagamento": "03",
                  "valor_do_pagamento": 301.96,
                  "tipo_de_integracao": 1,
                  "cnpj_credenciadora": "64187888000104",
                  "bandeira_operadora": "01",
                  "numero_autorizacao_operacao": "1"
                }
              ]
            }
          ]
        }
      }'


EXEMPLO DE RESPOSTA

{
  "nfce_batch": {
    "id": 53,
    "key": null,
    "request_id": "7d391761-1681-4e9c-ac6e-d47389f211f0",
    "remote_id": null,
    "nfces": [
      {
        "id": 111, # Identificador da NFC-e
        "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
        "remote_id": null,
        "organization_id": 1,
        "status": "processing"
      }
    ]
  }
}
```

A resposta conterá os mesmos campos que foram enviados na requisição, e adicionalmente campos exclusivos específicos sobre o status de rejeição causada por erro de validação de Schema da NFC-e:

Para consultar a NFC-e criada, é necessário realizar a seguinte requisição utilizando o identificador da NFC-e contido na resposta:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/11/nfce/111 \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'


EXEMPLO DE RESPOSTA:

{
  "nfce": {
    "access_key": null,
    "id": 111,
    "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
    "remote_id": null,
    "organization_id": 1,
    "status": "rejected",
    "data": {
      ...
      "resposta_emissao": {
        "erros": [
          "O campo 'idDest' contém o valor '5' mas não está entre: '{'1', '2', '3'}'. Verifique o node: dados_gerais.destino_operacao",
          "O valor '5' do campo 'idDest' não é válido. Verifique o node: dados_gerais.destino_operacao"
        ]
      }
    },
    "danfe_url": "",
    "xml_url": "",
    "taxrules_calculation_log": null
  }
}
```

## Valor Total por Período Fixo

Segue abaixo um exemplo de requisição para consultar o valor total de vendas em um determinado dia:

```shell
EXEMPLO DE REQUISIÇÃO

curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/11/document_totals \
  -d '{"cfop":"5000", "date": "20/08/2019", "date_type": "day"}'
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'

EXEMPLO DE RESPOSTA:

{
  "vICMS": 2000.00,
  "vII": 0.00,
  "vCOFINS": 2987.65,
  "vPIS": 4500.40,
  "vNF": 10000.00
}
```
