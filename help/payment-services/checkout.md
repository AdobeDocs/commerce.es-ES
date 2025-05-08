---
title: Cierre de compra en  [!DNL Payment Services]
description: Personaliza  [!DNL Payment Services] el pago y envío para adaptarlo a las necesidades de tus clientes.
feature: Payments, Checkout, Paas, Saas
exl-id: 47df165f-2145-4e0e-b272-54b8e768cf19
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# Cierre de compra en [!DNL Payment Services]

Puede configurar el cierre de compra de Adobe Commerce [!DNL Payment Services] para que se adapte mejor a sus compradores. Las funciones tales como [anulación automática de pedidos](#order-auto-voided-if-error) y [depósito de tarjetas de crédito](#credit-card-vaulting) garantizan que tus compradores tengan una experiencia de usuario sin problemas.

## Pedido anulado automáticamente en caso de error

Si se produce un error durante la desprotección, [!DNL Payment Services] anula o cancela automáticamente el pedido.

Aparece un mensaje de error en la página de cierre de compra del comprador. El mensaje puede variar.

![Error al comprobar](assets/user-checkout-error.png "Error al desproteger"){width="600" zoomable="yes"}

También se muestra un comentario sobre el pedido cancelado en el Administrador para un [pedido](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/order-management/orders/orders.html?lang=es) específico.

![Comentario de pedido cancelado en el administrador del pedido](assets/admin-checkout-error.png "Comentario de pedido cancelado en el administrador del pedido"){width="600" zoomable="yes"}

Si un comprador obtiene autorización para un pedido, pero el pedido no se creó ni se convirtió en un `Capture`, el pedido se anula automáticamente. Este proceso garantiza que no se reserve crédito en la tarjeta de crédito del comprador y evita la tarifa del proveedor de pagos que se produce cuando la autorización se anula al final del período estándar de 29 días.

>[!NOTE]
>
>La anulación automática de pedidos solo se produce cuando el cliente utiliza un método de pago establecido en el modo `Authorize`, no en el modo `Authorize and Capture`.

## Cierre de compra desde la página del producto

Cuando un cliente cierra la compra directamente desde la página del producto, utilizando los botones PayPal o [!DNL Pay Later], solo se compra el artículo representado en la página del producto actual. Los artículos que ya residen en el carro de compras del cliente no se agregan al flujo de cierre de compra y no se compran.

Esta función permite al cliente adquirir rápidamente el artículo que está viendo en ese momento, conservando los artículos que había añadido anteriormente al carro de compras.
Si el cliente cancela el pedido, el artículo de la página de producto actual se agrega al carro de compras del cliente.

Cuando un cliente introduce el flujo de cierre de compra desde la página del producto, la página de cierre de compra se simplifica: la vista solo muestra datos y opciones relacionados con el pedido.

## Bóveda de tarjetas de crédito

Los compradores pueden guardar la información de su tarjeta de crédito para futuras compras en el sitio web (cualquier tienda dentro de la cuenta del mismo comerciante).

Consulte [Avalúo de tarjetas de crédito](vaulting.md) para obtener más información
