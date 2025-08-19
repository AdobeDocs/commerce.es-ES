---
title: Configuración de [!DNL Payment Services]
description: Después de la instalación, puede configurar  [!DNL Payment Services]  en el Administrador en la configuración de la tienda.
role: Admin, User
level: Intermediate
exl-id: e1a3269d-bdf9-4b0f-972f-e8a0ef469503
feature: Payments, Checkout, Configuration
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '2568'
ht-degree: 0%

---

# Configuración de [!DNL Payment Services]

Puede personalizar [!DNL Payment Services] según sus necesidades con opciones de configuración útiles en el Administrador.

Cuando configura [!DNL Payment Services] para [!DNL Adobe Commerce] y [!DNL Magento Open Source] en el administrador, esas configuraciones se aplican únicamente al entorno establecido en el campo _[!UICONTROL Method]_&#x200B;de&#x200B;_[!UICONTROL General Configuration]_. Cualquier cambio que realice en los campos de configuración es independiente de cambiar la selección de _[!UICONTROL Method]_; si cambia el método, las selecciones no se restablecerán.

## Configuración general

Puede habilitar [!DNL Payment Services] para su tienda y su _[!UICONTROL Merchant Location]_, y habilitar la prueba de zona protegida o los pagos activos en la sección&#x200B;_[!UICONTROL General Configuration]_.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. En el panel izquierdo, expanda **[!UICONTROL Sales]** y elija **[!UICONTROL Payment Methods]**.
1. Establezca el campo _[!UICONTROL Merchant Country]_&#x200B;en&#x200B;_[!UICONTROL Merchant Location]_. Si no se especifica un(a) _[!UICONTROL Merchant Country]_, se utiliza el(la)_[!UICONTROL Default Country]_ de la configuración general.
1. Expanda la sección _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;para tener acceso a la sección&#x200B;_[!UICONTROL [!DNL Payment Services]]_.
1. En la sección _[!UICONTROL [!DNL Payment Services]]_, expanda la sección&#x200B;_[!UICONTROL General Configuration]_.
1. Para **Habilitar**, establézcalo en `Yes` para habilitar [!DNL Payment Services] en tu tienda.
1. Para **Método**, establézcalo en `Sandbox` si todavía estás probando [!DNL Payment Services] para tu tienda o `Production` si estás listo para habilitar los pagos activos.
1. Los valores de **[!UICONTROL Payment Services Sandbox ID]** y **[!UICONTROL Payment Services Production ID]** se rellenan automáticamente una vez que configura [Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/user-guides/integration-services/saas){target=_blank} y visita el panel [!DNL Payment Services] por primera vez. Haga esto para finalizar la incorporación para su zona protegida o entornos de producción. Estos valores asocian su ID de SaaS a [!DNL Payment Services].

   >[!WARNING]
   >
   > Si necesita cambiar el ID del espacio de datos en Commerce Services Connector, debe restablecer su ID de [!DNL Payment Services]. Haga clic en **Restablecer ID de servicios de pago** para restablecer el ID de la zona protegida. Si restablece su ID de zona protegida [!DNL Payment Services], debe incorporarse de nuevo.

1. PayPal proporciona automáticamente sus valores de **[!UICONTROL PayPal Merchant ID]** y **[!UICONTROL PayPal Merchant Status]** cuando visita el panel de [!DNL Payment Services] por primera vez.
1. Para **Descriptor suave** (valores personalizados que se muestran en los extractos bancarios de las transacciones de los clientes para delimitar entre tiendas/marcas/catálogos), agregue el texto personalizado (hasta 22 caracteres) en el campo de texto, reemplazando `Soft descriptor` o el valor existente.
1. Haga clic en **[!UICONTROL Save Config]** para guardar los cambios.
1. Vaya a **[!UICONTROL System]** > **[!UICONTROL Cache Management]** y, a continuación, haga clic en **[!UICONTROL Flush Cache]** para actualizar todas las cachés no válidas.

![Vista destacada de la solución Adobe](assets/config-view-all.png){width="700" zoomable="yes"}

