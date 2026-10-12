---
title: Rastreo de los envíos en [!DNL Payment Services]
description: Personaliza [!DNL Payment Services] envíos e información de seguimiento mostrados en el panel de control del comerciante de PayPal.
feature: Payments, Paas, Saas
exl-id: 17aede1f-56ae-441a-b723-3193e865e469
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
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
source-wordcount: '228'
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
