---
title: Configuración de servicios de pago
description: Después de la instalación, puede configurar  [!DNL Payment Services]  en Inicio.
role: Admin, User
level: Intermediate
exl-id: 108f2b24-39c1-4c87-8deb-d82ee1c24d55
feature: Payments, Checkout, Configuration, Paas, Saas
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '2420'
ht-degree: 0%

---

# Configuración

Puede personalizar [!DNL Payment Services] según sus necesidades con una configuración útil en la página de inicio de [!DNL Payment Services].

Para configurar [!DNL Payment Services] para [!DNL Adobe Commerce] y [!DNL Magento Open Source], haga clic en **[!UICONTROL Settings]**. Estas opciones de configuración solo se aplican al entorno establecido en el campo _[!UICONTROL Payment mode]_&#x200B;de las opciones de configuración[_ General _](#configure-general-settings).

Para la configuración heredada o de varias tiendas, consulte [Configurar en el administrador](configure-admin.md).

## Configuración general

La configuración de [!UICONTROL General] permite habilitar o deshabilitar Servicios de pago como método de pago y agregar información a las transacciones de clientes para marcar o codificar un sitio web o una vista de tienda con información personalizada.

### Habilitar servicios de pago

Puede habilitar [!DNL Payment Services] para su sitio web y habilitar la prueba de zona protegida o los pagos activos.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.

1. Haga clic en **[!UICONTROL Settings]**. Consulte [Introducción a [!DNL Payment Services] Inicio](payments-home.md) para obtener más información.

   ![Vista de configuración de React](assets/react-settings-view.png){width="500" zoomable="yes"}

   La sección _[!UICONTROL General]_&#x200B;incluye la configuración usada para habilitar [!DNL Payment Services] como método de pago.

1. Para habilitar [!DNL Payment Services] como método de pago para tu tienda, en la sección _[!UICONTROL General]_, cambia **[!UICONTROL Enable Payment Services as payment method]**&#x200B;a `Yes`.

1. Si todavía está probando [!DNL Payment Services] para su tienda, establezca **Modo de pago** en `Sandbox`. Si está listo para habilitar los pagos activos, establézcalo en `Production`.

