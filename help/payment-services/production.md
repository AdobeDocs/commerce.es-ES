---
title: Habilitar [!DNL Payment Services] para producción
description: Complete el proceso de incorporación habilitando  [!DNL Payment Services] for production.
exl-id: 3b1269e8-127b-47f8-9738-9722a5737c63
feature: Payments, Checkout, Configuration, Install, Paas, Saas
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# Habilitar [!DNL Payment Services] para producción

Puede poner el servicio en producción y completar el [proceso de incorporación](onboard.md), según los pasos de este tema, después de lo siguiente:

* [!BADGE Solo PaaS]{type=Informative tooltip="Solo se aplica a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe)."} [Instalar](install.md) la extensión de Servicios de pago
* [!BADGE Solo PaaS]{type=Informative tooltip="Solo se aplica a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe)."} [Configurar y conectar](connect.md) su instancia
* [Configura](sandbox.md) y [prueba](test-validate.md) tu zona protegida

## Establecer [!DNL Payment Services] como método de pago

Después de [configurar los servicios de Commerce](connect.md#configure-commerce-services) y habilitar la [prueba de zona protegida](sandbox.md#enable-sandbox-testing) o los [pagos activos](#enable-live-payments), debe establecer [!DNL Payment Services] como método de pago.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Haga clic en **[!UICONTROL Enable Payment Services]**.

   Esta opción está visible si aún no ha configurado [!DNL Payment Services] como método de pago para uno o más sitios web.

   Se le dirigirá al área de configuración en la vista Inicio con las opciones relevantes expandidas (**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Settings]_), donde puede habilitar las opciones de [!DNL Payment Services] como su [método de pago](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods){target="_blank"}.

1. En _[!UICONTROL General Configuration]_, establezca **[!UICONTROL Enable]**&#x200B;en `Yes`.
1. Establezca **[!UICONTROL Payment Action]**, tanto para _[!UICONTROL Credit Card Fields]_&#x200B;como para&#x200B;_[!UICONTROL PayPal payment buttons]_, en una de las siguientes opciones:

   | Configuración | Descripción |
   |---|---|
   | `Authorize` | Aprueba la compra y retiene los fondos. La cantidad no se retira hasta que sea &quot;capturada&quot; por el comerciante. |
   | `Authorize and Capture` | Aprueba la compra y el comerciante &quot;captura&quot; los fondos. |

   >[!IMPORTANT]
   >
   >[!DNL Payment Services] admite capturas parciales. Un comerciante puede capturar parcialmente (facturar) partes de un pedido. Por ejemplo, puede capturar cada elemento de forma individual, o un elemento ahora y el resto más tarde.

1. Haga clic en **[!UICONTROL Save]**.
1. Haga clic en **[!UICONTROL Go to Payment Services]** para que se le dirija de nuevo a la página de inicio de [!DNL Payment Services].
1. [Borra tu caché](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cache-management.html).

   La limpieza debe realizarse después de cada cambio de configuración.

Consulta [Configurar [!DNL Payment Services]](configure-admin.md) para obtener más información sobre cómo configurar los campos de tarjeta de crédito y los botones de pago de PayPal.

## Incorporación completa del comerciante

El siguiente paso para permitir que sus tiendas entren en funcionamiento con los servicios de pago es completar la incorporación activa.

