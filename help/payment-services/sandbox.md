---
title: Configuración de la zona protegida de pruebas
description: Usa una cuenta de zona protegida de PayPal para usar  [!DNL Payment Services] en modo de prueba.
exl-id: 99c14b4e-e6cf-48f9-9546-5c0d5c71464d
feature: Payments, Checkout, Configuration, Install, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Configuración de la zona protegida de pruebas

Antes de comenzar la incorporación a la zona protegida, debe registrarse para obtener una cuenta gratuita de desarrollador de PayPal y crear cuentas de comerciante (que se utilizarán para la incorporación) y de comprador (que se utilizarán para probar el cierre de compra). Si lo desea, puede crear varias cuentas de desarrollador.

Una cuenta de zona protegida de PayPal le permite usar [!DNL Payment Services] en el modo de prueba. PayPal requiere que uses una cuenta de prueba, un correo electrónico y una contraseña de zona protegida empresarial generados por el portal para desarrolladores de PayPal para la incorporación a la zona protegida. *No cree otra cuenta durante el proceso de incorporación a la zona protegida.*

## Integración de zona protegida

Para completar la incorporación a la zona protegida:

1. Vaya a la [página Cuenta de desarrollador de PayPal](https://developer.paypal.com/developer/accounts/).
1. Haz clic en **[!UICONTROL Log in to Dashboard]** e inicia sesión con tu cuenta de prueba de zona protegida empresarial generada por PayPal Developer Portal o haz clic en **Registrarse** para crear una cuenta.
1. Crear una cuenta de zona protegida de PayPal:
   1. Ir a _[!UICONTROL Testing Tools]_>**[!UICONTROL Sandbox Accounts]**.
   1. Haga clic en **[!UICONTROL Create account]**.

      Si creó una cuenta de zona protegida de PayPal durante el proceso de incorporación a la zona protegida de PayPal, debe [restablecer su zona protegida de incorporación](#reset-your-sandbox-account) porque o no puede verificar su correo electrónico.

   1. Seleccione **[!UICONTROL Business]** como tipo de cuenta y haga clic en **[!UICONTROL Create]**.
   1. En la sección _[!UICONTROL Sandbox Accounts]_, haga clic en los tres puntos de la columna&#x200B;_[!UICONTROL Manage accounts]_ para la cuenta de zona protegida que ha creado.
   1. Haga clic en **[!UICONTROL View/edit account]**.

      ![PayPal - Ver/editar cuenta de zona protegida](assets/onboarding-viewedit-sandbox.png){width="300" zoomable="yes"}

   1. Copie y guarde el ID de correo electrónico y la contraseña generados por el sistema para uso futuro.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Haga clic en **[!UICONTROL Sandbox onboarding]**.

   Esta opción está visible si todavía no ha completado la incorporación a la zona protegida de [!DNL Payment Services].

   Se genera automáticamente un identificador de comerciante de zona protegida, que se rellena en [settings](settings.md). No cambie ni modifique este ID.

   Se le mostrará una ventana de PayPal para conectar una cuenta PayPal y comenzar a aceptar pagos.

1. Introduzca el correo electrónico y la contraseña de la cuenta de zona protegida de PayPal que generó en el paso 3 (no la información de su cuenta comercial de PayPal) y su país o región.
1. Haga clic en **[!UICONTROL Next]**.

   ![PayPal - Conectar la cuenta PayPal para pagos](assets/paypal-connectacct.png){width="300" zoomable="yes"}

1. Siga el flujo de PayPal con las credenciales de la cuenta de la zona protegida guardada anteriormente.
1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.

   El botón **[!UICONTROL Sandbox onboarding]** ya no está visible y aparece el texto &quot;Pagos pendientes de zona protegida&quot;.

Cuando se apruebe la incorporación a la zona protegida de PayPal, debería ver una notificación que indique que su sistema de pago está actualmente en modo de zona protegida y no está procesando pagos activos.

>[!IMPORTANT]
>
>Si revocas el consentimiento de [!DNL Payment Services] para [!DNL Adobe Commerce] y [!DNL Magento Open Source] para procesar tus pagos (en la configuración de tu cuenta PayPal), los pedidos de tu tienda no se podrán procesar a través de [!DNL Payment Services]. En su página de inicio de Servicios de pago, aparece una alerta sobre el consentimiento revocado. Para descartar la alerta, haga clic en **[!UICONTROL Do not show again]**.

### Restablecer la cuenta de zona protegida

Si ha creado una cuenta de zona protegida de PayPal durante el proceso de incorporación a esta zona protegida, debe restablecer su zona protegida de incorporación porque o no puede verificar su correo electrónico.

Para restablecer la cuenta de la zona protegida:

1. Haga clic en **[!UICONTROL Reset sandbox]**. [Crear una cuenta de zona protegida empresarial de PayPal](https://developer.paypal.com/docs/api-basics/sandbox/accounts/#create-a-business-sandbox-account).
1. Haga clic en **[!UICONTROL Sandbox onboarding]** y complete el siguiente conjunto de pasos.

## Habilitar número de teléfono de contacto

El número de teléfono de contacto te permite obtener los números de teléfono de contacto que PayPal recopila de tus clientes. PayPal siempre recopila los números de teléfono de contacto de los titulares de cuentas de PayPal para ayudar a confirmar su identidad y ponerse en contacto con ellos para resolver problemas en sus cuentas o para completar sus procesos de cumplimiento. Sin embargo, PayPal desaconseja el uso de números de teléfono de contacto directamente del comerciante porque puede afectar negativamente a las ventas. Consulte la documentación de [PayPal obtiene los números de teléfono de contacto](https://www.sandbox.paypal.com/businessmanage/preferences/website) para obtener más información.

Esta característica es `off` de manera predeterminada. Cuando lo habilita, los administradores de tiendas pueden ver los números de teléfono cuando un cliente completa un flujo de cierre de compra con marca fuera de la página de cierre de compra.

>[!IMPORTANT]
>
>Esta configuración no se aplica a otros flujos de cierre de compra.

## Realizar pruebas en un entorno limitado

Se recomienda encarecidamente que utilice espacios de datos de prueba para entornos de integración y ensayo, y que pruebe Pagos en producción, con tarjetas de crédito y bancos reales, antes de exponer esta funcionalidad a los compradores.

Consulte [Probar y validar](test-validate.md) para obtener más información.