1. Los valores de **[!UICONTROL Payment Services Sandbox ID]** y **[!UICONTROL Payment Services Production ID]** se rellenan automáticamente una vez que configura [Commerce Services Connector](https://experienceleague.adobe.com/es/docs/commerce-merchant-services/user-guides/integration-services/saas){target=_blank} y visita el panel [!DNL Payment Services] por primera vez. Haga esto para finalizar la incorporación para su zona protegida o entornos de producción. Estos valores asocian su ID de SaaS a [!DNL Payment Services].

   >[!WARNING]
   >
   > Si restablece sus [!DNL Payment Services] ID, debe incorporarse de nuevo.

1. Haga clic en **[!UICONTROL Save]**.

   Si intenta salir de esta vista sin guardar los cambios, aparecerá un modal que le pedirá que descarte los cambios, que siga editándolos o que los guarde.

1. Vaya a **[!UICONTROL System]** > **[!UICONTROL Cache Management]** y haga clic en **[!UICONTROL Flush Cache]** para actualizar todas las cachés no válidas.

Ahora puede cambiar la configuración predeterminada de las funciones de [opciones de pago](#configure-payment-options) y la visualización de la tienda.

### Añadir descriptor temporal

Puede agregar un(a) [!UICONTROL Soft Descriptor] a sus sitios web o a la configuración de vistas de tiendas individuales. Los descriptores leves se muestran en los extractos bancarios de transacciones de clientes. Si, por ejemplo, tiene varias tiendas, marcas o catálogos, puede delinear fácilmente entre ellos agregando texto personalizado al campo [!UICONTROL Soft Descriptor].

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Haga clic en **[!UICONTROL Settings]**. Consulte [Introducción a [!DNL Payment Services] Inicio](payments-home.md) para obtener más información.
1. Seleccione el sitio web o la vista de tienda, en el menú desplegable **[!UICONTROL Scope]**, para los que desea crear un descriptor temporal. Para la configuración inicial, deje esto como **[!UICONTROL Default]** para establecer el valor predeterminado.
1. Agregue el texto personalizado (hasta 22 caracteres) en el campo de texto y reemplace `Soft descriptor`.
1. Haga clic en **[!UICONTROL Save]**.
1. Para crear un descriptor temporal distinto del predeterminado configurado para una vista de sitio web o tienda:
   1. Seleccione el sitio web o la vista de tienda, en el menú desplegable **[!UICONTROL Scope]**, para los que desea crear un descriptor temporal.
   1. Alternar _desactivado_ **[!UICONTROL Use website]** (o **[!UICONTROL Use default]**, en función del ámbito que haya seleccionado).
   1. Añada el texto personalizado en el campo de texto.
   1. Haga clic en **[!UICONTROL Save]**.
1. Para habilitar para un sitio web o una vista de tienda el descriptor en pantalla predeterminado _o_, el descriptor en pantalla utilizado para el sitio web principal:
   1. Seleccione el sitio web o la vista de tienda, en el menú desplegable **[!UICONTROL Scope]**, para los que desea habilitar un descriptor temporal existente.
   1. Alternar _en_ **[!UICONTROL Use website]** (o **[!UICONTROL Use default]**, según el ámbito que haya seleccionado).
   1. Haga clic en **[!UICONTROL Save]**.

   Si intenta salir de esta vista sin guardar los cambios, aparecerá un modal que le pedirá que descarte los cambios, que siga editándolos o que los guarde.

### Opciones de configuración

| Campo | Ámbito | Descripción |
|---|---|---|
| [!UICONTROL Enable] | sitio web | Habilite o deshabilite [!DNL Payment Services] para su sitio web. Opciones: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Payment mode] | vista de tienda | Defina el método o el entorno para su tienda. Opciones: [!UICONTROL Sandbox] / [!UICONTROL Production] |
| [!UICONTROL Payment Services Sandbox ID] | vista de tienda | El ID de comerciante de la zona protegida, que se genera automáticamente durante la incorporación a la zona protegida. |
| [!UICONTROL Payment Services Production ID] | vista de tienda | Su ID de comerciante de producción, que se genera automáticamente durante la incorporación de la producción (en directo). |
| [!UICONTROL Soft Descriptor] | sitio web o vista de tienda | Añada un descriptor temporal a sus sitios web y vistas de tiendas para añadir información a las transacciones de clientes que delimitan marcas, tiendas o líneas de productos. La opción [!UICONTROL Use website] aplica cualquier descriptor flexible agregado en el nivel de sitio web. La opción [!UICONTROL Use default] aplica cualquier descriptor flexible agregado como predeterminado. |

## Configurar opciones de pago

Ahora que ha habilitado [!UICONTROL Payment Services] para su sitio web, puede cambiar la configuración predeterminada de las funciones de pago y la visualización de la tienda.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Haga clic en **[!UICONTROL Settings]**. Consulte [Introducción a [!DNL Payment Services] Inicio](payments-home.md) para obtener más información.
1. Configure las opciones de pago para [tarjetas de crédito](#credit-card-fields), [botones de pago](#payment-buttons) y [estilo de botón](#button-style), según las secciones siguientes.

### Campos de tarjeta de crédito

La configuración de _[!UICONTROL Credit Card Fields]_&#x200B;proporciona una opción de pago simple y segura para los métodos de pago con tarjeta de crédito o débito.

Consulte [Opciones de pago](payments-options.md#credit-card-fields) para obtener más información.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Seleccione la vista de tienda, en el menú desplegable **[!UICONTROL Scope]**, para la que desea habilitar un método de pago.
1. En la sección **[!UICONTROL Credit card fields]**, edite el valor del campo **[!UICONTROL Checkout title]** para cambiar el nombre del método de pago que se muestra durante el cierre de compra.
1. Para [establecer la acción de pago](production.md#set-payment-services-as-payment-method), cambie **[!UICONTROL Payment action]** a `Authorize` o `Authorize and Capture`.
1. Para priorizar un método de pago en la página de cierre de compra, proporcione un valor `Numeric Only` en el campo **[!UICONTROL Sort order]**.
1. Para habilitar la autenticación segura de [3DS](security.md#3ds) (`Off` de forma predeterminada), cambie el selector de **[!UICONTROL 3DS Secure authentication]** a `Always` o `When required`.
1. Para habilitar o deshabilitar los campos de tarjeta de crédito en la página de cierre de compra, active el selector **[!UICONTROL Show on checkout page]**.
1. Para habilitar o deshabilitar [almacenamiento en depósito de tarjetas](#card-vaulting), alterne el selector **[!UICONTROL Vault enabled]**.
1. Para habilitar o deshabilitar [métodos de pago abovedados en Admin](#card-vaulting) (para que los comerciantes completen los pedidos de los clientes en Admin mediante su método de pago abovedado), alterne el selector **[!UICONTROL Show vaulted methods in Admin]**.
1. Para habilitar o deshabilitar el modo de depuración, alterne el selector **[!UICONTROL Debug Mode]**.
1. Haga clic en **[!UICONTROL Save]**.

   Si intenta salir de esta vista sin guardar los cambios, aparecerá un modal que le pedirá que descarte los cambios, que siga editándolos o que los guarde.

1. [Vaciar la caché](#flush-the-cache).

#### Opciones de configuración

| Campo | Ámbito | Descripción |
|---|---|---|
| [!UICONTROL Title] | vista de tienda | Añade el texto que se mostrará como el título de esta opción de pago en la vista Método de pago durante el cierre de compra. Opciones: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | sitio web | La [acción de pago](https://experienceleague.adobe.com/es/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} para el método de pago especificado. Opciones: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | vista de tienda | El orden de clasificación del método de pago especificado en la página de pago. Valor `Numeric Only` |
| [!UICONTROL 3DS Secure authentication] | sitio web | Habilitar o deshabilitar la [autenticación segura de 3DS](security.md#3ds). Opciones: [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Show on checkout page] | sitio web | Habilitar o deshabilitar los campos de tarjeta de crédito para mostrar en la página de cierre de compra. Opciones: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Vault enabled] | vista de tienda | Habilitar o deshabilitar el depósito de [tarjetas de crédito](vaulting.md). Opciones: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show vaulted payment methods in Admin] | vista de tienda | Habilite o deshabilite la capacidad del comerciante para completar pedidos de clientes en el administrador [mediante un método de pago abovedado](vaulting.md). Opciones: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | sitio web | Habilite o deshabilite el modo de depuración. Opciones: [!UICONTROL Off] / [!UICONTROL On] |

### Apple Pay

La opción de pago con botón [!UICONTROL Apple Pay] le permite proporcionar un botón de pago de [!UICONTROL Apple Pay] en el cierre de compra de su tienda desde el explorador Safari (para un máximo de 99 dominios por cuenta de comerciante).

Solo puedes usar Apple Pay si completas el registro automático de [Apple Pay a través de Paypal](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain) y luego [configuras Apple Pay](configure-admin.md#payment-buttons) para tus tiendas.

Consulte [Opciones de pago](payments-options.md#apple-pay-button) para obtener más información.

Puede activar y configurar la opción de pago mediante el botón [!UICONTROL Apple Pay]:

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Seleccione la vista de tienda, en el menú desplegable **[!UICONTROL Scope]**, para la que desea habilitar un método de pago.
1. En la sección **[!UICONTROL Apple Pay]**, edite el valor del campo _[!UICONTROL Checkout title]_&#x200B;para cambiar el nombre del método de pago que se muestra durante el cierre de compra.
1. Para [establecer la acción de pago](production.md#set-payment-services-as-payment-method), cambie **[!UICONTROL Payment action]** a `Authorize` o `Authorize and Capture`.
1. Para habilitar o deshabilitar Apple Pay en la página de cierre de compra, alterne el selector **[!UICONTROL Show Apple Pay on checkout page]**.
1. Para habilitar o deshabilitar Apple Pay en la página de detalles del producto, alterne el selector **[!UICONTROL Show Apple Pay on product detail page]**.
1. Para habilitar o deshabilitar Apple Pay en la vista previa del minicarrito, alterne el selector **[!UICONTROL Show Apple Pay on the mini cart preview]**.
1. Para habilitar o deshabilitar Apple Pay en la página del carro de compras, active el selector **[!UICONTROL Show Apple Pay on cart page]**.
1. Para habilitar o deshabilitar el modo de depuración, alterne el selector **[!UICONTROL Debug Mode]**.
1. Haga clic en **[!UICONTROL Save]**.

   Si intenta salir de esta vista sin guardar los cambios, aparecerá un modal que le pedirá que descarte los cambios, que siga editándolos o que los guarde.

1. [Vaciar la caché](#flush-the-cache).

#### Opciones de configuración

| Campo | Ámbito | Descripción |
|---|---|---|
| [!UICONTROL Checkout title] | vista de tienda | Añade el texto que se mostrará como el título de esta opción de pago en la vista Método de pago durante el cierre de compra. Opciones: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | sitio web | La [acción de pago](https://experienceleague.adobe.com/es/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions) para el método de pago especificado. Opciones: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show on checkout page] | sitio web | Activa o desactiva el botón Apple Pay para mostrar en la página de pago y envío. Opciones: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on checkout page] | sitio web | Activa o desactiva el botón Apple Pay para mostrar en la página de detalles del producto. Opciones: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on mini cart preview] | sitio web | Activa o desactiva el botón Apple Pay para mostrar la vista previa del minicarrito. Opciones: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on cart page] | sitio web | Activa o desactiva el botón Apple Pay para mostrar en la página del carro de compras. Opciones: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | sitio web | Habilite o deshabilite el modo de depuración. Opciones: [!UICONTROL Off] / [!UICONTROL On] |

### Botones de pago

Las opciones de pago de [!DNL PayPal payment buttons] proporcionan un proceso de pago simple, rápido y seguro para tu cliente. Consulte [Opciones de pago](payments-options.md#paypal-smart-buttons) para obtener más información.

Puedes activar y configurar las opciones de pago de los botones de pago de PayPal:

1. Seleccione la vista de tienda, en el menú desplegable **[!UICONTROL Scope]**, para la que desea habilitar un método de pago.
1. Para cambiar el nombre del método de pago como se muestra durante el cierre de compra, edite el valor en el campo **[!UICONTROL Checkout Title]**.
1. Para [establecer la acción de pago](production.md#set-payment-services-as-payment-method), cambie **[!UICONTROL Payment action]** a `Authorize` o `Authorize and Capture`.
1. Para priorizar un método de pago en la página de cierre de compra, proporcione un valor `Numeric Only` en el campo **[!UICONTROL Sort order]**.
1. Use los selectores de alternancia para habilitar o deshabilitar las características de visualización de [!DNL PayPal smart button]:

   - **[!UICONTROL Show PayPal buttons on product checkout page]**
   - **[!UICONTROL Show PayPal buttons on product detail page]**
   - **[!UICONTROL Show PayPal buttons in mini-cart preview]**
   - **[!UICONTROL Show PayPal buttons on cart page]**
   - **[!UICONTROL Show PayPal Pay Later button]**
   - **[!UICONTROL Show PayPal Pay Later message]**
   - **[!UICONTROL Show Venmo button]**
   - **[!UICONTROL Show Apple Pay button]**
   - **[!UICONTROL Show PayPal Credit and Debit Card button]**

     >[!NOTE]
     >
     > Para usar Apple Pay, [debes tener una cuenta de comprobador de zona protegida de Apple](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account) (con tarjeta de crédito falsa e información de facturación) para probarla. Cuando esté listo para usar Apple Pay en modo de producción de zona protegida _o_, después de completar cualquier [prueba y validación](test-validate.md#test-in-sandbox-environment), complete el registro automático de [con [!DNL Apple Pay]](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain) (_Registre su dominio activo_ solo en la sección) y configúrelo para sus tiendas en [!DNL Payment Services].

     Al activar o desactivar la visibilidad de los botones de pago o del mensaje PayPal Más tarde, se muestra una vista previa visual de esa configuración en la parte inferior de la página Configuración.

1. Para habilitar el modo de depuración, alterne el selector **[!UICONTROL Debug Mode]**.
1. Haga clic en **[!UICONTROL Save]**.

   Si intenta salir de esta vista sin guardar los cambios, aparecerá un modal que le pedirá que descarte los cambios, que siga editándolos o que los guarde.

1. [Vaciar la caché](#flush-the-cache).

#### Opciones de configuración

| Campo | Ámbito | Descripción |
|---|---|---|
| [!UICONTROL Title] | vista de tienda | Agrega el texto que se mostrará como título para esta opción de pago en la vista Método de pago durante el cierre de compra. Opciones: campo de texto |
| [!UICONTROL Payment Action] | sitio web | La [acción de pago](https://experienceleague.adobe.com/es/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} para el método de pago especificado. Opciones: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | vista de tienda | El orden de clasificación del método de pago especificado en la página de pago. Valor `Numeric Only` |
| [!UICONTROL Show PayPal buttons on checkout page] | vista de tienda | Habilitar o deshabilitar [!DNL PayPal payment buttons] en la página de cierre de compra. Opciones: [!UICONTROL &#x200B; Yes] / [!UICONTROL No] |
| [!UICONTROL Show PayPal buttons on product detail page] | vista de tienda | Habilite o deshabilite [!DNL PayPal payment buttons] en la página de detalles del producto. Opciones: [!UICONTROL &#x200B; Yes] / [!UICONTROL No] |
| [!UICONTROL Show PayPal buttons in mini-cart preview] | vista de tienda | Habilite o deshabilite [!DNL PayPal payment buttons] en la vista previa del minicarrito. Opciones: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal buttons on cart page] | vista de tienda | Habilite o deshabilite [!DNL PayPal payment buttons] en la página del carro de compras. Opciones: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Pay Later button] | vista de tienda | Activar o desactivar la aparición de la opción de pago posterior en la que se muestran los botones de pago. Opciones: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Pay Later Message] | sitio web | Habilite o deshabilite la mensajería Pagar más tarde en el carro de compras, la página del producto, el minicarrito y durante el flujo de cierre de compra. Opciones: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show Venmo button] | vista de tienda | Activa o desactiva la opción de pago Venmo donde se muestran los botones de pago. Opciones: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show Apple Pay button] | vista de tienda | Activa o desactiva la opción de pago de Apple Pay donde se muestran los botones de pago. Opciones: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Credit and Debit card button] | vista de tienda | Activa o desactiva la opción de pago con tarjeta de crédito y débito donde se muestran los botones de pago. Opciones: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | sitio web | Habilite o deshabilite el modo de depuración. Opciones: [!UICONTROL Off] / [!UICONTROL On] |

### Estilo de botón

También puede configurar las opciones _[!UICONTROL Button style]_&#x200B;de los botones de pago:

1. Para cambiar **[!UICONTROL Layout]**, seleccione `Vertical` o `Horizontal`.

   >[!NOTE]
   >
   > Si el estilo del botón está configurado como `Horizontal` y la tienda está configurada para mostrar varios botones de pago, es posible que solo vea dos botones en la página del producto, la página de cierre de compra y el minicarrito, y un botón en el carrito.

1. Para habilitar el lema en un diseño horizontal, alterne el selector **[!UICONTROL Show tagline]**.
1. Para modificar **[!UICONTROL Color]**, seleccione la opción de color que desee.
1. Para modificar **[!UICONTROL Shape]**, seleccione `Pill` o `Rectangle`.
1. Para habilitar el selector de altura del botón, alterne el selector **[!UICONTROL Responsive button height]**.
1. Para modificar **[!UICONTROL Label]**, seleccione la opción de etiqueta que desee.

   A medida que cambia las opciones de configuración de diseño, color, forma, altura y etiqueta, aparece una vista previa visual de esa configuración en la parte inferior de la página Configuración. En la imagen siguiente, **[!UICONTROL Shape]** está establecido en _Rectángulo_ y **[!UICONTROL Label]** en _PayPal (recomendado)_.

   ![[!DNL PayPal payment buttons] opciones](assets/payment-buttons.png){width="400" zoomable="yes"}

1. Haga clic en **[!UICONTROL Save]**.

   Si intenta salir de esta vista sin guardar los cambios, aparecerá un modal que le pedirá que descarte los cambios, que siga editándolos o que los guarde.

1. [Vaciar la caché](#flush-the-cache).

Puede configurar el estilo del botón de pago [&#x200B; en la configuración heredada en Admin](configure-admin.md#configure-paypal-smart-buttons) o aquí en [!DNL Payment Services Home]. Consulta la [Guía de estilo para los botones de PayPal](https://developer.paypal.com/docs/checkout/standard/customize/buttons-style-guide/) para obtener más información sobre cómo aplicar estilo a los botones de pago de PayPal.

#### Opciones de configuración

| Campo | Ámbito | Descripción |
|--- |--- |--- |
| [!UICONTROL Layout] | Vista de tienda | Definir el estilo del diseño de los botones de pago. Opciones: [!UICONTROL Vertical] / [!UICONTROL Horizontal] |
| [!UICONTROL Tagline] | Vista de tienda | Habilitar/deshabilitar el lema. Opciones: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Color] | Vista de tienda | Defina el color de los botones de pago. Opciones: [!UICONTROL Blue] / [!UICONTROL Gold] / [!UICONTROL Silver] / [!UICONTROL White] / [!UICONTROL Black] |
| [!UICONTROL Shape] | Vista de tienda | Definir la forma de los botones de pago. Opciones: [!UICONTROL Rectangular] / [!UICONTROL Pill] |
| [!UICONTROL Responsive Button Height] | Vista de tienda | Define si los botones de pago utilizan una altura predeterminada. Opciones: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Height] | Vista de tienda | Definir la altura de los botones de pago. Valor predeterminado: ninguno |
| [!UICONTROL Label] | Vista de tienda | Definir la etiqueta que aparece en los botones de pago. Opciones: [!UICONTROL PayPal] / [!UICONTROL Checkout] / [!UICONTROL Buynow] / [!UICONTROL Pay] / [!UICONTROL Installment] |

## Configurar funciones

Para asegurarse de que los usuarios administradores puedan crear y administrar pedidos en el administrador de Commerce, habilite los recursos específicos de [!DNL Payment Services] en los roles de usuario.

Consulte [Funciones de usuario](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html?lang=es) para obtener información sobre cómo administrar las funciones.

Al asignar recursos a la función, debe seleccionar:

- **Pagar con[!DNL Payment Services]**: este recurso garantiza que cuando cree un pedido en el administrador, las tarjetas de crédito de [!DNL Payment Services] estén disponibles como método de pago. Si selecciona el recurso principal **Actions**, también se seleccionará este recurso.
- **[!DNL Payment Services]**: este recurso incluye los recursos **Dashboard** y **proxy de servicios SaaS**, que también se deben seleccionar. Garantizan que [!DNL Payment Services] aparezca en el menú _Ventas_.

  ![Recursos de servicios de pago](assets/roles-payments.png){width="400" zoomable="yes"}

## Vaciar la caché

Si cambias la configuración en _Configuración_, por ejemplo, cambiando los botones Apple Pay, Venmo o PayPal Paylater, vacía manualmente la caché para que tu tienda muestre las configuraciones más recientes.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL System]** > **[!UICONTROL Cache Management]**.
1. Haga clic en **[!UICONTROL Flush Cache]** para actualizar todas las cachés no válidas.

Si algún tipo de caché de la tabla Administración de caché tiene un estado `INVALIDATED`, es posible que el almacén no muestre la configuración más reciente para ese elemento. Vacíe la caché para actualizar el almacén y mostrar la configuración más reciente.

Para asegurarse de que la tienda muestre la configuración correcta, [vacíe la caché](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/tools/cache-management) periódicamente.

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

En [!UICONTROL Payment Services], puedes usar varias cuentas de PayPal dentro de **una** cuenta de comerciante en el nivel de sitio web. Por ejemplo, si tienes tiendas en varios países (que usan [divisas](https://experienceleague.adobe.com/es/docs/commerce-admin/stores-sales/site-store/currency/currency) diferentes) o quieres usar Adobe Commerce para algunas partes de tu negocio, pero no para _todos_, puedes configurar tu cuenta de comerciante para que use varias cuentas de PayPal.

Vea [Sitio, tienda y ámbito de vista](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=es) para obtener más información sobre la jerarquía de sitios web, tiendas y vistas de tiendas.

Consulte [Configuración de la línea de comandos](configure-cli.md#configure-scope-via-cli) para obtener más información sobre cómo configurar ámbitos para varias cuentas de PayPal a través de CLI.

El representante de ventas puede crear un nuevo [ámbito](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=es#scope-settings) para tu cuenta de comerciante e incorporar el sitio adicional con PayPal para que se muestre en el sitio cualquiera de los botones de PayPal que configuraste para que aparezcan. Póngase en contacto con su representante de ventas para obtener ayuda con el uso de varias cuentas de PayPal para sus sitios web.
