---
title: Vacíos
description: Las anulaciones le permiten liberar los fondos en una cuenta de tarjeta de crédito o débito que están bloqueados o mantenidos a un lado por una autorización para el importe de una compra.
exl-id: 029a7038-2812-46ce-b188-929a7a758d89
feature: Payments, Checkout, Paas, Saas
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%
---
# Vacíos

[!DNL Payment Services] admite la funcionalidad existente de Commerce para anular transacciones. Una anulación libera fondos en una cuenta de tarjeta de crédito o débito que están siendo retenidos por una autorización para el importe de compra. Las transacciones sólo se pueden anular si aún no se ha registrado el pago.

* Si tu tienda está [configurada](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} para autorizar solo (no capturar) fondos en el punto de venta, una compra en tu tienda resultará en un pedido con un estado `Processing` en el administrador de Commerce.

* También puede [cancelar un pedido](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"} que no esté facturado. Las autorizaciones no capturadas también se anulan como parte de ese proceso de cancelación.

>[!NOTE]
>
>La cancelación de un pedido también produce un vacío, pero la anulación de un pedido no déclencheur una cancelación.

Para obtener más información sobre los pasos básicos por los que pasa un pedido, consulte el tema [Flujo de trabajo de pedidos](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"} en la guía del usuario principal.

Para obtener más información sobre la funcionalidad void y cómo anular una transacción de pedido, consulte [Procesar un pedido](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"} en la guía del usuario principal.