### Opciones de configuración

| Campo | Ámbito | Descripción |
|---|---|---|
| [!UICONTROL Enable] | sitio web | Habilite o deshabilite [!DNL Payment Services] para su sitio web. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Method] | vista de tienda | Defina el método o el entorno para su tienda. Opciones: [!UICONTROL Sandbox] / [!UICONTROL Production] |
| [!UICONTROL Payment Services Sandbox ID] | vista de tienda | El ID de comerciante de la zona protegida, que se genera automáticamente durante la incorporación a la zona protegida. |
| [!UICONTROL Payment Services Production ID] | vista de tienda | Su ID de comerciante de producción, que se genera automáticamente durante la incorporación de la producción (en directo). |
| [!UICONTROL PayPal Merchant ID] | vista de tienda | Tu ID único de cuenta de PayPal Merchant, generado al crear tu cuenta de PayPal. |
| [!UICONTROL PayPal Merchant Status] | vista de tienda | Estado de tu ID de comerciante de PayPal. |
| [!UICONTROL Soft Descriptor] | sitio web o vista de tienda | Añada un descriptor temporal a sus sitios web y vistas de tiendas para añadir información a las transacciones de clientes que delimitan marcas, tiendas o líneas de productos. |

## [!UICONTROL Credit Card Fields]

Las opciones de pago de [!UICONTROL Credit Card Fields] proporcionan un pago seguro y sencillo para los métodos de pago con tarjeta de crédito o débito.

