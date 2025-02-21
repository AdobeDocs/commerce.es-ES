---
title: Datos disponibles
description: Utilice los datos de informes financieros para reconciliar los informes con sistemas que no sean de Commerce.
role: User
level: Intermediate
feature: Payments, Checkout, Data Import/Export
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '152'
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
