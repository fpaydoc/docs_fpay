+++
description = "Use hugo shortcodes to quickly compose your documentation pages."
title = "Pago Presencial QR Estatico"
weight = 5

+++
### Generar la intencion de pago
Al ejecutar esta API, obtendrás una intención de pago en su estado inicial created, que contendrá las URLs HATEOAS relacionados con la llamada; es decir, no deben guardar las URL obtenidas en el responses de la intención de pago porque estas pueden cambiar.





**Header**
```markdown
Content-Type:application/json
Authorization:Basic {{client_id}}:{{client_secret}}
FP-Flow-Country:cl
```

**URL**
```markdown
https://payments-wallet-qa.fif.tech/checkout/payments
```

**Body**
```markdown
{
	"intent": "sale",
	"payment_method": "WALLET_QR",
	"transaction": {
		"store_id": "15",
		"terminal_id": "10",
		"description": "Articulos Electronicos",
		"soft_descriptor": "WALLET-QR-PAYMENT",
		"merchant_unique_id": "{{$timestamp}}",
		"reconciliation_id": "{{$timestamp}}",
        "item_list": {
			"shipping_method": "DIGITAL",
			"items": [
				{
					"thumbnail": "http://notfound404.cl/some.jpg",
					"sku": "TVLG43S",
					"name": "TVLG43",
					"description": "Tv LG 43",
					"quantity": 1,
					"price": 80,
					"tax": 0,
					"_id": "5a7a14343df88b000fdac92a"
				},
				{
					"thumbnail": "http://notfound404.cl/some.jpg",
					"sku": "TVLG55S",
					"name": "TVLG43",
					"description": "Tv LG 55",
					"quantity": 1,
					"price": 100,
					"tax": 0,
					"_id": "5a7a14343df88b000fdac92a"
				},
				{
					"thumbnail": "http://notfound404.cl/some.jpg",
					"sku": "TVLG60S",
					"name": "TVLG60",
					"description": "Tv LG 60",
					"quantity": 1,
					"price": 120,
					"tax": 0,
					"_id": "5a7a14343df88b000fdac92a"
				}
			],
			"shipping_address": {
				"line1": "Dirección Av. Irarrazabal",
				"city": "Santiago",
				"country_code": "CL",
				"phone": "+56 9 8762 1244",
				"type": "HOME_OR_WORK",
				"recipient_name": "Jose Torres"
			}
		},
		"amount": {
			"currency": "CLP",
			"total": 350,
			"details": {
				"subtotal": 350,
				"tax": 0,
				"shipping": 0,
				"shipping_discount": 0
			}
		},
		"promotions": [
			{
				"type": "CMR",
				"amount": 320,
				"currency": "CLP"
			},
			{
				"type": "BANCO",
				"amount": 320,
				"currency": "CLP"
			}
		]
	},
	"additional_attributes": {},
	"redirect_urls": {
		"return_url": "https://comercio.net/redirections/payment_success.html",
		"cancel_url": "https://comercio.com"
	}
}
```

 **Detalle de las URLs generadas:**


__self:__ desde esta URL puedes consultar la información de la intención de pago.

__approval_url:__ desde esta URL se levanta una interfaz web que permite al cliente autorizar el pago.

__qr_code:__ esta URL genera automáticamente un código QR para autorizar un pago.

__qr_code_plain:__ esta URL entrega la data del código QR, para que el comercio pueda usar su propia librería de QR.

__self_by_merchant_unique_id:__ desde esta URL puedes consultar la información de la intención de pago utilizando el código único de transacción enviado al crear la intención de pago (merchant_unique_id).

__refund:__ desde esta URL se puede realizar la anulación (parcial o total) del pago.


