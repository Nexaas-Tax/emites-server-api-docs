# Armazenamento de CF-e

Para armazenar uma CF-e, é necessário realizar uma requisição POST para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">POST</i>
        <h6>/api/v1/organizations/{organization_id}/cfe</h6>
    </div>
</div>

<aside class="notice">
  O valor do campo "xml" deve conter o XML da CF-e. Já o campo "danfe" deve conter a DANFE da CF-e em PDF codificado em **Base64**. Ambos os campos são obrigatórios para que o CF-e seja armazenado com sucesso.
</aside>

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/cfe \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json' \
  -d '{
        "cfe": {
          "xml": "<nfeProc xmlns="http://www.portalfiscal.inf.br/nfe" versao="4.00"><enviNFe xmlns="http://www.portalfiscal.inf.br/nfe" versao="4.00"><NFe><infNFe></infNFe></NFe></enviNFe></nfeProc>",
          "danfe": "JVBERi0xLjMKJcTl8uXrp/Og0MTGCjQgMCBvYmoKPDwgL0xlbmd0aCA1IDAg\nUiAvRmlsdGVyIC9GbGF0ZURlY29kZSA+PgpzdHJlYW0KeAErVAhUKFQwAEJT\nS1M9IwsFCxNDPQtLhaJUhXCFPAV952JDheRiBUMwLE4GqoMqyAVqMINxckAc\nLl0DPUMDS0sLUxOFHKBCFG6GQppCIAAgiBeUCmVuZHN0cmVhbQplbmRvYmoK\nNSAwIG9iago4NAplbmRvYmoKMiAwIG9iago8PCAvVHlwZSAvUGFnZSAvUGFy\nZW50IDMgMCBSIC9SZXNvdXJjZXMgNiAwIFIgL0NvbnRlbnRzIDQgMCBSIC9N\nZWRpYUJveCBbMCAwIDU5NS4yOCA4NDEuODldCj4+CmVuZG9iago2IDAgb2Jq\nCjw8IC9Qcm9jU2V0IFsgL1BERiBdIC9Db2xvclNwYWNlIDw8IC9DczEgNyAw\nIFIgPj4gPj4KZW5kb2JqCjggMCBvYmoKPDwgL0xlbmd0aCA5IDAgUiAvTiAz\nIC9BbHRlcm5hdGUgL0RldmljZVJHQiAvRmlsdGVyIC9GbGF0ZURlY29kZSA+\nPgpzdHJlYW0KeAGdlndUU9kWh8+9N73QEiIgJfQaegkg0jtIFQRRiUmAUAKG\nhCZ2RAVGFBEpVmRUwAFHhyJjRRQLg4Ji1wnyEFDGwVFEReXdjGsJ7601896a\n/cdZ39nnt9fZZ+9917oAUPyCBMJ0WAGANKFYFO7rwVwSE8vE9wIYEAEOWAHA\n4WZmBEf4RALU/L09mZmoSMaz9u4ugGS72yy/UCZz1v9/kSI3QyQGAApF1TY8\nfiYX5QKUU7PFGTL/BMr0lSkyhjEyFqEJoqwi48SvbPan5iu7yZiXJuShGlnO\nGbw0noy7UN6aJeGjjAShXJgl4GejfAdlvVRJmgDl9yjT0/icTAAwFJlfzOcm\noWyJMkUUGe6J8gIACJTEObxyDov5OWieAHimZ+SKBIlJYqYR15hp5ejIZvrx\ns1P5YjErlMNN4Yh4TM/0tAyOMBeAr2+WRQElWW2ZaJHtrRzt7VnW5mj5v9nf\nHn5T/T3IevtV8Sbsz55BjJ5Z32zsrC+9FgD2JFqbHbO+lVUAtG0GQOXhrE/v\nIADyBQC03pzzHoZsXpLE4gwnC4vs7GxzAZ9rLivoN/ufgm/Kv4Y595nL7vtW\nO6YXP4EjSRUzZUXlpqemS0TMzAwOl89k/fcQ/+PAOWnNycMsnJ/AF/GF6FVR\n6JQJhIlou4U8gViQLmQKhH/V4X8YNicHGX6daxRodV8AfYU5ULhJB8hvPQBD\nIwMkbj96An3rWxAxCsi+vGitka9zjzJ6/uf6Hwtcim7hTEEiU+b2DI9kciWi\nLBmj34RswQISkAd0oAo0gS4wAixgDRyAM3AD3iAAhIBIEAOWAy5IAmlABLJB\nPtgACkEx2AF2g2pwANSBetAEToI2cAZcBFfADXALDIBHQAqGwUswAd6BaQiC\n8BAVokGqkBakD5lC1hAbWgh5Q0FQOBQDxUOJkBCSQPnQJqgYKoOqoUNQPfQj\ndBq6CF2D+qAH0CA0Bv0BfYQRmALTYQ3YALaA2bA7HAhHwsvgRHgVnAcXwNvh\nSrgWPg63whfhG/AALIVfwpMIQMgIA9FGWAgb8URCkFgkAREha5EipAKpRZqQ\nDqQbuY1IkXHkAwaHoWGYGBbGGeOHWYzhYlZh1mJKMNWYY5hWTBfmNmYQM4H5\ngqVi1bGmWCesP3YJNhGbjS3EVmCPYFuwl7ED2GHsOxwOx8AZ4hxwfrgYXDJu\nNa4Etw/XjLuA68MN4SbxeLwq3hTvgg/Bc/BifCG+Cn8cfx7fjx/GvyeQCVoE\na4IPIZYgJGwkVBAaCOcI/YQRwjRRgahPdCKGEHnEXGIpsY7YQbxJHCZOkxRJ\nhiQXUiQpmbSBVElqIl0mPSa9IZPJOmRHchhZQF5PriSfIF8lD5I/UJQoJhRP\nShxFQtlOOUq5QHlAeUOlUg2obtRYqpi6nVpPvUR9Sn0vR5Mzl/OX48mtk6uR\na5Xrl3slT5TXl3eXXy6fJ18hf0r+pvy4AlHBQMFTgaOwVqFG4bTCPYVJRZqi\nlWKIYppiiWKD4jXFUSW8koGStxJPqUDpsNIlpSEaQtOledK4tE20Otpl2jAd\nRzek+9OT6cX0H+i99AllJWVb5SjlHOUa5bPKUgbCMGD4M1IZpYyTjLuMj/M0\n5rnP48/bNq9pXv+8KZX5Km4qfJUilWaVAZWPqkxVb9UU1Z2qbapP1DBqJmph\natlq+9Uuq43Pp893ns+dXzT/5PyH6rC6iXq4+mr1w+o96pMamhq+GhkaVRqX\nNMY1GZpumsma5ZrnNMe0aFoLtQRa5VrntV4wlZnuzFRmJbOLOaGtru2nLdE+\npN2rPa1jqLNYZ6NOs84TXZIuWzdBt1y3U3dCT0svWC9fr1HvoT5Rn62fpL9H\nv1t/ysDQINpgi0GbwaihiqG/YZ5ho+FjI6qRq9Eqo1qjO8Y4Y7ZxivE+41sm\nsImdSZJJjclNU9jU3lRgus+0zwxr5mgmNKs1u8eisNxZWaxG1qA5wzzIfKN5\nm/krCz2LWIudFt0WXyztLFMt6ywfWSlZBVhttOqw+sPaxJprXWN9x4Zq42Oz\nzqbd5rWtqS3fdr/tfTuaXbDdFrtOu8/2DvYi+yb7MQc9h3iHvQ732HR2KLuE\nfdUR6+jhuM7xjOMHJ3snsdNJp9+dWc4pzg3OowsMF/AX1C0YctFx4bgccpEu\nZC6MX3hwodRV25XjWuv6zE3Xjed2xG3E3dg92f24+ysPSw+RR4vHlKeT5xrP\nC16Il69XkVevt5L3Yu9q76c+Oj6JPo0+E752vqt9L/hh/QL9dvrd89fw5/rX\n+08EOASsCegKpARGBFYHPgsyCRIFdQTDwQHBu4IfL9JfJFzUFgJC/EN2hTwJ\nNQxdFfpzGC4sNKwm7Hm4VXh+eHcELWJFREPEu0iPyNLIR4uNFksWd0bJR8VF\n1UdNRXtFl0VLl1gsWbPkRoxajCCmPRYfGxV7JHZyqffS3UuH4+ziCuPuLjNc\nlrPs2nK15anLz66QX8FZcSoeGx8d3xD/iRPCqeVMrvRfuXflBNeTu4f7kufG\nK+eN8V34ZfyRBJeEsoTRRJfEXYljSa5JFUnjAk9BteB1sl/ygeSplJCUoykz\nqdGpzWmEtPi000IlYYqwK10zPSe9L8M0ozBDuspp1e5VE6JA0ZFMKHNZZruY\njv5M9UiMJJslg1kLs2qy3mdHZZ/KUcwR5vTkmuRuyx3J88n7fjVmNXd1Z752\n/ob8wTXuaw6thdauXNu5Tnddwbrh9b7rj20gbUjZ8MtGy41lG99uit7UUaBR\nsL5gaLPv5sZCuUJR4b0tzlsObMVsFWzt3WazrWrblyJe0fViy+KK4k8l3JLr\n31l9V/ndzPaE7b2l9qX7d+B2CHfc3em681iZYlle2dCu4F2t5czyovK3u1fs\nvlZhW3FgD2mPZI+0MqiyvUqvakfVp+qk6oEaj5rmvep7t+2d2sfb17/fbX/T\nAY0DxQc+HhQcvH/I91BrrUFtxWHc4azDz+ui6rq/Z39ff0TtSPGRz0eFR6XH\nwo911TvU1zeoN5Q2wo2SxrHjccdv/eD1Q3sTq+lQM6O5+AQ4ITnx4sf4H++e\nDDzZeYp9qukn/Z/2ttBailqh1tzWibakNml7THvf6YDTnR3OHS0/m/989Iz2\nmZqzymdLz5HOFZybOZ93fvJCxoXxi4kXhzpXdD66tOTSna6wrt7LgZevXvG5\ncqnbvfv8VZerZ645XTt9nX297Yb9jdYeu56WX+x+aem172296XCz/ZbjrY6+\nBX3n+l37L972un3ljv+dGwOLBvruLr57/17cPel93v3RB6kPXj/Mejj9aP1j\n7OOiJwpPKp6qP6391fjXZqm99Oyg12DPs4hnj4a4Qy//lfmvT8MFz6nPK0a0\nRupHrUfPjPmM3Xqx9MXwy4yX0+OFvyn+tveV0auffnf7vWdiycTwa9HrmT9K\n3qi+OfrW9m3nZOjk03dp76anit6rvj/2gf2h+2P0x5Hp7E/4T5WfjT93fAn8\n8ngmbWbm3/eE8/sKZW5kc3RyZWFtCmVuZG9iago5IDAgb2JqCjI2MTIKZW5k\nb2JqCjcgMCBvYmoKWyAvSUNDQmFzZWQgOCAwIFIgXQplbmRvYmoKMyAwIG9i\nago8PCAvVHlwZSAvUGFnZXMgL01lZGlhQm94IFswIDAgNTk1LjI4IDg0MS44\nOV0gL0NvdW50IDEgL0tpZHMgWyAyIDAgUiBdID4+CmVuZG9iagoxMCAwIG9i\nago8PCAvVHlwZSAvQ2F0YWxvZyAvUGFnZXMgMyAwIFIgPj4KZW5kb2JqCjEx\nIDAgb2JqCihibGFua1BERikKZW5kb2JqCjEyIDAgb2JqCij+/1wwMDBtXDAw\nMGFcMDAwY1wwMDBPXDAwMFNcMDAwIFwwMDBWXDAwMGVcMDAwclwwMDBzXDAw\nMONcMDAwb1wwMDAgXDAwMDFcMDAwMFwwMDAuXDAwMDFcMDAwNFwwMDAuXDAw\nMDNcMDAwIFwwMDBcKFwwMDBGXDAwMGFcMDAwc1wwMDBlXDAwMCBcMDAwMVww\nMDA4XDAwMERcMDAwMVwwMDAwXDAwMDlcMDAwXClcMDAwIFwwMDBRXDAwMHVc\nMDAwYVwwMDByXDAwMHRcMDAwelwwMDAgXDAwMFBcMDAwRFwwMDBGXDAwMENc\nMDAwb1wwMDBuXDAwMHRcMDAwZVwwMDB4XDAwMHQpCmVuZG9iagoxMyAwIG9i\nagooUGFnZXMpCmVuZG9iagoxNCAwIG9iagooRDoyMDE5MDMxMTE5MzgwOVow\nMCcwMCcpCmVuZG9iagoxIDAgb2JqCjw8IC9UaXRsZSAxMSAwIFIgL1Byb2R1\nY2VyIDEyIDAgUiAvQ3JlYXRvciAxMyAwIFIgL0NyZWF0aW9uRGF0ZSAxNCAw\nIFIgL01vZERhdGUKMTQgMCBSID4+CmVuZG9iagp4cmVmCjAgMTUKMDAwMDAw\nMDAwMCA2NTUzNSBmIAowMDAwMDAzNjU5IDAwMDAwIG4gCjAwMDAwMDAxOTgg\nMDAwMDAgbiAKMDAwMDAwMzE0NCAwMDAwMCBuIAowMDAwMDAwMDIyIDAwMDAw\nIG4gCjAwMDAwMDAxODAgMDAwMDAgbiAKMDAwMDAwMDMwOCAwMDAwMCBuIAow\nMDAwMDAzMTA5IDAwMDAwIG4gCjAwMDAwMDAzNzYgMDAwMDAgbiAKMDAwMDAw\nMzA4OSAwMDAwMCBuIAowMDAwMDAzMjMzIDAwMDAwIG4gCjAwMDAwMDMyODMg\nMDAwMDAgbiAKMDAwMDAwMzMxMCAwMDAwMCBuIAowMDAwMDAzNTkzIDAwMDAw\nIG4gCjAwMDAwMDM2MTcgMDAwMDAgbiAKdHJhaWxlcgo8PCAvU2l6ZSAxNSAv\nUm9vdCAxMCAwIFIgL0luZm8gMSAwIFIgL0lEIFsgPDM4NzkzYjhlZmU0YTBj\nZDY2MTUxNzUyOTM4YzM4YTg4Pgo8Mzg3OTNiOGVmZTRhMGNkNjYxNTE3NTI5\nMzhjMzhhODg+IF0gPj4Kc3RhcnR4cmVmCjM3NjQKJSVFT0YK\n",
          "cliente": {
            "cpf_cnpj": "46728754000163",
              "email": "teste@nexaas.com.br",
              "indicador_inscricao_estadual": 1,
              "inscricao_estadual": "407056228113",
              "inscricao_municipal": "",
              "inscricao_suframa": "",
              "nome": "NF-E EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
              "pessoa_fisica_juridica": "company",
              "endereco": {
                "bairro": "MEDEIROS",
                "cep": "13212255",
                "codigo_municipio": "3525904",
                "codigo_pais": "1058",
                "complemento": "",
                "logradouro": "AV GUILHERME PORCARI",
                "nome_municipio": "JUNDIAI",
                "nome_pais": "BRASIL",
                "numero": "S N",
                "telefone": "99999999",
                "uf": "SP"
              }
          },
            "cobranca": {
              "duplicatas": [
              {
                "data_vencimento": "",
                "numero": "",
                "valor": ""
              }
              ],
              "fatura": {
                "numero_fatura": "",
                "valor_desconto": 0,
                "valor_liquido": 0,
                "valor_original": 0
              }
            },
            "dados_gerais": {
              "codigo_mun_ocorrencia": "3525904",
              "data_saida_entrada": "2018-09-28T17:07:35-03:00",
              "destino_operacao": "1",
              "finalidade_nfe": "1",
              "serie": 1"
                "indicador_consumidor_final": "0",
              "indicador_presenca": "9",
              "natureza_operacao": "Venda merc. adq. rec. terc. efet. fora estab.",
              "tipo_operacao": "1",
              "uf": 35
            },
            "forma_de_pagamento": [
            {
              "tipo_de_pagamento": "01",
              "valor_do_pagamento": 50
            },
            {
              "tipo_de_integracao": "2",
              "tipo_de_pagamento": "03",
              "valor_do_pagamento": 8.97
            },
            {
              "bandeira_operadora": "02",
              "cnpj_credenciadora": "99999999999999",
              "numero_autorizacao_operacao": "99999999999999999999",
              "tipo_de_integracao": "1",
              "tipo_de_pagamento": "03",
              "valor_do_pagamento": 40
            }
            ],
            "informacoes_adicionais": {
              "informacoes_contribuinte": "",
              "informacoes_fisco": "Cliente: 112. Remessa: 000061074-0123"
            },
            "lista_autorizacao": [],
            "produtos": [
            {
              "cest": "",
              "cfop": 5104,
              "cnpj_fabricante_mercadoria": "99999999999999999",
              "codigo_beneficio_fiscal": "foo",
              "codigo_ean": "",
              "codigo_produto": "123456",
              "descricao": "NITROGENIO CIL 50L 10M3",
              "ean_unidade_trib": "",
              "informacoes_adicionais": "",
              "ncm": 28043000,
              "num_item_pedido": 1,
              "num_pedido": "S0100249134",
              "outras_despesas": 0,
              "producao_escala": "S",
              "quantidade_comercial": 6,
              "quantidade_tributaria": 6,
              "unidade_comercial": "M3",
              "unidade_tributaria": "M3",
              "valor_desconto": 0,
              "valor_frete": 0,
              "valor_seguro": 0,
              "valor_total_produto": "98.97",
              "valor_unitario_comercial": 16.49485,
              "valor_unitario_tributario": 16.49485,
              "tributacao": {
                "valor_aproximado_total": 269.64,
                "cofins": {
                  "aliquota_cofins": "7.60",
                  "aliquota_cofins_reais": 0,
                  "aliquota_cofins_st_reais": 0,
                  "aliquota_st": 0,
                  "situacao_tributaria": "01",
                  "valor_base_calculo": 989.69,
                  "valor_base_calculo_st": 0,
                  "valor_cofins": 75.2,
                  "valor_cofins_st": 0
                },
                "icms": {
                  "aliquota_consumidor_final": 0,
                  "aliquota_fcp": 0,
                  "aliquota_fcp_st": 0,
                  "aliquota_fcp_st_retido": 0,
                  "aliquota_icms": "18.00",
                  "aliquota_icms_simples_nacional": 0,
                  "aliquota_icms_st": 0,
                  "aliquota_interestadual": 0,
                  "aliquota_interna_interestadual": 0,
                  "base_icmsst_retido": 0,
                  "codigo_origem_produto": 3,
                  "credito_icms_simples_nacional": 0,
                  "modalidade_base_calculo": 3,
                  "modalidade_base_calculo_st": "3",
                  "motivo_desoneracao": "",
                  "perc_diferimento": 0,
                  "perc_fcp_interestadual": 0,
                  "perc_mva_icms_st": 0,
                  "perc_provisorio_interestadual": 0,
                  "perc_reducao_base_calculo": 0,
                  "perc_reducao_base_calculo_st": 0,
                  "situacao_simples_nacional": 0,
                  "situacao_tributaria": "00",
                  "valor_base_calculo": 989.69,
                  "valor_base_calculo_fcp": 0,
                  "valor_base_calculo_fcp_st": 0,
                  "valor_base_calculo_fcp_st_retido": 0,
                  "valor_base_calculo_st": 0,
                  "valor_base_calculo_uf_dest": 0,
                  "valor_fcp": 0,
                  "valor_fcp_interestadual": 0,
                  "valor_fcp_st": 0,
                  "valor_fcp_st_retido": 0,
                  "valor_icms": 178.14,
                  "valor_icms_desonerado": 0,
                  "valor_icms_diferido": 0,
                  "valor_icms_operacao": 0,
                  "valor_icms_st": 0,
                  "valor_icmsst_retido": 0,
                  "valor_uf_destinatario_interestadual": 0,
                  "valor_uf_rementente": 0,
                  "valor_uf_remetente_interestadual": 0
                },
                "importacao": {
                  "base_calculo_importacao": "",
                  "valor_despesas_aduaneiras": "",
                  "valor_imposto_importacao": "",
                  "valor_iof": ""
                },
                "ipi": {
                  "aliquota_ipi": "0.00",
                  "cnpj_produtor": "",
                  "codigo_enquadramento": 999,
                  "codigo_selo_controle": 0,
                  "quantidade_selo_controle": 0,
                  "situacao_tributaria": "01",
                  "valor_base_calculo": "989.69",
                  "valor_ipi": "0.00",
                  "valor_unidade": ""
                },
                "pis": {
                  "aliquota_pis": 1.65,
                  "aliquota_pis_reais": 0,
                  "aliquota_pis_reais_st": 0,
                  "aliquota_st": 0,
                  "situacao_tributaria": "01",
                  "valor_base_calculo": 989.69,
                  "valor_base_calculo_st": 0,
                  "valor_pis": 16.3,
                  "valor_pis_st": 0
                }
              },
              "declaracao_importacao": [
              {
                "cnpj": "",
                "codigo_exportador": "",
                "data_desembaraco": "",
                "data_importacao": "",
                "documento_importacao": "",
                "forma_importacao": "",
                "local_desembaraco": "",
                "uf_adquirente": "",
                "uf_desembaraco": "",
                "valor_afrmm": "",
                "via_transporte": "",
                "adicoes": [
                {
                  "codigo_fabricante": "",
                  "numero_adicao": "",
                  "numero_drawback": "",
                  "numero_sequencial": "",
                  "valor_desconto": ""
                }
                ]
              }
              ]
            }
            ],
            "retencao_tributos": {
              "base_calculo_retencao_previdencia": 0,
              "valor_base_calculo_irrf": 0,
              "valor_irrf": 0,
              "valor_retencao_previdencia": 0,
              "valor_retido_cofins": 0,
              "valor_retido_csll": 0,
              "valor_retido_pis": 0
            },
            "transporte": {
              "codigo_modalidade": 9,
              "retencao_icms": {
                "aliquota_retencao": 0,
                "cfop": "",
                "codigo_municipio": "",
                "uf": "",
                "valor_base_calculo": 0,
                "valor_retido": 0,
                "valor_servico": 0
              },
              "transportadora": {
                "cnpj_cpf": "",
                "endereco_completo": "",
                "inscricao_estadual": "",
                "municipio": "",
                "razao_social": "",
                "uf": ""
              },
              "veiculo": {
                "placa": "",
                "rntc": "",
                "uf": ""
              },
              "volume_transportado": [
              {
                "especie": "Cilindro",
                "marca": 0,
                "numeracao_volumes": 0,
                "peso_bruto": "450.780",
                "peso_liquido": "66.780",
                "quantidade_volumes": 1
              }
              ]
            }
        }
}'


EXEMPLO DE RESPOSTA

{
  "cfe": {
    "id": 10990,
    "status": "processing",
    "data":  {...}
  }
}
```
