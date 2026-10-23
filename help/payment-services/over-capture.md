---
title: Capturar En Exceso
description: Obtenga información sobre los requisitos de captura excesiva y la configuración de la extensión de servicios de pago.
role: Admin, User
level: Intermediate
feature: Payments, Paas
source-git-commit: d2bcc58f34af50f26d4a4f082e5b3fc30089ab58
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%
---
# Capturar En Exceso

La captura en exceso permite a los comerciantes elegibles con un acuerdo de captura en exceso de PayPal capturar más de la cantidad autorizada originalmente al facturar un pedido. Por ejemplo, el importe final podría aumentar debido a ajustes basados en el peso o cambios en los costes de material entre la autorización y el cumplimiento.

PayPal determina el límite de captura en exceso de cada cuenta de comerciante. Al habilitar la captura excesiva en [!DNL Payment Services] no se establece un acuerdo ni se aumenta el límite aprobado por PayPal.

>[!NOTE]
>
>En este tema se describe la captura excesiva en la extensión [!DNL Payment Services]. Para [!DNL Adobe Commerce as a Cloud Service], consulte [Cantidades de captura personalizadas](https://experienceleague.adobe.com/es/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts) para conocer los requisitos de disponibilidad y habilitación por separado.

## Requisitos previos

Antes de habilitar la captura excesiva:

* Overcapture solo está disponible en [!DNL Payment Services] 2.17.0 o posterior.
* La captura excesiva solo está disponible para empresas con sede en Estados Unidos. Los [requisitos de captura excesiva de PayPal (PSD2)](https://www.paypal.com/us/cshelp/article/overcapture-requirements-psd2-help954) también se aplican a los comerciantes estadounidenses que venden a compradores de PayPal en el Espacio Económico Europeo (EEE).
* La captura excesiva no está disponible para métodos de pago alternativos (APM).
* Obtenga un acuerdo de captura excesiva con PayPal y confirme el límite aprobado para su cuenta de comerciante con el administrador de cuentas de PayPal.
* Establece **[!UICONTROL Payment Action]** del método de pago en `Authorize`. La captura excesiva se aplica a los pedidos autorizados capturados más tarde durante la facturación, no a los pedidos capturados automáticamente con `Authorize and Capture`. Ver [Set [!DNL Payment Services] como método de pago](production.md#set-payment-services-as-payment-method).

## Habilitar captura excesiva

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. En el panel izquierdo, expanda **[!UICONTROL Sales]** y elija **[!UICONTROL Payment Methods]**.
1. Seleccione el sitio web que desea configurar mediante el selector de ámbito de tienda.
1. Expanda la sección _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. En la sección _[!UICONTROL Payment Services]_, expanda la sección&#x200B;_[!UICONTROL General Configuration]_.
1. Establezca **[!UICONTROL Over Capture Enabled]** en `Yes`.
1. Haga clic en **[!UICONTROL Save Config]** para guardar los cambios.
1. Vaya a **[!UICONTROL System]** > **[!UICONTROL Cache Management]** y, a continuación, haga clic en **[!UICONTROL Flush Cache]** para actualizar todas las cachés no válidas.

## Capturar un pago autorizado

La captura excesiva se produce durante la facturación en el administrador. La cantidad de captura solicitada debe estar dentro del límite aprobado por PayPal para tu cuenta de comerciante. Ver [Crear una factura](https://experienceleague.adobe.com/es/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice) para el flujo de trabajo de facturación estándar.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL Orders]**.
1. Abra un pedido con un pago autorizado que aún no se haya capturado.
1. Haga clic en **[!UICONTROL Invoice]**.
1. En el campo Cantidad de captura personalizada, introduzca la cantidad total que desea capturar. Por ejemplo, si la cantidad autorizada es USD 100 y el cargo final acordado es USD 110, escriba `110`, no `10`. El importe solicitado debe estar dentro del límite aprobado por PayPal.
1. Seleccione la captura en línea de la factura para solicitar el pago a través del proveedor de pagos.
1. Revise la factura y haga clic en **[!UICONTROL Submit Invoice]**.

### Capturar mediante la API de facturas

Usar el extremo estándar [Crear una factura](https://developer.adobe.com/commerce/webapi/rest/tutorials/orders/order-create-invoice):

```http
POST /rest/<store_code>/V1/order/<orderId>/invoice
```

Utilice el código de tienda del pedido y el ID interno del pedido. Autentique con un administrador autorizado o un token de integración y establezca `Content-Type: application/json`.

El siguiente ejemplo de carga útil solicita una factura completa con captura en línea de USD 110 para un pedido autorizado para USD 100, siempre que el acuerdo de PayPal del comerciante permita esa cantidad:

```json
{
  "capture": true,
  "notify": false,
  "arguments": {
    "extension_attributes": {
      "custom_capture_amount": 110
    }
  }
}
```

En este ejemplo:

1. `capture` solicita captura en línea.
1. `notify` controla si Commerce envía el correo electrónico de notificación de factura.
1. `custom_capture_amount` es la cantidad final que se va a capturar, no el aumento sobre la cantidad autorizada.

## Solución de problemas de una captura rechazada

Si PayPal rechaza una solicitud de captura excesiva:

* Confirme que hay un acuerdo de captura en exceso activo para la cuenta de comerciante de PayPal utilizada para el pago.
* Compruebe que la cantidad solicitada se encuentra dentro del límite aprobado. Si supera el límite, solicita una cantidad inferior o ponte en contacto con el administrador de cuentas de PayPal para hablar sobre un aumento.
