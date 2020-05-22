# Cálculo Tributário

Para calcular os tributos de um documento fiscal (NFe e NFCe), é necessário realizar uma requisição POST para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">POST</i>
        <h6>/api/v1/organizations/{organization_id}/tax_calculator</h6>
    </div>
</div>

<aside class="notice">
  A estrutura JSON será a mesma que a emissão em lote para NFe e NFCe
</aside>

## Exemplo NFe

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/tax_calculator \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json' \
  -d '{
    "nfe_batch": {
        "lote": 1,
        "serie": 22,
        "engine_de_calculo": "nexaas",
        "sincronicidade": 0,
        "uf": 53,
        "nfes": [
            {
                "cliente": {
                    "cpf_cnpj": "01716006000122",
                    "email": "teste@nexaas.com.br",
                    "indicador_inscricao_estadual": 1,
                    "inscricao_estadual": "0736913700156",
                    "inscricao_municipal": "",
                    "inscricao_suframa": "",
                    "nome": "NF-E EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                    "pessoa_fisica_juridica": "company",
                    "endereco": {
                        "bairro": "Bairro teste",
                        "cep": "05685040",
                        "codigo_municipio": "5300108",
                        "codigo_pais": "1058",
                        "complemento": "",
                        "logradouro": "Rua do Consultor",
                        "nome_municipio": "BRASILIA",
                        "nome_pais": "BRASIL",
                        "numero": "14",
                        "telefone": "99999999",
                        "uf": "DF"
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
                    "codigo_mun_ocorrencia": "5300108",
                    "destino_operacao": "1",
                    "finalidade_nfe": "1",
                    "indicador_consumidor_final": "0",
                    "indicador_presenca": "9",
                    "natureza_operacao": "Venda merc. adq. rec. terc. efet. fora estab.",
                    "tipo_operacao": "1",
                    "uf": 53,
                    "codigo_natureza_operacao": "002"
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
                            "icms": {
                                "codigo_origem_produto": 2
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
            },
            {
                "cliente": {
                    "cpf_cnpj": "01716006000122",
                    "email": "teste@nexaas.com.br",
                    "indicador_inscricao_estadual": 1,
                    "inscricao_estadual": "0736913700156",
                    "inscricao_municipal": "",
                    "inscricao_suframa": "",
                    "nome": "NF-E EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                    "pessoa_fisica_juridica": "company",
                    "endereco": {
                        "bairro": "Bairro teste",
                        "cep": "05685040",
                        "codigo_municipio": "5300108",
                        "codigo_pais": "1058",
                        "complemento": "",
                        "logradouro": "Rua do Consultor",
                        "nome_municipio": "BRASILIA",
                        "nome_pais": "BRASIL",
                        "numero": "14",
                        "telefone": "99999999",
                        "uf": "DF"
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
                    "codigo_mun_ocorrencia": "5300108",
                    "destino_operacao": "1",
                    "finalidade_nfe": "1",
                    "indicador_consumidor_final": "0",
                    "indicador_presenca": "9",
                    "natureza_operacao": "Venda merc. adq. rec. terc. efet. fora estab.",
                    "tipo_operacao": "1",
                    "uf": 53,
                    "codigo_natureza_operacao": "002"
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
                            "icms": {
                                "codigo_origem_produto": 2
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
            },
            {
                "cliente": {
                    "cpf_cnpj": "01716006000122",
                    "email": "teste@nexaas.com.br",
                    "indicador_inscricao_estadual": 1,
                    "inscricao_estadual": "0736913700156",
                    "inscricao_municipal": "",
                    "inscricao_suframa": "",
                    "nome": "NF-E EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                    "pessoa_fisica_juridica": "company",
                    "endereco": {
                        "bairro": "Bairro teste",
                        "cep": "05685040",
                        "codigo_municipio": "5300108",
                        "codigo_pais": "1058",
                        "complemento": "",
                        "logradouro": "Rua do Consultor",
                        "nome_municipio": "BRASILIA",
                        "nome_pais": "BRASIL",
                        "numero": "14",
                        "telefone": "99999999",
                        "uf": "DF"
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
                    "codigo_mun_ocorrencia": "5300108",
                    "destino_operacao": "1",
                    "finalidade_nfe": "1",
                    "indicador_consumidor_final": "0",
                    "indicador_presenca": "9",
                    "natureza_operacao": "Venda merc. adq. rec. terc. efet. fora estab.",
                    "tipo_operacao": "1",
                    "uf": 53,
                    "codigo_natureza_operacao": "002"
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
                        "descricao": "OXIGENIO CIL 50L 10M3",
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
                            "icms": {
                                "codigo_origem_produto": 2
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
        ]
    }
}
}'


EXEMPLO DE RESPOSTA
{
    "nfe_batch": {
        "lote": 1,
        "serie": 22,
        "engine_de_calculo": "nexaas",
        "sincronicidade": 0,
        "uf": 53,
        "nfes": [
            {
                "dados_gerais": {
                    "uf": "53",
                    "serie": 22,
                    "codigo_mun_ocorrencia": "5300108",
                    "natureza_operacao": "Venda merc. adq. rec. terc. efet. fora estab.",
                    "codigo_natureza_operacao": "002",
                    "tipo_operacao": "1",
                    "indicador_consumidor_final": "0",
                    "destino_operacao": "1",
                    "finalidade_nfe": "1",
                    "indicador_presenca": "9"
                },
                "emitente": {
                    "cnpj": "22769530000131",
                    "razao_social": "Organizacao Teste NFCe / DF",
                    "nome_fantasia": "Organizacao Teste NFCe / DF",
                    "inscricao_estadual": "772733700120",
                    "codigo_regime_tributario": 3,
                    "regime_tributario_diferenciado": "ISENLF",
                    "endereco": {
                        "bairro": "Asa Sul",
                        "cep": "70070938",
                        "logradouro": "SAUS Quadra 4 Lote 9/10",
                        "nome_pais": "Brasil",
                        "nome_municipio": "Brasilia",
                        "numero": "04",
                        "codigo_municipio": "5300108",
                        "codigo_pais": "1058",
                        "uf": "DF"
                    }
                },
                "cliente": {
                    "cpf_cnpj": "01716006000122",
                    "email": "teste@nexaas.com.br",
                    "inscricao_estadual": "0736913700156",
                    "nome": "NF-E EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                    "pessoa_fisica_juridica": "company",
                    "indicador_inscricao_estadual": "1",
                    "endereco": {
                        "bairro": "Bairro teste",
                        "cep": "05685040",
                        "logradouro": "Rua do Consultor",
                        "nome_pais": "BRASIL",
                        "nome_municipio": "BRASILIA",
                        "numero": "14",
                        "codigo_municipio": "5300108",
                        "codigo_pais": "1058",
                        "telefone": "99999999",
                        "uf": "DF"
                    }
                },
                "retirada": {
                    "endereco": {
                        "nome_pais": "Brasil",
                        "codigo_pais": "1058"
                    }
                },
                "entrega": {
                    "endereco": {
                        "nome_pais": "Brasil",
                        "codigo_pais": "1058"
                    }
                },
                "produtos": [
                    {
                        "codigo_produto": "123456",
                        "codigo_ean": "SEM GTIN",
                        "descricao": "NITROGENIO CIL 50L 10M3",
                        "ncm": "28043000",
                        "cfop": "5102",
                        "unidade_comercial": "M3",
                        "ean_unidade_trib": "SEM GTIN",
                        "unidade_tributaria": "M3",
                        "num_pedido": "S0100249134",
                        "num_item_pedido": "1",
                        "producao_escala": "S",
                        "cnpj_fabricante_mercadoria": "99999999999999999",
                        "codigo_beneficio_fiscal": "foo",
                        "quantidade_comercial": 6,
                        "valor_unitario_comercial": 16.49485,
                        "quantidade_tributaria": 6,
                        "valor_unitario_tributario": 16.49485,
                        "valor_frete": 0,
                        "valor_seguro": 0,
                        "valor_desconto": 0,
                        "valor_total_produto": 98.97,
                        "outras_despesas": 0,
                        "tributacao": {
                            "icms": {
                                "aliquota_consumidor_final": 0,
                                "aliquota_icms": 17,
                                "aliquota_icms_simples_nacional": 0,
                                "aliquota_icms_st": 0,
                                "aliquota_interestadual": "12",
                                "aliquota_interna_interestadual": "0.0000",
                                "base_icmsst_retido": 0,
                                "codigo_origem_produto": 2,
                                "credito_icms_simples_nacional": 0,
                                "modalidade_base_calculo": "3",
                                "perc_diferimento": 0,
                                "perc_fcp_interestadual": "0.0000",
                                "perc_mva_icms_st": 0,
                                "perc_provisorio_interestadual": "100",
                                "perc_reducao_base_calculo": 0,
                                "perc_reducao_base_calculo_st": 0,
                                "situacao_tributaria": "00",
                                "valor_base_calculo": 98.97,
                                "valor_base_calculo_st": 0,
                                "valor_icms": 16.82,
                                "valor_icms_desonerado": 0,
                                "valor_icms_diferido": 0,
                                "valor_icms_operacao": 0,
                                "valor_icms_st": 0,
                                "valor_icmsst_retido": 0
                            },
                            "pis": {
                                "aliquota_st": 0,
                                "valor_base_calculo": 98.97,
                                "valor_base_calculo_st": 0,
                                "situacao_tributaria": "49",
                                "aliquota_pis": 3,
                                "aliquota_pis_reais": 0,
                                "aliquota_pis_reais_st": 0,
                                "valor_pis": 2.97,
                                "valor_pis_st": 0
                            },
                            "cofins": {
                                "aliquota_st": 0,
                                "valor_base_calculo": 98.97,
                                "valor_base_calculo_st": 0,
                                "situacao_tributaria": "49",
                                "aliquota_cofins": 4,
                                "aliquota_cofins_reais": 0,
                                "aliquota_cofins_reais_st": 0,
                                "valor_cofins": 3.96,
                                "valor_cofins_st": 0
                            }
                        }
                    }
                ],
                "transporte": {
                    "codigo_modalidade": 9,
                    "retencao_icms": {
                        "valor_servico": 0,
                        "valor_base_calculo": 0,
                        "aliquota_retencao": 0,
                        "valor_retido": 0
                    },
                    "volume_transportado": [
                        {
                            "numeracao_volumes": "0",
                            "marca": "0",
                            "especie": "Cilindro",
                            "quantidade_volumes": 1,
                            "peso_liquido": 66.78,
                            "peso_bruto": 450.78
                        }
                    ]
                },
                "cobranca": {
                    "fatura": {
                        "valor_original": 0,
                        "valor_desconto": 0,
                        "valor_liquido": 0
                    }
                },
                "forma_de_pagamento": [
                    {
                        "tipo_de_pagamento": "01",
                        "valor_do_pagamento": 50
                    },
                    {
                        "tipo_de_pagamento": "03",
                        "valor_do_pagamento": 8.97,
                        "tipo_de_integracao": 2
                    },
                    {
                        "tipo_de_pagamento": "03",
                        "valor_do_pagamento": 40,
                        "tipo_de_integracao": 1,
                        "cnpj_credenciadora": "99999999999999",
                        "bandeira_operadora": "02",
                        "numero_autorizacao_operacao": "99999999999999999999"
                    }
                ],
                "informacoes_adicionais": {
                    "informacoes_fisco": "Cliente: 112. Remessa: 000061074-0123"
                },
                "retencao_tributos": {
                    "valor_retido_pis": 0,
                    "valor_retido_cofins": 0,
                    "valor_retido_csll": 0,
                    "valor_base_calculo_irrf": 0,
                    "valor_irrf": 0,
                    "base_calculo_retencao_previdencia": 0,
                    "valor_retencao_previdencia": 0
                }
            },
            {
                "dados_gerais": {
                    "uf": "53",
                    "serie": 22,
                    "codigo_mun_ocorrencia": "5300108",
                    "natureza_operacao": "Venda merc. adq. rec. terc. efet. fora estab.",
                    "codigo_natureza_operacao": "002",
                    "tipo_operacao": "1",
                    "indicador_consumidor_final": "0",
                    "destino_operacao": "1",
                    "finalidade_nfe": "1",
                    "indicador_presenca": "9"
                },
                "emitente": {
                    "cnpj": "22769530000131",
                    "razao_social": "Organizacao Teste NFCe / DF",
                    "nome_fantasia": "Organizacao Teste NFCe / DF",
                    "inscricao_estadual": "772733700120",
                    "codigo_regime_tributario": 3,
                    "regime_tributario_diferenciado": "ISENLF",
                    "endereco": {
                        "bairro": "Asa Sul",
                        "cep": "70070938",
                        "logradouro": "SAUS Quadra 4 Lote 9/10",
                        "nome_pais": "Brasil",
                        "nome_municipio": "Brasilia",
                        "numero": "04",
                        "codigo_municipio": "5300108",
                        "codigo_pais": "1058",
                        "uf": "DF"
                    }
                },
                "cliente": {
                    "cpf_cnpj": "01716006000122",
                    "email": "teste@nexaas.com.br",
                    "inscricao_estadual": "0736913700156",
                    "nome": "NF-E EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                    "pessoa_fisica_juridica": "company",
                    "indicador_inscricao_estadual": "1",
                    "endereco": {
                        "bairro": "Bairro teste",
                        "cep": "05685040",
                        "logradouro": "Rua do Consultor",
                        "nome_pais": "BRASIL",
                        "nome_municipio": "BRASILIA",
                        "numero": "14",
                        "codigo_municipio": "5300108",
                        "codigo_pais": "1058",
                        "telefone": "99999999",
                        "uf": "DF"
                    }
                },
                "retirada": {
                    "endereco": {
                        "nome_pais": "Brasil",
                        "codigo_pais": "1058"
                    }
                },
                "entrega": {
                    "endereco": {
                        "nome_pais": "Brasil",
                        "codigo_pais": "1058"
                    }
                },
                "produtos": [
                    {
                        "codigo_produto": "123456",
                        "codigo_ean": "SEM GTIN",
                        "descricao": "NITROGENIO CIL 50L 10M3",
                        "ncm": "28043000",
                        "cfop": "5102",
                        "unidade_comercial": "M3",
                        "ean_unidade_trib": "SEM GTIN",
                        "unidade_tributaria": "M3",
                        "num_pedido": "S0100249134",
                        "num_item_pedido": "1",
                        "producao_escala": "S",
                        "cnpj_fabricante_mercadoria": "99999999999999999",
                        "codigo_beneficio_fiscal": "foo",
                        "quantidade_comercial": 6,
                        "valor_unitario_comercial": 16.49485,
                        "quantidade_tributaria": 6,
                        "valor_unitario_tributario": 16.49485,
                        "valor_frete": 0,
                        "valor_seguro": 0,
                        "valor_desconto": 0,
                        "valor_total_produto": 98.97,
                        "outras_despesas": 0,
                        "tributacao": {
                            "icms": {
                                "aliquota_consumidor_final": 0,
                                "aliquota_icms": 17,
                                "aliquota_icms_simples_nacional": 0,
                                "aliquota_icms_st": 0,
                                "aliquota_interestadual": "12",
                                "aliquota_interna_interestadual": "0.0000",
                                "base_icmsst_retido": 0,
                                "codigo_origem_produto": 2,
                                "credito_icms_simples_nacional": 0,
                                "modalidade_base_calculo": "3",
                                "perc_diferimento": 0,
                                "perc_fcp_interestadual": "0.0000",
                                "perc_mva_icms_st": 0,
                                "perc_provisorio_interestadual": "100",
                                "perc_reducao_base_calculo": 0,
                                "perc_reducao_base_calculo_st": 0,
                                "situacao_tributaria": "00",
                                "valor_base_calculo": 98.97,
                                "valor_base_calculo_st": 0,
                                "valor_icms": 16.82,
                                "valor_icms_desonerado": 0,
                                "valor_icms_diferido": 0,
                                "valor_icms_operacao": 0,
                                "valor_icms_st": 0,
                                "valor_icmsst_retido": 0
                            },
                            "pis": {
                                "aliquota_st": 0,
                                "valor_base_calculo": 98.97,
                                "valor_base_calculo_st": 0,
                                "situacao_tributaria": "49",
                                "aliquota_pis": 3,
                                "aliquota_pis_reais": 0,
                                "aliquota_pis_reais_st": 0,
                                "valor_pis": 2.97,
                                "valor_pis_st": 0
                            },
                            "cofins": {
                                "aliquota_st": 0,
                                "valor_base_calculo": 98.97,
                                "valor_base_calculo_st": 0,
                                "situacao_tributaria": "49",
                                "aliquota_cofins": 4,
                                "aliquota_cofins_reais": 0,
                                "aliquota_cofins_reais_st": 0,
                                "valor_cofins": 3.96,
                                "valor_cofins_st": 0
                            }
                        }
                    }
                ],
                "transporte": {
                    "codigo_modalidade": 9,
                    "retencao_icms": {
                        "valor_servico": 0,
                        "valor_base_calculo": 0,
                        "aliquota_retencao": 0,
                        "valor_retido": 0
                    },
                    "volume_transportado": [
                        {
                            "numeracao_volumes": "0",
                            "marca": "0",
                            "especie": "Cilindro",
                            "quantidade_volumes": 1,
                            "peso_liquido": 66.78,
                            "peso_bruto": 450.78
                        }
                    ]
                },
                "cobranca": {
                    "fatura": {
                        "valor_original": 0,
                        "valor_desconto": 0,
                        "valor_liquido": 0
                    }
                },
                "forma_de_pagamento": [
                    {
                        "tipo_de_pagamento": "01",
                        "valor_do_pagamento": 50
                    },
                    {
                        "tipo_de_pagamento": "03",
                        "valor_do_pagamento": 8.97,
                        "tipo_de_integracao": 2
                    },
                    {
                        "tipo_de_pagamento": "03",
                        "valor_do_pagamento": 40,
                        "tipo_de_integracao": 1,
                        "cnpj_credenciadora": "99999999999999",
                        "bandeira_operadora": "02",
                        "numero_autorizacao_operacao": "99999999999999999999"
                    }
                ],
                "informacoes_adicionais": {
                    "informacoes_fisco": "Cliente: 112. Remessa: 000061074-0123"
                },
                "retencao_tributos": {
                    "valor_retido_pis": 0,
                    "valor_retido_cofins": 0,
                    "valor_retido_csll": 0,
                    "valor_base_calculo_irrf": 0,
                    "valor_irrf": 0,
                    "base_calculo_retencao_previdencia": 0,
                    "valor_retencao_previdencia": 0
                }
            },
            {
                "dados_gerais": {
                    "uf": "53",
                    "serie": 22,
                    "codigo_mun_ocorrencia": "5300108",
                    "natureza_operacao": "Venda merc. adq. rec. terc. efet. fora estab.",
                    "codigo_natureza_operacao": "002",
                    "tipo_operacao": "1",
                    "indicador_consumidor_final": "0",
                    "destino_operacao": "1",
                    "finalidade_nfe": "1",
                    "indicador_presenca": "9"
                },
                "emitente": {
                    "cnpj": "22769530000131",
                    "razao_social": "Organizacao Teste NFCe / DF",
                    "nome_fantasia": "Organizacao Teste NFCe / DF",
                    "inscricao_estadual": "772733700120",
                    "codigo_regime_tributario": 3,
                    "regime_tributario_diferenciado": "ISENLF",
                    "endereco": {
                        "bairro": "Asa Sul",
                        "cep": "70070938",
                        "logradouro": "SAUS Quadra 4 Lote 9/10",
                        "nome_pais": "Brasil",
                        "nome_municipio": "Brasilia",
                        "numero": "04",
                        "codigo_municipio": "5300108",
                        "codigo_pais": "1058",
                        "uf": "DF"
                    }
                },
                "cliente": {
                    "cpf_cnpj": "01716006000122",
                    "email": "teste@nexaas.com.br",
                    "inscricao_estadual": "0736913700156",
                    "nome": "NF-E EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                    "pessoa_fisica_juridica": "company",
                    "indicador_inscricao_estadual": "1",
                    "endereco": {
                        "bairro": "Bairro teste",
                        "cep": "05685040",
                        "logradouro": "Rua do Consultor",
                        "nome_pais": "BRASIL",
                        "nome_municipio": "BRASILIA",
                        "numero": "14",
                        "codigo_municipio": "5300108",
                        "codigo_pais": "1058",
                        "telefone": "99999999",
                        "uf": "DF"
                    }
                },
                "retirada": {
                    "endereco": {
                        "nome_pais": "Brasil",
                        "codigo_pais": "1058"
                    }
                },
                "entrega": {
                    "endereco": {
                        "nome_pais": "Brasil",
                        "codigo_pais": "1058"
                    }
                },
                "produtos": [
                    {
                        "codigo_produto": "123456",
                        "codigo_ean": "SEM GTIN",
                        "descricao": "OXIGENIO CIL 50L 10M3",
                        "ncm": "28043000",
                        "cfop": "5102",
                        "unidade_comercial": "M3",
                        "ean_unidade_trib": "SEM GTIN",
                        "unidade_tributaria": "M3",
                        "num_pedido": "S0100249134",
                        "num_item_pedido": "1",
                        "producao_escala": "S",
                        "cnpj_fabricante_mercadoria": "99999999999999999",
                        "codigo_beneficio_fiscal": "foo",
                        "quantidade_comercial": 6,
                        "valor_unitario_comercial": 16.49485,
                        "quantidade_tributaria": 6,
                        "valor_unitario_tributario": 16.49485,
                        "valor_frete": 0,
                        "valor_seguro": 0,
                        "valor_desconto": 0,
                        "valor_total_produto": 98.97,
                        "outras_despesas": 0,
                        "tributacao": {
                            "icms": {
                                "aliquota_consumidor_final": 0,
                                "aliquota_icms": 17,
                                "aliquota_icms_simples_nacional": 0,
                                "aliquota_icms_st": 0,
                                "aliquota_interestadual": "12",
                                "aliquota_interna_interestadual": "0.0000",
                                "base_icmsst_retido": 0,
                                "codigo_origem_produto": 2,
                                "credito_icms_simples_nacional": 0,
                                "modalidade_base_calculo": "3",
                                "perc_diferimento": 0,
                                "perc_fcp_interestadual": "0.0000",
                                "perc_mva_icms_st": 0,
                                "perc_provisorio_interestadual": "100",
                                "perc_reducao_base_calculo": 0,
                                "perc_reducao_base_calculo_st": 0,
                                "situacao_tributaria": "00",
                                "valor_base_calculo": 98.97,
                                "valor_base_calculo_st": 0,
                                "valor_icms": 16.82,
                                "valor_icms_desonerado": 0,
                                "valor_icms_diferido": 0,
                                "valor_icms_operacao": 0,
                                "valor_icms_st": 0,
                                "valor_icmsst_retido": 0
                            },
                            "pis": {
                                "aliquota_st": 0,
                                "valor_base_calculo": 98.97,
                                "valor_base_calculo_st": 0,
                                "situacao_tributaria": "49",
                                "aliquota_pis": 3,
                                "aliquota_pis_reais": 0,
                                "aliquota_pis_reais_st": 0,
                                "valor_pis": 2.97,
                                "valor_pis_st": 0
                            },
                            "cofins": {
                                "aliquota_st": 0,
                                "valor_base_calculo": 98.97,
                                "valor_base_calculo_st": 0,
                                "situacao_tributaria": "49",
                                "aliquota_cofins": 4,
                                "aliquota_cofins_reais": 0,
                                "aliquota_cofins_reais_st": 0,
                                "valor_cofins": 3.96,
                                "valor_cofins_st": 0
                            }
                        }
                    }
                ],
                "transporte": {
                    "codigo_modalidade": 9,
                    "retencao_icms": {
                        "valor_servico": 0,
                        "valor_base_calculo": 0,
                        "aliquota_retencao": 0,
                        "valor_retido": 0
                    },
                    "volume_transportado": [
                        {
                            "numeracao_volumes": "0",
                            "marca": "0",
                            "especie": "Cilindro",
                            "quantidade_volumes": 1,
                            "peso_liquido": 66.78,
                            "peso_bruto": 450.78
                        }
                    ]
                },
                "cobranca": {
                    "fatura": {
                        "valor_original": 0,
                        "valor_desconto": 0,
                        "valor_liquido": 0
                    }
                },
                "forma_de_pagamento": [
                    {
                        "tipo_de_pagamento": "01",
                        "valor_do_pagamento": 50
                    },
                    {
                        "tipo_de_pagamento": "03",
                        "valor_do_pagamento": 8.97,
                        "tipo_de_integracao": 2
                    },
                    {
                        "tipo_de_pagamento": "03",
                        "valor_do_pagamento": 40,
                        "tipo_de_integracao": 1,
                        "cnpj_credenciadora": "99999999999999",
                        "bandeira_operadora": "02",
                        "numero_autorizacao_operacao": "99999999999999999999"
                    }
                ],
                "informacoes_adicionais": {
                    "informacoes_fisco": "Cliente: 112. Remessa: 000061074-0123"
                },
                "retencao_tributos": {
                    "valor_retido_pis": 0,
                    "valor_retido_cofins": 0,
                    "valor_retido_csll": 0,
                    "valor_base_calculo_irrf": 0,
                    "valor_irrf": 0,
                    "base_calculo_retencao_previdencia": 0,
                    "valor_retencao_previdencia": 0
                }
            }
        ]
    }
}

```

## Exemplo NFCe

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  https://app.production.emites.com.br/api/v1/organizations/11/tax_calculator \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json' \
  -d '{
    "nfce_batch": {
        "lote": "1",
        "serie": "233",
        "engine_de_calculo": "nexaas",
        "sincronicidade": "0",
        "uf": "53",
        "nfces": [
            {
                "dados_gerais": {
                    "csc": "000002",
                    "id_token": "A16A5A2DD8FA443FB8710D9AB8EB5432",
                    "codigo_mun_ocorrencia": "5300108",
                    "destino_operacao": 1,
                    "finalidade_nfe": "1",
                    "indicador_presenca": "1",
                    "natureza_operacao": "saida",
                    "codigo_natureza_operacao": "002",
                    "tipo_operacao": "1",
                    "uf": "53"
                },
                "cliente": {
                    "pessoa_fisica_juridica": "person",
                    "cpf_cnpj": "86152288843",
                    "nome": "NF-E EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                    "email": "teste@teste.com",
                    "endereco": {
                        "bairro": "Bairro teste",
                        "cep": "05685040",
                        "codigo_municipio": "5300108",
                        "codigo_pais": "1058",
                        "complemento": "",
                        "logradouro": "Rua do Consultor",
                        "nome_municipio": "Brasilia",
                        "nome_pais": "Brasil",
                        "numero": "14",
                        "telefone": "",
                        "uf": "DF"
                    }
                },
                "forma_de_pagamento": [
                    {
                        "tipo_de_pagamento": "03",
                        "valor_do_pagamento": 15,
                        "cnpj_credenciadora": "27.197.888/0186-02",
                        "bandeira_operadora": "01",
                        "numero_autorizacao_operacao": "1",
                        "tipo_de_integracao": "1"
                    },
                    {
                        "tipo_de_pagamento": "01",
                        "cnpj_credenciadora": null,
                        "bandeira_operadora": null,
                        "tipo_de_integracao": null,
                        "numero_autorizacao_operacao": null,
                        "valor_do_pagamento": 85
                    }
                ],
                "produtos": [
                    {
                        "cest": "1300402",
                        "cfop": "5103",
                        "cnpj_fabricante_mercadoria": null,
                        "codigo_beneficio_fiscal": null,
                        "codigo_ean": "7891000315507",
                        "codigo_produto": "14600",
                        "declaracao_importacao": [],
                        "descricao": "NOTA FISCAL EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                        "ean_unidade_trib": "7891000315507",
                        "extipi": "22",
                        "imposto_devolvido": null,
                        "ind_valor_total": null,
                        "informacoes_adicionais": "teste",
                        "ncm": "22086000",
                        "num_controle_fci": null,
                        "num_item_pedido": "1",
                        "num_pedido": "5100003910",
                        "outras_despesas": 0,
                        "producao_escala": null,
                        "quantidade_comercial": 10,
                        "quantidade_tributaria": 10,
                        "tributacao": { "icms": { "codigo_origem_produto": 2 } },
                        "unidade_comercial": "UN",
                        "unidade_tributaria": "UN",
                        "valor_desconto": 0,
                        "valor_frete": 0,
                        "valor_seguro": 0,
                        "valor_total_produto": 100,
                        "valor_unitario_comercial": 10,
                        "valor_unitario_tributario": 10
                    }
                ],
                "transporte": {
                    "volume_transportado": [
                        {
                            "especie": "A Granel",
                            "lacres": [],
                            "marca": "0",
                            "numeracao_volumes": "333",
                            "peso_bruto": 0,
                            "peso_liquido": 0,
                            "quantidade_volumes": 1
                        }
                    ]
                }
            }
        ]
    }
}'


EXEMPLO DE RESPOSTA
{
    "nfce_batch": {
        "lote": "1",
        "serie": "233",
        "engine_de_calculo": "nexaas",
        "sincronicidade": "0",
        "uf": "53",
        "nfces": [
            {
                "dados_gerais": {
                    "uf": "53",
                    "serie": 233,
                    "codigo_mun_ocorrencia": "5300108",
                    "natureza_operacao": "saida",
                    "codigo_natureza_operacao": "002",
                    "csc": "000002",
                    "id_token": "A16A5A2DD8FA443FB8710D9AB8EB5432",
                    "tipo_operacao": "1",
                    "destino_operacao": "1",
                    "finalidade_nfe": "1",
                    "indicador_presenca": "1"
                },
                "emitente": {
                    "cnpj": "22769530000131",
                    "razao_social": "Organizacao Teste NFCe / DF",
                    "nome_fantasia": "Organizacao Teste NFCe / DF",
                    "inscricao_estadual": "772733700120",
                    "codigo_regime_tributario": 3,
                    "regime_tributario_diferenciado": "ISENLF",
                    "endereco": {
                        "bairro": "Asa Sul",
                        "cep": "70070938",
                        "logradouro": "SAUS Quadra 4 Lote 9/10",
                        "nome_pais": "Brasil",
                        "nome_municipio": "Brasilia",
                        "numero": "04",
                        "codigo_municipio": "5300108",
                        "codigo_pais": "1058",
                        "uf": "DF"
                    }
                },
                "cliente": {
                    "cpf_cnpj": "86152288843",
                    "email": "teste@teste.com",
                    "nome": "NF-E EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                    "pessoa_fisica_juridica": "person",
                    "endereco": {
                        "bairro": "Bairro teste",
                        "cep": "05685040",
                        "logradouro": "Rua do Consultor",
                        "nome_pais": "Brasil",
                        "nome_municipio": "Brasilia",
                        "numero": "14",
                        "codigo_municipio": "5300108",
                        "codigo_pais": "1058",
                        "uf": "DF"
                    }
                },
                "retirada": {
                    "endereco": {
                        "nome_pais": "Brasil",
                        "codigo_pais": "1058"
                    }
                },
                "entrega": {
                    "endereco": {
                        "nome_pais": "Brasil",
                        "codigo_pais": "1058"
                    }
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
                        "cfop": "5102",
                        "unidade_comercial": "UN",
                        "ean_unidade_trib": "7891000315507",
                        "unidade_tributaria": "UN",
                        "num_pedido": "5100003910",
                        "num_item_pedido": "1",
                        "quantidade_comercial": 10,
                        "valor_unitario_comercial": 10,
                        "quantidade_tributaria": 10,
                        "valor_unitario_tributario": 10,
                        "valor_frete": 0,
                        "valor_seguro": 0,
                        "valor_desconto": 0,
                        "valor_total_produto": 100,
                        "outras_despesas": 0,
                        "tributacao": {
                            "icms": {
                                "aliquota_consumidor_final": 0,
                                "aliquota_icms": 17,
                                "aliquota_icms_simples_nacional": 0,
                                "aliquota_icms_st": 0,
                                "aliquota_interestadual": "12",
                                "aliquota_interna_interestadual": "0.0000",
                                "base_icmsst_retido": 0,
                                "codigo_origem_produto": 2,
                                "credito_icms_simples_nacional": 0,
                                "modalidade_base_calculo": "3",
                                "perc_diferimento": 0,
                                "perc_fcp_interestadual": "0.0000",
                                "perc_mva_icms_st": 0,
                                "perc_provisorio_interestadual": "100",
                                "perc_reducao_base_calculo": 0,
                                "perc_reducao_base_calculo_st": 0,
                                "situacao_tributaria": "00",
                                "valor_base_calculo": 100,
                                "valor_base_calculo_st": 0,
                                "valor_icms": 17,
                                "valor_icms_desonerado": 0,
                                "valor_icms_diferido": 0,
                                "valor_icms_operacao": 0,
                                "valor_icms_st": 0,
                                "valor_icmsst_retido": 0
                            },
                            "pis": {
                                "aliquota_st": 0,
                                "valor_base_calculo": 100,
                                "valor_base_calculo_st": 0,
                                "situacao_tributaria": "49",
                                "aliquota_pis": 3,
                                "aliquota_pis_reais": 0,
                                "aliquota_pis_reais_st": 0,
                                "valor_pis": 3,
                                "valor_pis_st": 0
                            },
                            "cofins": {
                                "aliquota_st": 0,
                                "valor_base_calculo": 100,
                                "valor_base_calculo_st": 0,
                                "situacao_tributaria": "49",
                                "aliquota_cofins": 4,
                                "aliquota_cofins_reais": 0,
                                "aliquota_cofins_reais_st": 0,
                                "valor_cofins": 4,
                                "valor_cofins_st": 0
                            }
                        }
                    }
                ],
                "transporte": {
                    "volume_transportado": [
                        {
                            "numeracao_volumes": "333",
                            "marca": "0",
                            "especie": "A Granel",
                            "quantidade_volumes": 1,
                            "peso_liquido": 0,
                            "peso_bruto": 0
                        }
                    ]
                },
                "forma_de_pagamento": [
                    {
                        "tipo_de_pagamento": "03",
                        "valor_do_pagamento": 15,
                        "tipo_de_integracao": 1,
                        "cnpj_credenciadora": "27197888018602",
                        "bandeira_operadora": "01",
                        "numero_autorizacao_operacao": "1"
                    },
                    {
                        "tipo_de_pagamento": "01",
                        "valor_do_pagamento": 85
                    }
                ]
            }
        ]
    }
}
```
