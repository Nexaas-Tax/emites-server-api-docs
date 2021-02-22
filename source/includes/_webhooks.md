# Webhooks

Os Webhooks são notificações assíncronas enviadas para todos os eventos solicitados ao Emites.  
Sendo assim, ao receber um evento, o sistema envia uma requisição HTTP para a url configurada no Emites com as informações relacionadas ao evento.
Os webhooks também são conhecidos como Callbacks ou Reverse API .  

Para adicionar uma nova url, acesse a interface do Emites, clique no ícone do menu, depois em conta, no final da página terá um botão para a adição do novo webhook.  

Após adicionado, a cada requisição efetuada ao Emites, será retornada uma notificação sobre o estado do evento.  

Os webhooks seguem a mesma estrutura com exceção da inutilização solicitada, rejeitada e com erro que possuem o campo "additional_info" com informações adicionais;

Veja abaixo a descrição de cada campo:

`object_type: tipo do objeto solicitado (NFe/NFeBatch e NFCe/NFCeBatch)`  

`object_id: id interno objeto solicitado`

`organization_id: id da organização`

`event: status da nota`

`additional_info: informações adicionais`

<aside class="notice">
    OBS.: O tipo de objeto NFeBatch e NFCeBatch é referente a lotes compostos de várias notas e o tipo de objeto NFe ou NFCe é referente à nota avulsa.
</aside>

## Lote enviado

É Quando é realizado o envio de um lote de NF para a SEFAZ e o mesmo é recebido. Nesta etapa será enviado o seguinte webhook:  

```
{
  "object_type":"NFeBatch",
  "object_id":5,
  "organization_id":1,
  "event":"sent"
}
```

## Lote sendo processado

Quando a SEFAZ do estado recebe o lote e inicia o processo de autenticação do mesmo. Nesta etapa será enviado o seguinte webhook:

```
{
  "object_type":"NFeBatch",
  "object_id":5,
  "organization_id":1,
  "event":"processed"
}
```

## Lote rejeitado

Quando o lote é rejeitado pela SEFAZ. Nesta etapa será enviado o seguinte webhook:

```
{
  "object_type":"NFeBatch",
  "object_id":5,
  "organization_id":1,
  "event":"rejected"
}
```

## Lote com erro

Quando ocorre um erro interno durante o processo de emissão de um lote. Nesta etapa será enviado o seguinte webhook:

```
{
  "object_type":"NFeBatch",
  "object_id":5,
  "organization_id":1,
  "event":"error"
}
```

## Nota emitida

Quando a NF é aceita pela SEFAZ. Nesta etapa será enviado o seguinte webhook:

```
{
  "object_type":"NFe",
  "object_id":5,
  "organization_id":1,
  "event":"succeeded"
}
```

## Nota rejeitada

Quando a NF é rejeitada pela SEFAZ. Nesta etapa será enviado o seguinte webhook:

```
{
  "object_type":"NFe",
  "object_id":5,
  "organization_id":1,
  "event":"rejected"
}
```

## Nota denegada

Quando a NF é denegada pela SEFAZ. Nesta etapa será enviado o seguinte webhook:

```
{
  "object_type":"NFe",
  "object_id":5,
  "organization_id":1,
  "event":"denegated"
}
```

## Nota não enviada

Quando a NF não é enviada para SEFAZ. Nesta etapa será enviado o seguinte webhook:

```
{
  "object_type":"NFe",
  "object_id":5,
  "organization_id":1,
  "event":"not_sent"
}
```

## Nota com erro

Quando ocorre um erro interno durante o processo de emissão de uma nota. Nesta etapa será enviado o seguinte webhook:

```
{
  "object_type":"NFe",
  "object_id":5,
  "organization_id":1,
  "event":"error"
}
```

## Nota cancelada  

Quando o cancelamento da NF é aceito pela SEFAZ. Nesta etapa será enviado o seguinte webhook:

**Obs.: Após o processamento da solicitação de cancelamento da NF, o XML do evento estará disponível via consulta da NF no campo "cancel_xml_url".**

```
{
  "object_type":"NFe",
  "object_id":5,
  "organization_id":1,
  "event":"cancelled"
}
```

## Nota emitida em contingência offline

Quando a NF é emitida em contingência offline no server. Nesta etapa será enviado o seguinte webhook:

```
{
  "object_type":"NFCe",
  "object_id":5,
  "organization_id":1,
  "event":"pending_offline_contingency_authorization"
}
```

## Cancelamento rejeitado

Quando o cancelamento da NF é rejeitado pela SEFAZ. Nesta etapa será enviado o seguinte webhook:

```
{
  "object_type":"NFe",
  "object_id":5,
  "organization_id":1,
  "event":"cancel_rejected"
}
```

## Inutilização solicitada

Quando uma solicitação de inutilização de um número de NF é enviada para SEFAZ

```
{
  "object_type":"NFeDisablement",
  "object_id":5,
  "organization_id":1,
  "event":"disabled",
  "additional_info": {
    "uf":"35",
    "serie":"0",
    "motivo": "Erro na emissão da nota fiscal",
    "numero_inicial":"98080986123",
    "numero_final":"98080986123",
    "protocolo": "135180216568911"
  }
}
```

## Inutilização rejeitada

Quando uma solicitação de inutilização de um número de NF é rejeitada pela SEFAZ

```
{
  "object_type":"NFeDisablement",
  "object_id":5,
  "organization_id":1,
  "event":"disablement_rejected",
  "additional_info": {
    "uf":"35",
    "serie":"0",
    "motivo": "Erro na emissão da nota fiscal",
    "numero_inicial":"98080986123",
    "numero_final":"98080986123",
    "errors":["215 - Rejeição: Falha no schema XML"]
  }
}
```

## Inutilização com erro

Quando ocorre um erro interno durante o processo de solicitação de inutilização de um número ou intervalo

```
{
  "object_type":"NFeDisablement",
  "object_id":5,
  "organization_id":1,
  "event": "disablement_error",
  "additional_info": {
    "uf":"35",
    "serie":"0",
    "motivo": "Erro na emissão da nota fiscal",
    "numero_inicial":"98080986123",
    "numero_final":"98080986123",
    "errors":["Ocorreu um erro interno ao acessar o Webservice da SEFAZ. Por favor, entre em contato com o nosso suporte"]
  }
}
```

## Carta de Correção rejeitada

Quando uma solicitação de carta de correção de uma NF é rejeitada pela SEFAZ

**Obs.: Após o processamento da solicitação da carta de correção da NF, o XML do evento estará disponível via consulta da NF no campo "correction_xml_url".**

```
{
  "object_type":"NFe",
  "object_id":5,
  "organization_id":1,
  "event":"correction_rejected"
}
```

## Importação de regras tributárias concluída

Quando uma importação de regras tributárias é finalizada

```
{
  "object_type": "TaxationRulesImport",
  "object_id": 5,
  "organization_id": 1,
  "event": "taxation_rules_import_completed"
}
```