**Response**
```markdown
{
    "intent": "sale",
    "state": "created",
    "_id": "60f75ba528c0f40039e4659d",
    "payment_method": "WALLET_QR",
    "transaction": {
        "purchase_order": "0",
        "invoice_type": "BOLETA",
        "store_id": "15",
        "terminal_id": "10",
        "description": "Articulos Electronicos",
        "soft_descriptor": "WALLET-QR-PAYMENT",
        "merchant_unique_id": "1626823589",
        "reconciliation_id": "60f75ba528c0f40039e4659d",
        "item_list": {
            "shipping_method": "DIGITAL",
            "items": [
                {
                    "sku": "TVLG43S",
                    "name": "TVLG43",
                    "description": "Tv LG 43",
                    "quantity": 1,
                    "price": 80,
                    "tax": 0
                },
                {
                    "sku": "TVLG55S",
                    "name": "TVLG43",
                    "description": "Tv LG 55",
                    "quantity": 1,
                    "price": 100,
                    "tax": 0
                },
                {
                    "sku": "TVLG60S",
                    "name": "TVLG60",
                    "description": "Tv LG 60",
                    "quantity": 1,
                    "price": 120,
                    "tax": 0
                }
            ],
            "shipping_address": {
                "line1": "Dirección Av. Irarrazabal",
                "city": "Santiago",
                "country_code": "CL",
                "phone": "+56 9 8762 1244",
                "recipient_name": "Jose Torres"
            }
        },
        "amount": {
            "currency": "CLP",
            "total": 350,
            "details": {
                "subtotal": 350,
                "tax": 0,
                "shipping": 0,
                "shipping_discount": 0
            },
            "installments_number": 1,
            "deferred_months_number": 0
        },
        "promotions": [
            {
                "type": "CMR",
                "amount": 320,
                "currency": "CLP"
            },
            {
                "type": "BANCO",
                "amount": 320,
                "currency": "CLP"
            }
        ]
    },
    "redirect_urls": {
        "return_url": "https://comercio.net/redirections/payment_success.html",
        "cancel_url": "https://comercio.com"
    },
    "application": "5e5e92d6b8f6a5001602123a",
    "invoice_number": "IP-16268235894845181",
    "create_time": "2021-07-20T23:26:29.484Z",
    "update_time": "2021-07-20T23:26:29.484Z",
    "links": [
        {
            "href": "https://payments-wallet-qa.fif.tech/checkout/payments/60f75ba528c0f40039e4659d",
            "rel": "self",
            "security": [
                "ApiKey"
            ],
            "method": "GET"
        },
        {
            "href": "https://payments-wallet-qa.fif.tech/checkout/cl/payments/gateways/wallet/qr/60f75ba528c0f40039e4659d/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://payments-wallet-qa.fif.tech/checkout/payments/60f75ba528c0f40039e4659d/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://payments-wallet-qa.fif.tech/checkout/payments/1626823589/merchant-unique-id",
            "rel": "self_by_merchant_unique_id",
            "security": [
                "ApiKey"
            ],
            "method": "GET"
        },
        {
            "href": "https://payments-wallet-qa.fif.tech/checkout/payments/gateways/wallet/qr/60f75ba528c0f40039e4659d/qr",
            "rel": "qr_code",
            "method": "GET"
        },
        {
            "href": "https://payments-wallet-qa.fif.tech/checkout/payments/gateways/wallet/qr/60f75ba528c0f40039e4659d/qr-plain",
            "rel": "qr_code_plain",
            "method": "GET"
        },
        {
            "href": "https://payments-wallet-qa.fif.tech/checkout/payments/gateways/wallet/qr/60f75ba528c0f40039e4659d/refund",
            "rel": "refund_method",
            "method": "POST"
        }
    ],
    "expiration_date": "2021-07-20T23:27:29.521Z",
    "short_transaction_code": "71583283",
    "long_transaction_code": "2021072071583283",
    "fpay_merchant_id": "PP5e5e92d6b8f6a5001602123a",
    "id": "60f75ba528c0f40039e4659d"
}
```


**Video**

{{< youtube "_4o17G9y8bQ" >}}

&nbsp;
&nbsp;

### Generar QR
Cada QR esta asociado a un store y a un terminal único por comercio, con esta información se genera y se entrega un banner físico con la imagen QR al comercio, este banner debe ser colocado en el POS de cara al cliente.&nbsp;

Una vez escaneado el código QR, el cliente realizará el pago desde su aplicación “Fpay”. En caso de que el cliente tenga problemas para scanear el código QR, podrá optar por utilizar el código alternativo que podrá visualizar debajo de la imagen del código QR

**Informacion requerida para generar el QR fisico**

El comercio debe suministrar la informacion referente a la identificacion de cada local y los POS que tenga habilitados para el pago QR:

