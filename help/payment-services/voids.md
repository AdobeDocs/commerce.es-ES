---
title: Vacíos
description: Las anulaciones le permiten liberar los fondos en una cuenta de tarjeta de crédito o débito que están bloqueados o mantenidos a un lado por una autorización para el importe de una compra.
exl-id: 029a7038-2812-46ce-b188-929a7a758d89
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Vacíos

[!DNL Payment Services] admite la funcionalidad existente de Commerce para anular transacciones. Una anulación libera fondos en una cuenta de tarjeta de crédito o débito que están siendo retenidos por una autorización para el importe de compra. Las transacciones sólo se pueden anular si aún no se ha registrado el pago.

* Si tu tienda está [configurada](https://experienceleague.adobe.com/es/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} para autorizar solo (no capturar) fondos en el punto de venta, una compra en tu tienda resultará en un pedido con un estado `Processing` en el administrador de Commerce.

* También puede [cancelar un pedido](https://experienceleague.adobe.com/es/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"} que no esté facturado. Las autorizaciones no capturadas también se anulan como parte de ese proceso de cancelación.

>[!NOTE]
>
>La cancelación de un pedido también produce un vacío, pero la anulación de un pedido no déclencheur una cancelación.

Para obtener más información sobre los pasos básicos por los que pasa un pedido, consulte el tema [Flujo de trabajo de pedidos](https://experienceleague.adobe.com/es/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"} en la guía del usuario principal.

Para obtener más información sobre la funcionalidad void y cómo anular una transacción de pedido, consulte [Procesar un pedido](https://experienceleague.adobe.com/es/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"} en la guía del usuario principal.
