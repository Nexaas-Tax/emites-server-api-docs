# Importação de regras tributárias

O processo de importação das regras tributárias segue resumidamente o seguinte fluxo:

1. Um CSV com os dados da regra deve ser enviado para o _endpoint_ de [criação de importação](#cria-o-de-uma-importa-o)
2. Ao receber a requisição, o Emites irá registar o CSV para processá-lo em um momento oportuno
3. Ao iniciar a importação, o Emites processa o CSV linha a linha, decodificando e validando seus dados
4. Se todas as regras estiverem corretas, o Emites substituirá as regras atuais da Organização pelas da importação
5. Caso haja qualquer erro, nenhuma substituição ocorrerá
6. A qualquer momento é possível [consultar o status da importação](#consulta-de-importa-o)
7. Em caso de falha, ao consultar o status da importação haverá uma lista de erros encontrados durante o processo
8. Para um CSV com muitas linhas, é conveniente utilizar o serviço de [webhooks](#importa-o-de-regras-tribut-rias-conclu-da) para ser notificado após o fim do processo

## Criação de uma importação

Para criar uma importação, é necessário realizar uma requisição POST para o seguinte endereço:

<div class="api-endpoint">
  <div class="endpoint-data">
    <i class="label label-get">POST</i>
    <h6>/api/v1/organizations/{:organization_id}/taxation_rules_import</h6>
  </div>
</div>

```shell
EXEMPLO DE REQUISIÇÃO

curl -X POST \
  -F 'file=@/path/to/csv/import.csv' \
  https://app.production.emites.com.br/api/v1/organizations/8/taxation_rules_import \
  -H 'authorization: Bearer c3b1164e8ae17f6d9712730ec75be6da'

EXEMPLO DE RESPOSTA

{
  "taxation_rules_import": {
    "id": 12,
    "account_id": 2,
    "organization_id": 8,
    "status": "pending",
    "errors": [],
    "created_at": "2019-06-24T15:58:51.866-03:00",
    "updated_at": "2019-06-24T15:58:51.866-03:00"
  }
}
```
<br>
Observe que a requisição é do tipo `multipart/form-data`. O arquivo CSV deve ser referenciado através do atributo `file`.

Um erro será retornado caso se tente criar uma nova importação quando ainda houver, para mesma Organização, outra com o status `pending` ou `prossessing`.

## Consulta de importação

Para consultar uma importação de regras tributárias é necessário realizar a seguinte requisição:  

<div class="api-endpoint">
  <div class="endpoint-data">
    <i class="label label-get">GET</i>
    <h6>/api/v1/organizations/{:organization_id}/taxation_rules_import/{:taxation_rules_import}</h6>
  </div>
</div>

```shell
EXEMPLO DE REQUISIÇÃO

curl -X GET \
  https://app.production.emites.com.br/api/v1/organizations/8/taxation_rules_import/12 \
  -H 'authorization: Bearer 6f42433270bc61d746556b17605db1s4' \
  -H 'content-type: application/json'


EXEMPLO DE RESPOSTA:

{
  "taxation_rules_import": {
    "id": 12,
    "account_id": 2,
    "organization_id": 8,
    "status": "processing",
    "errors": [],
    "created_at": "2019-06-24T15:58:51.866-03:00",
    "updated_at": "2019-06-24T15:58:51.866-04:00"
  }
}
```

## Status da importação

 Status       | Pode transitar para  | Descrição
--------------|----------------------|-----------
 `pending`    | `processing`         | A importação foi registrada mas ainda aguarda processamento
 `processing` | `success` ou `error` | A importação está sendo processada
 `success`    |                      | A importação foi concluída com sucesso e as regras antigas foram substituídas pelas da importação
 `error`      |                      | A importação foi concluída, mas nenhuma regra foi substituída porque erros foram identificados


## Erros de importação

Os erros identificados durante o processo de importação são retornados pelo consulta de [status da importação](#consulta-de-importa-o) e seguem o seguinte formato:

```shell
{
  "taxation_rules_import": {
    "id": 12,
    "account_id": 2,
    "organization_id": 8,
    "status": "processing",
    "errors": [
      {
        "row": 1,
        "message": "invalid_nat_op_code",
        "description": "Código de natureza de operação inválido"
      },
      {
        "row": 10,
        "message": "invalid_condition_criterion",
        "description": "O atributo de condição aplicacao não aceita os critérios diferente/não está entre"
      }
    ],
    "created_at": "2019-06-24T15:58:51.866-03:00",
    "updated_at": "2019-06-24T15:58:51.866-04:00"
  }
}
```
<br>

Onde:

 Campo         | Descrição
---------------| ----------
 `row`         | A linha do arquivo CSV onde o erro foi identificado, será `-1` em caso de erros globais
 `message`     | O tipo da mensagem de erro
 `description` | Uma descrição detalhada

Os possíveis erros são:

 `message`                     | `description`
-------------------------------|--------------
 `server_error`                | O servidor falhou ao tentar processar a importação
 `invalid_nat_op_code`         | Código de natureza de operação inválido
 `invalid_condition_criterion` | O atributo de condição **`{atributo}`** não aceita o critério **`{critério}`**
 `invalid_condition_value`     | O atributo de condição **`{condição}`** não aceita o valor **`{valor}`**

**Obs.**: A importação identifica no máximo 100 erros, quando este limite é atingido o processo de importação é encerrado e eventuais erros adicionais não serão identificados.

## Arquivo CSV

Ao construir o arquivo, as seguintes regras gerais que devem ser observadas:

- As células devem ser separadas por vírgula (`,`)
- O arquivo deve possuir um cabeçalho com o nome das colunas (Ex.: `nat_op_code,uf_origem,uf_destino`)
- Não pode haver espaços entre os valores (Ex.: `007, RJ,SP` é um erro, o correto seria `007,RJ,SP`)
- Valores numéricos devem ser separados por ponto (Ex.: R$ 2.000,12 deve ser traduzido como `2000.12`)
- Valores como listas devem estar entre aspas e seus itens internos separados com vírgula (Ex.: `007,"RJ,SP,RS",SP`)
- Não há uma ordem obrigatória para as colunas

### Código da natureza de operação

A coluna `nat_op_code` é obrigatória e deve ser preenchida em cada linha com um dos seguintes códigos:

 Código | Descrição
--------|-----------
 001    | Compra
 002    | Venda
 003    | Transferência
 004    | Devolução
 005    | Importação
 006    | Exportação
 007    | Remessa
 008    | Retorno
 009    | Outras Entradas
 010    | Outras Saídas
 011    | Serviços - ISSQN
 012    | Lançamento de Crédito
 013    | Recebimento
 014    | Ressarcimento

### Atributos de condição

Os seguintes atributos de condição podem ser enviados pelo CSV:

 Atributo | Nome | Aceita uma lista de valores? | Aceita os critérios **DIFERENTE DE** e **NÃO ESTÁ ENTRE** | Valores permitidos
----------|------|------------------------------|-----------------------------------------------------------|--------------------
 `aplicacao` | Aplicação do produto | Não | Não | Veja **Tabela de valores para Aplicação do produto**
 `cest` | CEST | Sim | Sim | Sem restrições
 `cnpj_destinatario` | CNPJ do destinatário | Não | Não | Sem restrições
 `destinatario_consumidor_final` | Destinatário é consumidor final | Não | Não | `S` para **Sim** e `N` para **Não**
 `destinatario_contribuinte_icms` | Destinatário é contribuinte do ICMS | Não | Não | `S` para **Sim** e `N` para **Não**
 `destinatario_pessoa_juridica` | Destinatário é pessoa jurídica | Não | Não | `S` para **Sim** e `N` para **Não**
 `destinatario_beneficiario_suframa` | Destinatário beneficiário do SUFRAMA | Não | Não | `S` para **Sim** e `N` para **Não**
 `emitente_beneficiario_suframa` | Emitente beneficiário do SUFRAMA | Não | Não | `S` para **Sim** e `N` para **Não**
 `documentos_referenciados` | Possui documentos referenciados | Não | Não | `S` para **Sim** e `N` para **Não**
 `extipi` | ExTIPI | Não | Não | Sem restrições
 `municipio_destino` | Município de destino | Não | Não | Sem restrições
 `ncm` | NCM | Sim | Sim | Sem restricões
 `origem_produto` | Origem do produto | Sim | Sim | Veja **Tabela de valores para Origem do produto**
 `uf_destino` | UF destino | Sim | Sim | Sigla da unidade federativa, em maiúsculo
 `uf_origem` | UF origem | Sim | Sim | Sigla da unidade federativa, em maiúsculo
 `codigo_regime_tributario` | Código de regime tributário | Sim | Sim | Veja **Tabela de valores para Código de regime tributário**
 `regime_tributario_diferenciado` | Regime Tributário Diferenciado do emitente | Sim | Sim | Veja **Tabela de valores para Regime Tributário Diferenciado do emitente**
 `tipo_operacao` | Tipo da operação | Não | Não | `0` para **Entrada** e `1` para **Saída**
 `inscricao_suframa` | SUFRAMA | Não | Não | Sem restrições
 `situacao_fiscal` | Situação fiscal | Sim | Sim | Sem restrições
 `codigo_beneficio_fiscal` | Código de benefício fiscal | Sim | Sim | Sem restrições
 `indicador_presenca` | Indicador de presença do comprador no estabelecimento comercial no momento da operação | Sim | Sim | Veja **Tabela de valores para Indicador de presença do comprador no estabelecimento comercial**
 `codigo_produto` | Código do produto | Sim | Sim | Sem restrições
 `vigencia_start` | Data inicial de vigência | Não | Não | Data válida no formato `dd/mm/aaaa`
 `vigencia_end` | Data final de vigência | Não | Não | Data válida no formato `dd/mm/aaaa`

**Obs.**: O atributo `codigo_do_produto` pode ser omitido automaticamente durante a importação mesmo quando presente no CSV. O `codigo_do_produto` só **NÃO SERÁ OMITIDO** quando existir uma regra para a mesma natureza de operação e mesmo grupo tributário com condições diferentes mas consequências potencialmente conflitantes, de modo que a presença do atributo é relevante para evitar o enquadramento inadequado em determinados cenários.

#### Tabela de valores para Aplicação do produto

 Valor | Descrição
-------|----------
 001 | Amostra Grátis
 002 | Anulação de Valor
 003 | Aquisição
 004 | Armazenagem
 005 | Ativo Imobilizado
 006 | Ato Cooperativo
 007 | Baixa de Estoque a título de encerramento de atividade
 008 | Baixa de Estoque a título de perda, roubo ou deteriorização
 009 | Bonificação, Doação ou Brinde
 010 | Comercialização
 011 | Comodato
 012 | Devolução de Compra - Industrialização
 013 | Conserto ou Reparo
 014 | Consignação
 015 | Conta e Ordem de Terceiros
 016 | Crédito Acumulado de ICMS
 017 | Demonstração
 018 | Distribuição
 019 | Embalagem
 020 | Exposição ou Feira
 021 | ICMS retido por ST
 022 | Industrialização
 023 | Locação
 024 | Operação fora estabelecimento
 025 | Prestação
 026 | Regime Especial Aduaneiro de Admissão temporária
 027 | Saldo Credor de ICMS
 028 | Saldo Devedor de ICMS
 029 | Uso e Consumo
 030 | Vasilhame ou Sacaria
 031 | Devolução de Venda - Industrialização
 032 | Transferência
 033 | Simples Faturamento
 034 | Devolução de Compra - Comercialização
 035 | Devolução de Venda - Comercialização
 099 | Outros

#### Tabela de valores para Origem do produto

 Valor | Descrição
-------|----------
 0 | Nacional, exceto as indicadas nos códigos 3 a 5
 1 | Estrangeira - Importação direta, exceto a indicada no código 6
 2 | Estrangeira - Adquirida no mercado interno, exceto a indicada no código 7
 3 | Nacional, mercadoria ou bem com conteúdo de Importação superior a  40%
 4 | Nacional, cuja produção tenha sido feita em conformidade com os processos produtivos básicos de que tratam o Decreto-Lei nº 288/67, e as Leis nºs  8.248/91, 8.387/91, 10.176/01 e 11.484/07
 5 | Nacional, mercadoria ou bem com Conteúdo de Importação inferior ou igual a 40%
 6 | Estrangeira - Importação direta, sem similar nacional, constante em lista de Resolução CAMEX
 7 | Estrangeira - Adquirida no mercado interno, sem similar nacional, constante em lista de Resolução CAMEX
 8 | Serviço - Nacional
 9 | Serviço - Estrangeiro, cujo resultado se verifique no país
 10 | Serviço - Estrangeiro, cujo resultado se verifique no exterior

#### Tabela de valores para Código de regime tributário

 Valor | Descrição
-------|-----------
 1 | Simples Nacional
 2 | Simples Nacional, excesso sublimite de receita bruta
 3 | Regime Normal

#### Tabela de valores para Regime Tributário Diferenciado do emitente

 Valor | Descrição
-------|----------
 001 | Repes
 002 | Recap
 003 | Padis
 004 | Patvd
 005 | Reidi
 006 | Repenec
 007 | Reicomp
 008 | Retaero
 009 | Recine
 010 | Resíduos Sólidos
 011 | Recopa
 012 | Copa do Mundo
 013 | Retid
 014 | Repnbl-Redes
 015 | Reif
 016 | Olimpíadas
 017 | TaxWeb - LFDES
 018 | TaxWeb - LFEM
 019 | TaxWeb - ISENLF
 020 | ICMS Substituto Tributário
 021 | ICMS Substituído Tributário

#### Tabela de valores para Indicador de presença do comprador no estabelecimento comercial

 Valor | Descrição
-------|----------
 0 | Não se aplica
 1 | Operação presencial
 2 | Operação não presencial, pela Internet
 3 | Operação não presencial, Teleatendimento
 4 | NFC-e em operação com entrega a domicílio
 9 | Operação não presencial, outros

### Critérios para os atributos de condição

Os valores de um atributo de condição são comparados com os dados de um documento fiscal, esta comparação pode ser feita utilizando-se quatro critérios diferentes: **IGUAL A**, **DIFERENTE DE**, **ESTÁ ENTRE** e **NÃO ESTÁ ENTRE**.

Para representar estes diferentes critérios no CSV, os valores de cada condição devem vir formatados da seguinte forma:

 Critério | Formato do valor no CSV
----------|-------------------------
 **IGUAL A** | Sem nenhuma formatação específica, é o critério padrão
 **DIFERENTE DE** | Deve-se adicionar o caractere `!` antes do valor (Ex.: `!1`)
 **ESTÁ ENTRE** | Deve-se por o valor entre aspas (`"`) e separar os itens por vígula (`,`), (Ex.: `"0,1,2"`)
 **NÃO ESTÁ ENTRE** | Semelhante ao **ESTÁ ENTRE**, só que com o caractere `!` antes do primeiro item (Ex.: `"!0,1,2"`)

Os atributos `vigencia_start` e `vigencia_end` possuem critérios próprios que são inferidos dinâmicamente pelo processo de importação.

### Atributos de consequência

Os seguintes atributos de consequência podem ser enviados pelo CSV:

 Atributo | Nome | Tipo de imposto | Valores permitidos
----------|------|-----------------|-------------------
 `aliquota_icms` | Alíquota de ICMS | ICMS | Valores numéricos
 `aliquota_icms_st` | Alíquota de ICMS ST | ICMS | Valores numéricos
 `cfop` | CFOP | ICMS | Consulte [aqui](http://www.sped.fazenda.gov.br/spedtabelas/AppConsulta/publico/aspx/ConsultaTabelasExternas.aspx?CodSistema=SpedFiscal)
 `modalidade_base_calculo` | Modalidade de base de cálculo | ICMS | Veja **Tabela de valores para Modalidade de base de cálculo**
 `modalidade_base_calculo_st` | Modalidade de base de cálculo ST | ICMS | Veja **Tabela de valores para Modalidade de base de cálculo ST**
 `motivo_desoneracao` | Motivo de desoneração | ICMS | Veja **Tabela de valores para  Motivo de desoneração**
 `percentual_de_diferimento` | Percentual de diferimento | ICMS | Valores numéricos
 `percentual_de_fcp` | Percentual de FCP | ICMS | Valores numéricos
 `percentual_de_mva_st` | Percentual de MVA ST | ICMS | Valores numéricos
 `reducao_base_calculo` | Redução da base de cálculo | ICMS | Valores numéricos
 `reducao_de_base_de_calculo_st` | Redução da base de cálculo ST | ICMS | Valores numéricos
 `situacao_tributaria_icms` | Situação Tributária do ICMS | ICMS | Veja **Tabela de valores para Situação Tributária do ICMS**
 `uf_icms_st_devido` | UF de ICMS ST devido na operação | ICMS | Sigla da unidade federativa, em maiúsculo
 `aliquota_de_fcp_do_difal` | Alíquota de FCP do Difal | ICMS | Valores numéricos
 `aliquota_interestadual` | Alíquota interestadual | ICMS | Veja **Tabela de valores para Alíquota interestadual**
 `aliquota_interna_uf_destino` | Alíquota interna - UF destino | ICMS | Valores numéricos
 `base_de_calculo_da_uf_destino` | Base de cálculo da UF destino | ICMS | Valores numéricos
 `percentual_provisorio_de_partilha` | Percentual provisório de partilha | ICMS | Veja **Tabela de valores para Percentual provisório de partilha**
 `valor_icms_desonerado` | Valor do ICMS Desonerado | ICMS | Valores numéricos
 `aliquota_ipi` | Alíquota do IPI | IPI | Valores numéricos
 `situacao_tributaria_ipi` | Situação Tributária do IPI | IPI | Valores numéricos
 `valor_por_unidade_em_reais` | Valor por unidade (em reais) | IPI | Valores numéricos
 `codigo_enquadramento` | Código de Enquadramento Legal (cEnq) | IPI | Sem restrições
 `aliquota_cofins` | Alíquota do COFINS | PIS e COFINS | Valores numéricos
 `aliquota_do_cofins_st` | Alíquota do COFINS-ST | PIS e COFINS | Valores numéricos
 `aliquota_do_pis_st` | Alíquota do PIS-ST | PIS e COFINS | Valores numéricos
 `aliquota_em_reais_do_cofins` | Alíquota em reais do COFINS | PIS e COFINS | Valores numéricos
 `aliquota_em_reais_do_cofins_st` | Alíquota em reais do COFINS-ST | PIS e COFINS | Valores numéricos
 `aliquota_em_reais_do_pis` | Alíquota em reais do PIS | PIS e COFINS | Valores numéricos
 `aliquota_em_reais_do_pis_st` | Alíquota em reais do PIS-ST | PIS e COFINS | Valores numéricos
 `aliquota_pis` | Alíquota do PIS | PIS e COFINS | Valores numéricos
 `situacao_tributaria_pis` | Situação Tributária do PIS | PIS | Valores numéricos
 `situacao_tributaria_cofins` | Situação Tributária do COFINS | COFINS | Valores numericos

#### Tabela de valores para Modalidade de base de cálculo

 Valor | Descrição
-------|----------
 0 | Margem de Valor Agregado
 1 | Pauta (valor)
 2 | Preço Tabelado Máximo (valor)
 3 | Valor da Operação

#### Tabela de valores para Modalidade de base de cálculo ST

 Valor | Descrição
-------|----------
 0 | Preço Tabelado ou Máximo Sugerido
 1 | Lista Negativa (valor)
 2 | Lista Positiva (valor)
 3 | Lista Neutra (valor)
 4 | Margem de Valor Agregado (%)
 5 | Pauta (valor)

#### Tabela de valores para  Motivo de desoneração

 Valor | Descrição
-------|----------
 1  | Táxi
 3  | Produtor Agropecuário
 4  | Frotista/Locadora
 5  | Diplomático/Consular
 6  | Utilitários e Motocicletas da Amazônia Ocidental e Áreas de Livre Comércio (Resolução 714/88 e 790/94 – CONTRAN e suas alterações)
 7  | SUFRAMA
 8  | Venda a Órgão Público
 9  | Outros. (NT 2011/004)
 10 | Deficiente Condutor (Convênio ICMS 38/12)
 11 | Deficiente Não Condutor (Convênio ICMS 38/12)
 12 | Órgão de fomento e desenvolvimento agropecuário
 16 | Olimpíadas Rio 2016 (NT 2015.002)
 90 | Solicitado pelo Fisco (NT 2016/002) (Revogada a partir da versão 3.10 a possibilidade de usar o motivo 2 - Deficiente Físico)

#### Tabela de valores para Situação Tributária do ICMS

 Valor | Descrição
-------|----------
00  | Tributada integralmente
10  | Tributada e com cobrança do ICMS por substituição tributária
20  | Com redução de base de cálculo
30  | Isenta ou não tributada e com cobrança do ICMS por substituição tributária
40  | Isenta
41  | Não Tributada
50  | Suspensão
51  | Diferimento
60  | ICMS cobrado anteriormente por substituição tributária
70  | Com redução de base de cálculo e cobrança do ICMS por substituição tributária
90  | Outros
101 | Tributada pelo Simples Nacional com permissão de crédito
102 | Tributada pelo Simples Nacional sem permissão de crédito
103 | Isenção do ICMS no Simples Nacional para faixa de receita bruta
201 | Tributada pelo Simples Nacional com permissão de crédito e com cobrança do ICMS por Substituição Tributária
202 | Tributada pelo Simples Nacional sem permissão de crédito e com cobrança do ICMS por Substituição Tributária
203 | Isenção do ICMS nos Simples Nacional para faixa de receita bruta e com cobrança do ICMS por Substituição Tributária
300 | Imune
400 | Não tributada pelo Simples Nacional
500 | ICMS cobrado anteriormente por substituição tributária (substituído) ou por antecipação
900 | Outros

#### Tabela de valores para Alíquota interestadual

 Valor | Descrição
-------|----------
 4  | 4% alíquota para produtos importados
 7  | 7% para os estados de origem do Sul e Sudeste (exceto ES), destinado para os estados do Norte, Nordeste, Centro-Oeste e Espírito Santo
 12 | 12% para os demais casos

#### Tabela de valores para Percentual provisório de partilha

 Valor | Descrição
-------|----------
 40  | 40% em 2016
 60  | 60% em 2017
 80  | 80% em 2018
 100 | 100% a partir de 2019
