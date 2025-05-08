---
title: Probar y validar
description: Las pruebas y la validación ayudan a garantizar que [!DNL Payment Services] las funciones funcionan según lo esperado y proporcionan las mejores opciones de pago para sus clientes
exl-id: 95b4615e-73b0-41e8-83e2-e65a0b22f10f
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Probar y validar

Antes de exponer [!DNL Payment Services] para [!DNL Adobe Commerce] y [!DNL Magento Open Source] a los compradores, es aconsejable probar _y_ en producción en el entorno de espacio aislado. Las pruebas y la validación ayudan a garantizar que [!DNL Payment Services] funcione según lo esperado y proporcionan las mejores opciones de pago para su tienda y clientes.

## Realizar pruebas en un entorno limitado

Probar [!DNL Payment Services] en un entorno de espacio aislado es un paso de validación importante, aunque sea un entorno simulado conectado únicamente al espacio aislado de PayPal, no a bancos y comerciantes reales.

1. Completa un pago y envío correcto desde tu tienda, ya sea con [Campos de tarjeta de crédito](payments-options.md#credit-card-fields) o cualquiera de los [botones de pago de PayPal](payments-options.md#paypal-smart-buttons). Ver [Credenciales de prueba](#testing-credentials) para obtener más información acerca del uso de tarjetas de crédito falsas para realizar pruebas.
1. Capture (cuando su acción de pago esté [establecida en `Authorize and Capture`](onboard.md#set-payment-services-as-payment-method)), [reembolso](refunds.md) o [anule](voids.md) el pedido que acaba de completar. También puede [crear una factura](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"} para un pedido si la acción de pago está establecida en `Authorize` en lugar de en `Authorize and Capture`.
1. En un plazo de 24 a 48 horas, consulta la transacción y otra información en el [informe de pagos](payouts.md).
1. Ver los detalles del pedido en el [informe de estado de pago del pedido](order-payment-status.md).

### Credenciales de prueba

Al probar y validar su zona protegida debe utilizar números de tarjeta de crédito falsos, para que no esté creando cargos reales en una cuenta de tarjeta de crédito existente.

Use el generador de tarjetas de crédito de PayPal para [generar información aleatoria sobre tarjetas de crédito](https://www.paypal.com/us/smarthelp/article/where-can-i-find-test-credit-card-numbers-ts2157) para realizar pruebas.

Para probar Apple Pay en modo de zona protegida:

* Cree una cuenta de [probador de zona protegida de Apple](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account) con información falsa de tarjetas de crédito y facturación.
* [Registre los dominios de su zona protegida](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains).

>[!NOTE]
>
>El procesamiento del pago en la zona protegida de PayPal a veces es lento y el servicio puede caerse ocasionalmente. Esta situación no es una indicación de la velocidad y la eficiencia del procesamiento de pagos de productos en vivo.

## Prueba en producción

Se recomienda encarecidamente probar [!DNL Payment Services] en producción, con tarjetas de crédito reales y bancos, antes de exponer esta funcionalidad a los compradores. Aunque es importante probar [!DNL Payment Services] en una zona protegida, probar en producción es el método más sencillo para garantizar que [!DNL Payment Services] funcione según lo esperado.

Puede probar [!DNL Payment Services] en producción de una de las dos maneras siguientes:

* Elija un momento en el que sepa que los compradores no realizarán ningún pedido.
* Utilice una tienda web a la que los compradores no puedan acceder temporalmente, pero a la que usted pueda acceder para realizar pruebas.

Complete sus pruebas de producción con tarjetas de crédito reales y cuentas de PayPal, probando todo el ciclo de vida de un pago, incluyendo la captura y el reembolso. Completar todo el flujo de pago y pago durante la prueba te ofrece una idea más clara de cómo funcionará tu funcionalidad de [!DNL Payment Services] cuando la usen los compradores activos.

También debe verificar que la información que aparece en los extractos bancarios para los métodos de pago que utiliza en las pruebas de producción es correcta y esperada (incluida la descripción de su negocio).

Para probar Apple Pay en el modo de producción, debes [registrar tus dominios de producción](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain).
