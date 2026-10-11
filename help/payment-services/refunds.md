---
title: Reembolsos
description: Cree reembolsos para [!DNL Payment Services] pedidos en el administrador como parte del proceso de abono.
exl-id: 2b3721a1-9c9d-4e3f-ab7d-5bd61573dcb4
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
source-wordcount: '305'
ht-degree: 0%
---
# Reembolsos

Los reembolsos de [!DNL Payment Services] pedidos se crean en el administrador como parte del proceso de abono. Una nota de abono es un documento que muestra el importe que se debe al cliente, para un reembolso completo o parcial, que se puede aplicar a una compra o reembolsar directamente al cliente. Solo se pueden emitir notas de abono para pedidos que se hayan [facturado](https://experienceleague.adobe.com/es/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}.

Consulte [Notas de crédito](https://experienceleague.adobe.com/es/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos){target="_blank"} en nuestra guía de usuario principal para obtener más información y para aprender a emitir e imprimir notas de crédito.

Para pedidos procesados con PayPal o una tarjeta de crédito, puede:

* Devolver el importe total del pedido
* Devolución de un importe parcial de un pedido (o de varios importes parciales)
* Devolución de una cantidad inferior al valor de un artículo de pedido específico

Consulte [Emisión de una nota de crédito](https://experienceleague.adobe.com/es/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create){target="_blank"} en nuestra guía de usuario principal para obtener más información.

>[!NOTE]
>
>Se produce un error en los pedidos procesados con PayPal o con tarjeta de crédito si intenta reembolsar parcialmente un pedido por un importe superior al importe del pedido restante (importe original menos el total de los reembolsos existentes) o si emite un reembolso por un importe superior al importe total del pedido.

La configuración de [!UICONTROL Payment Action] de su configuración de [!UICONTROL Payment Settings] (ya sea `Authorize` o `Authorize and Capture`) determina el [flujo de trabajo básico de reembolso](https://experienceleague.adobe.com/es/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos#refund-workflow){target="_blank"} para los pedidos.

Consulte la [sección de configuración de la acción de pago](https://experienceleague.adobe.com/es/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create#payment-action-setting){target="_blank"} de _Emisión de una nota de crédito_ para obtener más información.
