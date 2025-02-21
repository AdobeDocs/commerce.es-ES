---
title: Reembolsos
description: Cree reembolsos para  [!DNL Payment Services] pedidos en el administrador como parte del proceso de abono.
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Reembolsos

Los reembolsos de [!DNL Payment Services] pedidos se crean en el administrador como parte del proceso de abono. Una nota de abono es un documento que muestra el importe que se debe al cliente, para un reembolso completo o parcial, que se puede aplicar a una compra o reembolsar directamente al cliente. Solo se pueden emitir notas de abono para pedidos que se hayan [facturado](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}.

Consulte [Notas de crédito](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos){target="_blank"} en nuestra guía de usuario principal para obtener más información y para aprender a emitir e imprimir notas de crédito.

Para pedidos procesados con PayPal o una tarjeta de crédito, puede:

* Devolver el importe total del pedido
* Devolución de un importe parcial de un pedido (o de varios importes parciales)
* Devolución de una cantidad inferior al valor de un artículo de pedido específico

Consulte [Emisión de una nota de crédito](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create){target="_blank"} en nuestra guía de usuario principal para obtener más información.

>[!NOTE]
>
>Se produce un error en los pedidos procesados con PayPal o con tarjeta de crédito si intenta reembolsar parcialmente un pedido por un importe superior al importe del pedido restante (importe original menos el total de los reembolsos existentes) o si emite un reembolso por un importe superior al importe total del pedido.

La configuración de [!UICONTROL Payment Action] de su configuración de [!UICONTROL Payment Settings] (ya sea `Authorize` o `Authorize and Capture`) determina el [flujo de trabajo básico de devolución de fondos](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos#refund-workflow){target="_blank"} para los pedidos.

Consulte la [sección de configuración de la acción de pago](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create#payment-action-setting){target="_blank"} de _Emisión de una nota de crédito_ para obtener más información.