Consulte [Opciones de pago](payments-options.md#paypal-smart-buttons) para obtener más información.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. En el panel izquierdo, expanda **[!UICONTROL Sales]** y elija **[!UICONTROL Payment Methods]**.
1. Expanda la sección _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. En la sección _[!UICONTROL Payment Services]_, expanda la sección&#x200B;_[!UICONTROL Credit Card Fields]_.
1. Para **[!UICONTROL Title]**, escriba texto (si es necesario) para cambiar el nombre del método de pago como se muestra durante el cierre de compra.
1. Para [establecer la acción de pago](production.md#set-payment-services-as-payment-method), seleccione **[!UICONTROL Authorize]** o **Autorizar y capturar**.
1. Para priorizar un método de pago en la página de cierre de compra, proporcione un valor `Numeric Only` en el campo **[!UICONTROL Sort order]**.
1. Para **[!UICONTROL Show on checkout page]**, elija `Yes` para habilitar los campos de tarjeta de crédito en la página de pago y envío.
1. Para **[!UICONTROL Vault Enabled]**, elija `Yes` para habilitar el depósito de tarjetas de crédito para el cierre de compra.
1. Para **[!UICONTROL Vault Enabled in Admin]**, elija `Yes` para permitir que el comerciante cree pedidos para clientes que usen su tarjeta de crédito abovedada.
1. Para habilitar **[!UICONTROL 3D Secure authentication]** (`Off` de forma predeterminada), elija `Always` o `When required`.
1. Para **[!UICONTROL Debug Mode]**, elija `Yes` para habilitar el modo de depuración o `No` para deshabilitarlo.
1. Haga clic en **[!UICONTROL Save Config]** para guardar los cambios.
1. Vaya a **[!UICONTROL System]** > **[!UICONTROL Cache Management]** y, a continuación, haga clic en **[!UICONTROL Flush Cache]** para actualizar todas las cachés no válidas.

### Opciones de configuración

| Campo | Ámbito | Descripción |
|---|---|---|
| [!UICONTROL Title] | vista de tienda | Añada el texto que se mostrará como título para esta opción de pago en la vista Método de pago durante el cierre de compra. Opciones: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | sitio web | La [acción de pago](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html) para el método de pago especificado. Opciones: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | vista de tienda | El orden de clasificación del método de pago especificado en la página de pago. Valor `Numeric Only` |
| [!UICONTROL Show on checkout page] | sitio web | Habilite o deshabilite los campos de tarjeta de crédito en la página de cierre de compra. Opciones: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled] | vista de tienda | Habilitar o deshabilitar el depósito de [tarjetas de crédito](vaulting.md). Opciones: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled in Admin] | vista de tienda | Habilite o deshabilite la capacidad para que [el comerciante complete los pedidos de los clientes del administrador](vaulting.md) mediante un método de pago abovedado. Opciones: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL 3D Secure authentication] | sitio web | Habilitar o deshabilitar la [autenticación segura de 3DS](security.md#3ds). Opciones: [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | sitio web | Habilite o deshabilite el modo de depuración. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Fastlane]

[[!DNL Fastlane by PayPal]](https://www.paypal.com/us/cshelp/article/what-is-fastlane-by-paypal-help1096) es una forma rápida y sencilla de pagar en línea de forma segura. Durante el **pago y envío de los invitados**, puedes guardar de manera segura tu tarjeta y los detalles de envío para realizar compras aún más rápidas en el futuro.

Consulte [Opciones de pago](payments-options.md#fastlane-button) para obtener más información.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. En el panel izquierdo, expanda **[!UICONTROL Sales]** y elija **[!UICONTROL Payment Methods]**.
1. Expanda la sección _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. En la sección _[!UICONTROL Payment Services]_, expanda la sección&#x200B;_[!UICONTROL Fastlane]_.
1. Para habilitarlo, seleccione `Yes` para **[!UICONTROL Enable Fastlane]** (`No` lo deshabilita).

   >[!NOTE]
   >
   > Si [!UICONTROL Fastlane] está habilitado, la opción de pago [!UICONTROL Credit Card Fields] está deshabilitada.

1. Para **[!UICONTROL Title]**, escriba texto (si es necesario) para cambiar el nombre del método de pago como se muestra durante el cierre de compra. El título predeterminado es `Credit Card (via Fastlane)`
1. Para [establecer la acción de pago](production.md#set-payment-services-as-payment-method), seleccione **[!UICONTROL Authorize]** o **Autorizar y capturar**.
1. Para priorizar un método de pago en la página de cierre de compra, proporcione un valor `Numeric Only` en el campo **[!UICONTROL Sort order]**.
1. Especifique si la marca [!UICONTROL Fastlane] está habilitada durante el cierre de compra en Adobe Commerce estableciendo el campo **[!UICONTROL Enable messaging]** en `Yes`.
1. Haga clic en **[!UICONTROL Save Config]** para guardar los cambios.
1. Vaya a **[!UICONTROL System]** > **[!UICONTROL Cache Management]** y, a continuación, haga clic en **[!UICONTROL Flush Cache]** para actualizar todas las cachés no válidas.

| Campo | Ámbito | Descripción |
|---|---|---|
| [!UICONTROL Enable Fastlane] | vista de tienda | Habilitar o deshabilitar [!DNL Fastlane] en la página de cierre de compra. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Title] | vista de tienda | Añada el texto que se mostrará como título para esta opción de pago en la vista Método de pago durante el cierre de compra. El valor predeterminado es `Credit Card (via Fastlane)`. Opciones: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | sitio web | La [acción de pago](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html) para el método de pago especificado. Opciones: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | vista de tienda | El criterio de ordenación para el método de pago especificado en la página de pago. Valor `Numeric Only` |
| [!UICONTROL Enable messaging] | vista de tienda | Especifique si la marca [!UICONTROL Fastlane] está habilitada durante el cierre de compra en Adobe Commerce. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

### Opcional. Configuración de estilo avanzada

Esta configuración opcional puede personalizar el modo en que [!UICONTROL Fastlane] se muestra en el sitio web.

>[!TIP]
>
>Los estilos que no cumplen las directrices de accesibilidad vuelven a la configuración predeterminada.

1. En la sección _[!UICONTROL Payment Services]_, vaya a la sección&#x200B;_[!UICONTROL Fastlane]_.
1. Expanda la sección _[!UICONTROL Advanced Style Settings (optional)]_.
1. Modifique la configuración según sea necesario.
1. Haga clic en **[!UICONTROL Save Config]** para guardar los cambios.

Consulte [Documentos de desarrolladores de PayPal](https://developer.paypal.com/limited-release/accelerated-checkout-bt/) para obtener más información sobre la personalización.

#### Configuración raíz

Esta configuración opcional modifica el componente de cierre de compra general [!UICONTROL Fastlane].

| Campo | Ámbito | Descripción |
|---|---|---|
| [!UICONTROL Background Color] | vista de tienda | Define el color de fondo del componente. Solo `RGB` valores |
| [!UICONTROL Border Color] | vista de tienda | Define el color del borde del componente. Solo `RGB` valores |
| [!UICONTROL Font Family] | vista de tienda | Establece la fuente del componente. Solo se muestran las fuentes disponibles en la temática |
| [!UICONTROL Font Size Base] | vista de tienda | Define el tamaño de la fuente. Solo valores de `px` (píxel) |
| [!UICONTROL Padding] | vista de tienda | Establece el relleno en el componente. Solo valores de `px` (píxel) |
| [!UICONTROL Primary Color] | vista de tienda | Define el color principal del componente. Solo `RGB` valores |
| [!UICONTROL Text Color] | vista de tienda | Define el color principal del texto en el componente. Solo `RGB` valores |

#### Configuración de entrada

Esta configuración opcional se aplica a los campos de entrada del cliente del componente [!UICONTROL Fastlane].

| Campo | Ámbito | Descripción |
|---|---|---|
| [!UICONTROL Background Color] | vista de tienda | Define el color de fondo del componente. Solo `RGB` valores |
| [!UICONTROL Border Color] | vista de tienda | Define el color del borde del componente. Solo `RGB` valores |
| [!UICONTROL Border Radius] | vista de tienda | Define el radio del borde. Solo valores de `px` (píxel) |
| [!UICONTROL Border Width] | vista de tienda | Define la anchura del borde. Solo valores de `px` (píxel) |
| [!UICONTROL Focus Border Color] | vista de tienda | Define el color del borde de enfoque del componente. Solo `RGB` valores |
| [!UICONTROL Text Color Base] | vista de tienda | Define el color principal del texto en el componente. Solo `RGB` valores |

## [!UICONTROL Apple Pay]

Con [!DNL Apple Pay], los comerciantes pueden ofrecer una experiencia de pago segura, rápida y sin problemas en Safari, que admite hasta 99 dominios por cuenta de comerciante. El botón [!DNL Apple Pay] rellena automáticamente la información de pago, contacto y envío desde el dispositivo iOS o macOS del cliente, lo que permite realizar compras rápidas de un solo toque que pueden ayudar a aumentar las tasas de conversión.

Consulte [Opciones de pago](payments-options.md#apple-pay-button) para obtener más información.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. En el panel izquierdo, expanda **[!UICONTROL Sales]** y elija **[!UICONTROL Payment Methods]**.
1. Expanda la sección _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. En la sección _[!UICONTROL Payment Services]_, expanda la sección&#x200B;_[!UICONTROL Apple Pay]_.
1. Para **[!UICONTROL Title]**, escriba texto (si es necesario) para cambiar el nombre del método de pago como se muestra durante el cierre de compra.
1. Para [establecer la acción de pago](production.md#set-payment-services-as-payment-method), seleccione **[!UICONTROL Authorize]** o **[!UICONTROL Authorize and Capture]**.
1. Especifique si la opción [!DNL Apple Pay] está habilitada en Adobe Commerce seleccionando `Yes` en las siguientes opciones según sea necesario:
   * **[!UICONTROL Show Apple Pay on checkout page]**
   * **[!UICONTROL Show Apple Pay on product detail page]**
   * **[!UICONTROL Show Apple Pay in mini cart preview]**
   * **[!UICONTROL Show Apple Pay on cart page]**
1. Para habilitar el modo de depuración, seleccione `Yes` para **[!UICONTROL Debug Mode]** (`No` lo deshabilita).
1. Para guardar los cambios, haga clic en **[!UICONTROL Save Config]**
1. Vaya a **[!UICONTROL System]** > **[!UICONTROL Cache Management]** y, a continuación, haga clic en **[!UICONTROL Flush Cache]** para actualizar todas las cachés no válidas.

### Opciones de configuración

| Campo | Ámbito | Descripción |
|---|---|---|
| [!UICONTROL Title] | vista de tienda | Añada el texto que se mostrará como título para esta opción de pago en la vista Método de pago durante el cierre de compra. Opciones: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | sitio web | La [acción de pago](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html) para el método de pago especificado. Opciones: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show on checkout page] | sitio web | Habilitar o deshabilitar [!DNL Apple Pay] en la página de cierre de compra. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | vista de tienda | El criterio de ordenación para el método de pago especificado en la página de pago. Valor `Numeric Only` |
| [!UICONTROL Show buttons on product detail page] | vista de tienda | Habilite o deshabilite [!DNL Apple Pay] en la página de detalles del producto. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | vista de tienda | Habilite o deshabilite [!DNL Apple Pay] en la vista previa del minicarrito. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | vista de tienda | Habilite o deshabilite [!DNL Apple Pay] en la página del carro de compras. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | sitio web | Habilite o deshabilite el modo de depuración. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Google Pay]

La opción de pago [!UICONTROL Google Pay] permite que el comerciante ofrezca Google Pay a sus compradores, que pueden usar Google Wallet en sus dispositivos para realizar compras.

Consulte [Opciones de pago](payments-options.md#google-pay-button) para obtener más información.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. En el panel izquierdo, expanda **[!UICONTROL Sales]** y elija **[!UICONTROL Payment Methods]**.
1. Expanda la sección _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. En la sección _[!UICONTROL Payment Services]_, expanda la sección&#x200B;_[!UICONTROL Google Pay]_.
1. (Opcional) Cambie el nombre del método de pago mostrado durante el cierre de compra introduciendo el nuevo nombre en el campo **[!UICONTROL Title]**.
1. [Establece la acción de pago](production.md#set-payment-services-as-payment-method) seleccionando **[!UICONTROL Authorize]** o **[!UICONTROL Authorize and Capture]**.
1. Especifique si la opción [!DNL Google Pay] está habilitada en Adobe Commerce seleccionando `Yes` en las siguientes opciones según sea necesario:
   * **[!UICONTROL Show Google Pay on checkout page]**
   * **[!UICONTROL Show Google Pay on product detail page]**
   * **[!UICONTROL Show Google Pay in mini cart preview]**
   * **[!UICONTROL Show Google Pay on cart page]**
1. Para habilitar **[!UICONTROL 3D Secure authentication]** (`Off` de forma predeterminada), elija `Always` o `When required`.
1. Para habilitar el modo de depuración, seleccione `Yes` para **[!UICONTROL Debug Mode]** (`No` lo deshabilita).
1. Configure el aspecto del botón _[!UICONTROL Google Pay]_&#x200B;seleccionando **[!UICONTROL Button Color]**,**[!UICONTROL Button Type]**&#x200B;y **[!UICONTROL Button Style]**&#x200B;según sea necesario.
1. Para establecer la altura, utiliza el valor predeterminado para la altura definida en **[!UICONTROL Button Style]**.
1. Para guardar los cambios, haga clic en **[!UICONTROL Save Config]**
1. Vaya a **[!UICONTROL System]** > **[!UICONTROL Cache Management]** y, a continuación, haga clic en **[!UICONTROL Flush Cache]** para actualizar todas las cachés no válidas.

### Opciones de configuración

| Campo | Ámbito | Descripción |
|---|---|---|
| [!UICONTROL Title] | vista de tienda | Especifica la etiqueta de texto que se muestra para esta opción de pago en la vista Método de pago durante el cierre de compra. Opciones: `[!UICONTROL text field]` |
| [!UICONTROL Payment Action] | sitio web | La [acción de pago](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html) para el método de pago especificado. Opciones: `[!UICONTROL Authorize]` / `[!UICONTROL Authorize and Capture]` |
| [!UICONTROL Show on checkout page] | sitio web | Habilitar o deshabilitar [!DNL Google Pay] en la página de cierre de compra. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | vista de tienda | El criterio de ordenación para el método de pago especificado en la página de pago. Valor `Numeric Only` |
| [!UICONTROL Show buttons on product detail page] | vista de tienda | Habilite o deshabilite [!DNL Google Pay] en la página de detalles del producto. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | vista de tienda | Habilite o deshabilite [!DNL Google Pay] en la vista previa del minicarrito. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | vista de tienda | Habilite o deshabilite [!DNL Google Pay] en la página del carro de compras. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL 3D Secure authentication] | vista de tienda | Habilitar o deshabilitar [autenticación 3D Secure](security.md#3ds). Opciones: [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | sitio web | Habilite o deshabilite el modo de depuración. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Button Color] | Vista de tienda | Definir color del botón [!DNL Google Pay]. Opciones: `[!UICONTROL Default]` / `[!UICONTROL Black]` / `[!UICONTROL White]` |
| [!UICONTROL Button Type] | Vista de tienda | Definir tipo del botón [!DNL Google Pay]. Opciones: `[!UICONTROL buy]` / `[!UICONTROL checkout]` / `[!UICONTROL order]` / `[!UICONTROL pay]` / `[!UICONTROL plain]` |

Consulte la documentación de [opciones de objeto de solicitud de API de Google Pay](https://developers.google.com/pay/api/web/reference/request-objects) para obtener más información.

## [!DNL PayPal Payment Buttons]

Las opciones de pago de [!DNL PayPal payment buttons] proporcionan un proceso de pago simple, rápido y seguro para tu cliente.

Consulte [Opciones de pago](payments-options.md#paypal-smart-buttons) para obtener más información.

Configurar [!DNL PayPal payment buttons]

Puede activar y configurar las opciones de pago de los botones de pago de PayPal en Admin:

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. En el panel izquierdo, expanda **[!UICONTROL Sales]** y elija **[!UICONTROL Payment Methods]**.
1. Expanda la sección _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. En la sección _[!UICONTROL Payment Services]_, expanda la sección&#x200B;_[!UICONTROL PayPal payment buttons]_.
1. Para cambiar el nombre de la forma de pago como se muestra durante el cierre de compra, edite el campo _[!UICONTROL Title]_.
1. Para [establecer la acción de pago](production.md#set-payment-services-as-payment-method), seleccione **[!UICONTROL Authorize]** o **[!UICONTROL Authorize and Capture]**.
1. Para priorizar un método de pago en la página de cierre de compra, proporcione un valor `Numeric Only` en el campo **[!UICONTROL Sort order]**.
1. Para habilitar/deshabilitar la [mensajería de pago posterior](payments-options.md#pay-later-button), seleccione `Yes`/`No` para **[!UICONTROL Display Pay Later Message]**.

   * Si habilitas [Pagar más tarde](payments-options.md#pay-later-button), se mostrará un botón modal **[!UICONTROL Configure Messaging]** para que puedas establecer los estilos de **[!UICONTROL PayPal Pay Later messaging]**.

1. Especifique dónde están habilitados los botones de pago de PayPal en Adobe Commerce seleccionando `Yes` en las siguientes opciones según sea necesario:
   * **[!UICONTROL Show buttons on checkout page]**
   * **[!UICONTROL Show buttons on product detail page]**
   * **[!UICONTROL Show buttons in mini cart preview]**
   * **[!UICONTROL Show buttons on cart page]**
1. Para habilitar la opción Venmo como pago, selecciona `Yes` para **[!UICONTROL Venmo Enabled]**.
1. Para habilitar las tarjetas de crédito y débito como opción de pago (botón PayPal Smart), selecciona `Yes` para **[!UICONTROL Credit and Debit Card Enabled]**.
1. Para habilitar/deshabilitar la opción de pago [PayPal más tarde](payments-options.md#pay-later-button), selecciona `Yes`/`No` para **[!UICONTROL PayPal Pay Later Enabled]**.
1. Para habilitar el modo de depuración, seleccione `Yes` para **[!UICONTROL Debug Mode]** (`No` lo deshabilita).
1. Para guardar los cambios, haga clic en **[!UICONTROL Save Config]**
1. Vaya a **[!UICONTROL System]** > **[!UICONTROL Cache Management]** y, a continuación, haga clic en **[!UICONTROL Flush Cache]** para actualizar todas las cachés no válidas.

### Opciones de configuración

| Campo | Ámbito | Descripción |
|---|---|---|
| [!UICONTROL Title] | vista de tienda | Agrega el texto que se mostrará como título para esta opción de pago en la vista Método de pago durante el cierre de compra. Opciones: campo de texto |
| [!UICONTROL Payment Action] | sitio web | La [acción de pago](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} para el método de pago especificado. Opciones: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Display Pay Later Message] | sitio web | Activa o desactiva la mensajería PayPal Más tarde en el carro de compras, la página del producto, el minicarrito y durante el flujo de pago. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Configure Messaging] | vista de tienda | Modifica los estilos de mensajería PayPal más tarde. Opciones: `[!UICONTROL Product page]` / `[!UICONTROL Cart]` |
| [!UICONTROL Show buttons on checkout page] | vista de tienda | Habilitar o deshabilitar [!DNL PayPal payment buttons] en la página de cierre de compra. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on product detail page] | vista de tienda | Habilite o deshabilite [!DNL PayPal payment buttons] en la página de detalles del producto. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | vista de tienda | Habilite o deshabilite [!DNL PayPal payment buttons] en la vista previa del minicarrito. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | vista de tienda | Habilite o deshabilite [!DNL PayPal payment buttons] en la página del carro de compras. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Venmo Enabled] | vista de tienda | Activa o desactiva la opción de pago Venmo donde se muestran los botones de pago. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Credit and Debit Card Enabled] | vista de tienda | Activa o desactiva las opciones de tarjeta de crédito y débito donde se muestran los botones de pago. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL PayPal Pay Later Enabled] | vista de tienda | Activar o desactivar la opción de pago PayPal Más tarde en la que se muestran los botones de pago. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | sitio web | Habilite o deshabilite el modo de depuración. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## Estilo de botón

También puede configurar las opciones _[!UICONTROL Button style]_&#x200B;de los botones de pago:

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. En el panel izquierdo, expanda **[!UICONTROL Sales]** y elija **[!UICONTROL Payment Methods]**.
1. Expanda la sección _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. En la sección _[!UICONTROL [!DNL Payment Services]]_, expanda la sección&#x200B;_[!UICONTROL PayPal Smart Button Styling]_.
1. Para establecer el diseño, seleccione `Vertical` o `Horizontal` para **[!UICONTROL Layout]**
1. Para establecer el color, seleccione uno de los colores disponibles en **[!UICONTROL Color]**.
1. Para establecer la forma, seleccione `Rectangular` o `Pill` para **[!UICONTROL Shape]**.
1. Para usar la altura predeterminada, seleccione `Yes` o `No` para **[!UICONTROL Use Default Height]**.
1. Para establecer la altura personalizada, agregue la altura de píxeles deseada para **[!UICONTROL Height]**.
1. Para establecer el lema, seleccione `Yes` o `No` para **[!UICONTROL Tagline]**.
1. Para guardar los cambios, haga clic en **[!UICONTROL Save Config]**
1. Vaya a **[!UICONTROL System]** > **[!UICONTROL Cache Management]** y, a continuación, haga clic en **[!UICONTROL Flush Cache]** para actualizar todas las cachés no válidas.

### Opciones de configuración

| Campo | Ámbito | Descripción |
|--- |--- |--- |
| [!UICONTROL Layout] | Vista de tienda | Define el estilo del diseño de los botones de pago de PayPal. Opciones: `[!UICONTROL Vertical]` / `[!UICONTROL Horizontal]` |
| [!UICONTROL Color] | Vista de tienda | Define el color de los botones de pago de PayPal. Opciones: [!UICONTROL Blue] / `[!UICONTROL Gold]` / `[!UICONTROL Silver]` / `[!UICONTROL White]` / `[!UICONTROL Black]` |
| [!UICONTROL Shape] | Vista de tienda | Define la forma de los botones de pago de PayPal. Opciones: `[!UICONTROL Rectangular]` / `[!UICONTROL Pill]` |
| [!UICONTROL Use Default Height] | Vista de tienda | Define si los botones de pago de PayPal utilizan una altura predeterminada. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Height] | Vista de tienda | Definir la altura de los botones de pago de PayPal. Valor predeterminado: ninguno |
| [!UICONTROL Label] | Vista de tienda | Define la etiqueta que aparece en los botones de pago de PayPal. Opciones: `[!UICONTROL PayPal]` / `[!UICONTROL Checkout]` / `[!UICONTROL Buynow]` / `[!UICONTROL Pay]` / `[!UICONTROL Installment]` |
| [!UICONTROL Tagline] | Vista de tienda | Habilita el lema. Opciones: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## Vaciar la caché

Si cambias la configuración en _Configuración_, por ejemplo, cambiando los botones Apple Pay, Venmo o PayPal Paylater, vacía manualmente la caché para que tu tienda muestre las configuraciones más recientes.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL System]** > **[!UICONTROL Cache Management]**.
1. Haga clic en **[!UICONTROL Flush Cache]** para actualizar todas las cachés no válidas.

Si algún tipo de caché de la tabla Administración de caché tiene un estado `INVALIDATED`, es posible que el almacén no muestre la configuración más reciente para ese elemento. Vacíe la caché para actualizar el almacén y mostrar la configuración más reciente.

Para asegurarse de que la tienda muestre la configuración correcta, [vacíe la caché](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management) periódicamente.

## Bóveda de tarjetas

Puede habilitar una funcionalidad que permita a los clientes almacenar (o &quot;guardar&quot;) la información de su tarjeta de crédito en Mi cuenta para usarla en futuras compras.

También puede utilizar el depósito de tarjetas en el Administrador para completar pedidos posteriores para clientes existentes.

Habilite o deshabilite el depósito de tarjetas en la [configuración del campo de tarjeta de crédito](#credit-card-fields).

Consulte [Avalúo de tarjetas de crédito](vaulting.md) para obtener más información.

## 3DS

3DS protege a clientes y comerciantes de actividades fraudulentas en sus tiendas y permite el cumplimiento de las normas de la Unión Europea (UE).

Habilitar o deshabilitar 3DS en la [configuración del campo de la tarjeta de crédito](#credit-card-fields).

Consulte [3DS en Seguridad](security.md#3ds) para obtener más información.

## Usar varias cuentas de PayPal

En [!UICONTROL Payment Services], puedes usar varias cuentas de PayPal dentro de **una** cuenta de comerciante en el nivel de sitio web. Por ejemplo, si tienes tiendas en varios países (que usan [divisas](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency) diferentes) o quieres usar Adobe Commerce para algunas partes de tu negocio, pero no para _todos_, puedes configurar tu cuenta de comerciante para que use varias cuentas de PayPal.

Vea [Sitio, tienda y ámbito de vista](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html) para obtener más información sobre la jerarquía de sitios web, tiendas y vistas de tiendas.

Consulte [Configuración de la línea de comandos](configure-cli.md#configure-scope-via-cli) para obtener más información sobre cómo configurar ámbitos para varias cuentas de PayPal a través de CLI.

El representante de ventas puede crear un nuevo [ámbito](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) para tu cuenta de comerciante e incorporar el sitio adicional con PayPal para que se muestre en el sitio cualquiera de los botones de PayPal que configuraste para que aparezcan. Póngase en contacto con Ventas
representante de para obtener ayuda con el uso de varias cuentas de PayPal en sus sitios web.