| CAMPO | DESCRIPCION |
| :--- | :--- |
| store_id | Identificación de la tienda |
| terminal_id |Identificador del POS |


 **Banner con QR**


{{< picture "qr_estatico.png" "Compose Logo" >}}

&nbsp;
&nbsp;

### Consultar el estado

Para consultar el estado de la transacción mediante API, llamando a la URL self obtenida en la respuesta de la intención de pago de la siguiente forma. Se debe establecer un tiempo máximo de espera para recibir la notificación y una vez pasado este tiempo realizar un self para confirmar el estado de la transacción, esto previendo cualquier error de comunicación que impida la notificación al comercio.

>  Puedes integrar esta API en paralelo con un WeebHook.

| Estado | Definicion |
| :--- | :--- |
| created | Estado inicial de una intención |
| expired |La intención pasó su fecha de expiración y ya no puede ser utilizada |
| paid | La intención fue pagada exitósamente |
| rejected |La intención se intentó pagar, pero el pago fue rechazado |
| partially_refunded | Tiene al menos una devolución asociada por monto menor al total de la compra |
| refunded |La devolución se completó exitosamente por el monto total de la compra |
| reversed | La intención fue pagada pero se realizó una reversa del pago |

**Header**
```markdown
Content-Type:application/json
Authorization:Basic {{client_id}}:{{client_secret}}
FP-Flow-Country:cl
```

**URL**
```markdown
https://payments-wallet-qa.fif.tech/checkout/payments/123456
```

&nbsp;
&nbsp;

### Devoluciones
Con la url refund_method generada en la respuesta de la intención de pago.
Se puede hacer anulación total o múltiples anulaciones parciales hasta alcanzar el total de la compra.

| Estado | Definicion |
| :--- | :--- |
| partially_refunded | Tiene al menos una devolución asociada por monto menor al total de la compra |
| refunded |La devolución se completó exitosamente por el monto total de la compra |



**Header**
```markdown
Content-Type:application/json
Authorization:Basic {{client_id}}:{{client_secret}}
FP-Flow-Country:cl
```

**URL**
```markdown
https://payments-wallet-qa.fif.tech/checkout/payments/gateways/wallet/qr/60f8cd1e7d98ba28ab7385ed/refund
```

**Body**
```markdown
{
	    "refunded_amount":320,
        "refund_merchant_unique_id":"{{$timestamp}}",
        "operation_type":"003820",
         "items": [
        {
          "thumbnail": "http://notfound404.cl/some.jpg",
          "sku": "TVLG43S",
          "name": "TVLG43",
          "description": "Tv LG 43",
          "quantity": 1,
          "price": 400,
          "tax": 0,
          "_id": "5a7a14343df88b000fdac92a"
        }
      ]
        
    }
```

&nbsp;
&nbsp;

### Reversa
Para ejecutar la Reversa de la Captura debes invocar la URL silent_charge_void . Esta url sólo puede ser invocada durante el mismo día de la operación antes de la conciliación. El resultado será un mensaje confirmando la reversa exitosa y el estado de la intención de pago esta será “reversed”. &nbsp;

Reversa Técnica: Corresponde a la eliminación de una Transacción con lo cual no queda movimiento financiero registrado, es conocida como Void.

**Header**
```markdown
Content-Type:application/json
Authorization:Basic {{client_id}}:{{client_secret}}
FP-Flow-Country:cl
```

**URL**
```markdown
https://payments-wallet-qa.fif.tech/checkout/payments
```

**Body**
```markdown
{
        "transaction": {
        "merchant_unique_id":"1626919071"
}
}
```
&nbsp;
&nbsp;

### Diagrama de flujo

{{< picture "diagrama_estaticoqr.png" "Compose Logo" >}}

&nbsp;
&nbsp;


### Presentacion Fpay (Descarga)

# [Clic aqui.](https://docs.google.com/presentation/d/1xnqIqLHJdKG-moE-RJyDM8n5vKsS5hpqTFzWa0BqduE/edit?usp=sharing)

&nbsp;
&nbsp;

### Postman collection

Puedes copiar la siguiente URL e importar una collection desde Postman:


URL: https://www.getpostman.com/collections/a8c0fe7841e021034542





