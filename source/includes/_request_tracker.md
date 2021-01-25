# Request Tracker (Request ID)

Para consultar as informações de um documento fiscal ou mais pelo ID da requisição (Request ID) ou pelo ID próprio enviado (Remote ID), é necessário realizar uma requisição GET para o seguinte endereço:

<div class="api-endpoint">
    <div class="endpoint-data">
        <i class="label label-get">GET</i>
        <h6>/api/v1/request_tracker/{request_id}</h6>
    </div>
</div>

## Exemplo de busca pelo ID de autorização para uma emissão single
```shell
EXEMPLO DE REQUISIÇÃO

### Usando Request ID
curl --request GET \
  --url http://app.production.emites.com.br/api/v1/request_tracker/491dd276-b7d9-4623-beb1-234c66a80be3 \
  --header 'authorization: Bearer 6f42433270bc61d746556b17605db05a' \
  --header 'content-type: application/json'

### Usando Remote ID
curl --request GET \
  --url http://app.production.emites.com.br/api/v1/request_tracker/abc123 \
  --header 'authorization: Bearer 6f42433270bc61d746556b17605db05a' \
  --header 'content-type: application/json'

EXEMPLO DE RESPOSTA
{
  "request_tracker": {
    "request_id": "491dd276-b7d9-4623-beb1-234c66a80be3",
    "remote_id": "abc123",
    "request_kind": "authorization",
    "client_version": "client 2.0",
    "incoming_requests": [
      "/path/to/incoming_request/file.json"
    ],
    "nfces": [
      {
        "access_key": null,
        "id": 1,
        "organization_id": 1,
        "status": "processing",
        "messages": null,
        "xml_url": null,
        "danfe_url": null,
        "request_id": null,
        "remote_id": null,
        "other_trackers": []
      }
    ]
  }
}
```

## Exemplo de busca pelo ID de autorização para uma emissão batch
```shell
EXEMPLO DE RESPOSTA
{
  "request_tracker": {
    "request_id": "7d391761-1681-4e9c-ac6e-d47389f211f0",
    "remote_id": "abc123",
    "request_kind": "authorization",
    "client_version": "client 2.0",
    "incoming_requests": [
      "/path/to/incoming_request/file.json"
    ],
    "nfce_batches": [
      {
        "id": 1,
        "organization_id": 1,
        "nfces": [
          {
            "access_key": "53190222769530000131556110000002001616311935",
            "id": 2,
            "organization_id": 1,
            "status": "succeeded",
            "messages": null,
            "xml_url": "http://download-xml-url.com.br",
            "danfe_url": "http://download-danfe-url.com.br",
            "request_id": "c1faf5c3-0f13-4376-800d-dc814c3932be",
            "remote_id": null,
            "other_trackers": []
          }
        ]
      }
    ]
  }
}
```

## Exemplo de busca pelo ID de autorização para uma nota cancelada
```shell
EXEMPLO DE RESPOSTA

{
  "request_tracker": {
    "request_id": "7d391761-1681-4e9c-ac6e-d47389f211f0",
    "remote_id": "abc123",
    "request_kind": "authorization",
    "client_version": "client 2.0",
    "incoming_requests": [
      "/path/to/incoming_request/file.json"
    ],
    "nfes": [
      {
        "access_key": "33210127197888003680557590000003591034461550",
        "id": 3,
        "organization_id": 1,
        "status": "cancelled",
        "messages": null,
        "xml_url": "http://download-xml-url.com.br",
        "danfe_url": "http://download-danfe-url.com.br",
        "request_id": null,
        "remote_id": null,
        "other_trackers": [
          {
            "request_id": "8fe845d5-3a1c-4810-aea1-96e008012753",
            "remote_id": "foobar123",
            "request_type": "cancel",
            "status": "cancelled",
            "messages": null
          }
        ]
      }
    ]
  }
}
```

## Exemplo de busca pelo ID de cancelamento
```shell
EXEMPLO DE RESPOSTA

{
  "request_tracker": {
    "request_id": "8fe845d5-3a1c-4810-aea1-96e008012754",
    "remote_id": "foobar124",
    "request_kind": "cancel",
    "client_version": "foo2",
    "incoming_requests": [
      "/path/to/incoming_request/file.json"
    ],
    "nfes": [
      {
        "access_key": "33210127197888003680557590000003591034461550",
        "id": 4,
        "organization_id": 1,
        "status": "cancel_rejected",
        "messages": "SEFAZ indisponível no momento, por favor tente mais tarde",
        "xml_url": "http://download-xml-url.com.br",
        "danfe_url": "http://download-danfe-url.com.br",
        "request_id": "2a82ab3f-9d64-40e4-a0b3-63b050235107",
        "remote_id": "foobar543",
        "other_trackers": null
      }
    ]
  }
}
```