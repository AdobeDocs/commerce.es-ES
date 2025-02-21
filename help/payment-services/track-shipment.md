---
title: Rastreando sus envíos en  [!DNL Payment Services]
description: Personaliza  [!DNL Payment Services] la información de envíos y seguimiento mostrada en el panel de control del comerciante de PayPal.
feature: Payments
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Rastreo de los envíos en [!DNL Payment Services]

[!DNL Payment Services] permite a los comerciantes ver la información de seguimiento de un envío en su panel de comerciantes de PayPal.

Consulte el tema [envíos](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/shipments){target=_blank} para obtener más información sobre la cuadrícula de envíos de Adobe Commerce.

## Cómo funciona el seguimiento de su envío

Esta funcionalidad depende de si el pedido se ha facturado, ya que PayPal debe recibir un `capture_id` para procesar la información de seguimiento. Si un comerciante envía sus productos antes de la captura, la información de seguimiento no se envía a PayPal.

>[!NOTE]
>
> Se recomienda crear un envío por número de seguimiento, asociando los artículos correctos con el envío.

## Adición del número de seguimiento

Las siguientes instrucciones lo guiarán a través del proceso para crear un envío en Adobe Commerce con [!DNL Payment Services]:

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL Orders]**.

1. En la columna **[!UICONTROL Action]** del orden seleccionado, haga clic en **[!UICONTROL View]**.

1. Haga clic en **[!UICONTROL Ship]**.

1. Desplácese hasta el bloque **[!UICONTROL Payment & Shipping Method]** y haga clic en **[!UICONTROL Add Tracking Number]** en **[!UICONTROL Shipping Information]**.

1. Establezca **[!UICONTROL Carrier]**.

1. Para realizar el seguimiento del envío, escriba **[!UICONTROL Title]** y **[!UICONTROL Number]**

1. Haga clic en **[!UICONTROL Submit Shipment]**.

>[!NOTE]
>
> También puedes utilizar un módulo de envío para introducir la información del número de seguimiento. Asegúrese de que el módulo de envío está guardando la información del número de seguimiento en el campo `tracking_number`.

### Compatibilidad con terceros

Cualquier extensión de terceros es compatible con la funcionalidad cuando se crea una entidad de envío mediante [Commerce API](https://developer.adobe.com/commerce/webapi/rest/attributes/#ShipmentRepositoryInterface){target=_blank}.
