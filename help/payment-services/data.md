---
title: Datos disponibles
description: Utilice los datos de informes financieros para reconciliar los informes con sistemas que no sean de Commerce.
role: User
level: Intermediate
exl-id: dbf41ce9-01f9-45d0-b651-e4c499e83822
feature: Payments, Checkout, Data Import/Export, Paas, Saas
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%
---
# Datos disponibles

Algunos datos de pedidos y pagos están disponibles para que pueda coordinar la creación de informes financieros de Adobe Commerce en sistemas externos.

## Reconciliación con el sistema ERP

Puede reconciliar los informes financieros de Adobe Commerce con un sistema que no sea de planificación de recursos empresariales (ERP) de Adobe mediante el ID de incremento asociado a un pedido específico.

Cuando Payment Services envía el pedido de Commerce a PayPal, el identificador de incremento se incluye como `custom_id` _y_ en `invoice_id` (que también contiene una cadena aleatoria después de `increment_id`).

Los ID son fácilmente accesibles tanto en el detalle de la actividad comercial para un pago como en el webhook de PayPal.

`invoice_id` y `custom_id` se muestran cerca de la parte inferior del detalle de actividad de comerciante para un pago:

![`custom_id` en detalle de actividad de comerciante](assets/merchant-activity-ids.png){width="600" zoomable="yes"}

`custom_id` y `invoice_id` en los detalles del webhook de PayPal:

```json
   ...
   {
    "id": "4E855005GK253170H",
    "intent": "AUTHORIZE",
    "status": "COMPLETED",
    "payment_source": {
        ...
    },
    "purchase_units": [
        {
            ...
            "custom_id": "000001322",
            "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
            ...
            "payments": {
                "authorizations": [
                    {
                       ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ],
                "captures": [
                    {
                        ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ]
            }
        }
    ],
    "payer": {
        ...
    },
    "create_time": "2022-09-12T14:59:01Z",
    "update_time": "2022-09-12T14:59:45Z",
    "links": [
        ...
    ]
}
   ...
```

Consulte la documentación de las API de REST de PayPal para obtener más información:

* [`purchase_unit`, en el cual residen `custom_id` y `invoice_id`](https://developer.paypal.com/docs/api/orders/v2/#definition-purchase_unit)
* [Mostrar detalles del pedido](https://developer.paypal.com/docs/api/orders/v2/#orders_get)