Payment Services proporciona [**opciones de pago avanzadas** (totalmente admitidas) y **estándar** (cierre de compra exprés)](../payment-services/payments-options.md#standard-vs-advanced-payments-experience), así como flujos de incorporación, según el país en el que opere y su experiencia de pago preferida.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Haga clic en **[!UICONTROL Live onboarding]**.

   Esta opción está visible si todavía no ha completado la incorporación activa de [!DNL Payment Services].

1. En el modal _Seleccione su país_, seleccione el país desde el cual está operando.

   Servicios de pago proporciona soporte completo para todas las opciones de pago en [cinco países](../payment-services/introduction.md#availability) actualmente. Payment Services proporciona la capacidad de Pago y envío exprés (un subconjunto de opciones de pago) para todos los demás países representados en la lista de países.

   El país que elijas de la lista determinará las opciones de pago y el flujo de incorporación—[Avanzado](#advanced-onboarding) (totalmente compatible) o [Estándar](#standard-onboarding) (Pago y envío exprés)—disponible para ti.

>[!TIP]
>
> Una vez que elija y continúe con una opción de incorporación (Estándar o Avanzada), debe volver a completar la incorporación para actualizar o reducir la categoría desde la selección inicial.

### Incorporación avanzada

Este flujo de incorporación está disponible para comerciantes de [países totalmente compatibles](../payment-services/introduction.md#availability).

Una vez seleccionado el país:

1. En el modal que aparece, selecciona **Avanzado**.

   Para la opción **Standard**, continúe con el [flujo de incorporación estándar](#standard-onboarding).

1. Haga clic en **Continuar**.
1. Continúa con el flujo de PayPal para la incorporación avanzada totalmente compatible, usando las credenciales de tu cuenta PayPal (no las credenciales de tu cuenta de zona protegida) _o_ regístrate para obtener una nueva cuenta PayPal.

>[!IMPORTANT]
>
>**La incorporación avanzada** requiere que los comerciantes [soliciten derechos de pago](#request-payments-entitlement-from-adobe) para habilitar la incorporación activa.

### Incorporación estándar

Este flujo de incorporación estándar está disponible para los comerciantes de los países disponibles para los que se proporciona [solo soporte para Pago y envío exprés](../payment-services/introduction.md#availability).

Una vez seleccionado el país:

1. En el modal _Acuerdo de servicios de pago_ que aparece, haga clic en el vínculo **Acuerdo de servicios de pago** para ver el acuerdo de servicios de pago de Adobe Commerce.
1. En el modal _Acuerdo de servicios de pago_, haz clic en **Acepto**.
1. Continúa con el flujo de PayPal para la incorporación de Pago y envío exprés, usando tus credenciales de cuenta de PayPal (no tus credenciales de cuenta de zona protegida) o regístrate en una nueva cuenta de PayPal.

>[!IMPORTANT]
>
>[Los campos Apple Pay y de tarjeta de crédito](../payment-services/payments-options.md) no están disponibles para la **incorporación estándar**.

## Confirmar correo electrónico

1. En la barra lateral de Administración, vaya a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**

   El botón _[!UICONTROL Live onboarding]_&#x200B;ya no está visible y verá un cuadro de texto &quot;[!UICONTROL Live payments pending]&quot;.

   En ese cuadro de texto, también se le puede pedir que confirme su dirección de correo electrónico con PayPal para completar la incorporación.

1. Si se te pide que confirmes tu dirección de correo electrónico, comprueba en tu correo electrónico el mensaje de confirmación enviado desde PayPal y pulsa para confirmar tu dirección de correo electrónico.
1. En la barra lateral de Administración, vaya a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Actualice la ventana del explorador.

   Cuando se apruebe la incorporación de tu comerciante PayPal, deberías ver una notificación que indique que tu sistema de pago está en modo de zona protegida y no está procesando pagos en vivo.

   >[!IMPORTANT]
   >
   >Si revocas el consentimiento de [!DNL Payment Services] para [!DNL Adobe Commerce] y [!DNL Magento Open Source] para procesar tus pagos (en la configuración de tu cuenta PayPal), los pedidos de tu tienda no se podrán procesar a través de [!DNL Payment Services]. En su página de inicio de servicios de pago, aparece una alerta sobre el consentimiento revocado.

## Solicitud de derechos de pagos de Adobe

Para permitir que tus tiendas se activen, solicita el derecho de pagos de Adobe (solo para [incorporación avanzada](#advanced-onboarding)):

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Haga clic en **[!UICONTROL Get Live Payments]** en su página de inicio [!DNL Payment Services].

   ![Solicitar derechos](assets/request-entitlements.png){width="500" zoomable="yes"}

1. Complete el formulario.
1. Un miembro del equipo de ventas se pondrá en contacto con usted.

También puede solicitar el derecho de pago a Adobe en [business.adobe.com](https://business.adobe.com/resources/payment-services.html).

>[!IMPORTANT]
>
>**No se puede acceder a la incorporación activa** hasta que se apruebe el derecho de pagos.

## Configurar nivel de precios

Obtener su [!DNL Payment Services] _ID de comerciante_:

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. En la vista Inicio, haga clic en **[!UICONTROL Settings]**. Ver [Hogar](payments-home.md) para obtener más información.
1. Seleccione el _ID de comerciante_ necesario y envíelo a su representante de ventas, quien configurará el nivel de precios correcto.

Consulte [Procesamiento de nivel 2 y nivel 3](levels-card-payment-transactions.md) para obtener más información sobre las transacciones de pago.

## Habilitar pagos activos

_El ID de comerciante de producción_ se genera automáticamente y se rellena en la [configuración](configure-admin.md). No cambie ni modifique este ID.

Activar pagos activos:

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. En Inicio, haga clic en **[!UICONTROL Settings]** en la parte superior derecha de la página. Ver [Hogar](payments-home.md) para obtener más información.
1. En la sección _[!UICONTROL General Configuration]_, establezca **[!UICONTROL Payment mode]**&#x200B;en `Production`.
1. Haga clic en **[!UICONTROL Save]**.
1. [Borra tu caché](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management){target="_blank"}.

   >[!IMPORTANT]
   >
   >Si no borras la caché, los clientes no podrán ver las opciones de pago de PayPal durante el proceso de pago y envío.

Si vuelve a la página de inicio de [!DNL Payment Services], el mensaje del modo de pago de zona protegida ya no aparece porque está procesando pagos activos.

Consulte [Configurar en el administrador](configure-admin.md) para ver las opciones de configuración heredadas.

>[!IMPORTANT]
>
>Si revocas el consentimiento de [!DNL Payment Services] para procesar tus pagos (en la configuración de tu cuenta PayPal), [!DNL Payment Services] no podrá procesar los pedidos de tu tienda. Si deseas volver a habilitar el procesamiento de pagos, debes completar de nuevo la incorporación. En su página de inicio de servicios de pago, aparece una alerta sobre el consentimiento revocado.

## Prueba en producción

Es muy recomendable probar Payments in production, con tarjetas de crédito y bancos reales, antes de exponer esta funcionalidad a los compradores.

Consulte [Probar y validar](test-validate.md) para obtener más información.
