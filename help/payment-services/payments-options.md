---
title: Opciones de pago
description: Configura las opciones de pago para personalizar los métodos disponibles para los clientes de tu tienda.
feature: Payments, Checkout, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---

# Opciones de pago

Con [!DNL Adobe Commerce] y [!DNL Magento Open Source] [!DNL Payment Services], tiene varias opciones de pago disponibles.

Puedes configurar estas opciones de pago en [Configuración de la página principal](payments-home.md) o [Configuración de la tienda](configure-admin.md) (recomendado para opciones de pago heredadas o para una configuración de varias tiendas).

Hay diferentes comportamientos para cada método de pago según dónde se encuentre en el proceso de pago:

* Página de producto: la página de producto de un elemento.
* Minicarrito: disponible al hacer clic en el icono del carro de compras cuando se agrega un producto al carro de compras
* Carro de compras: disponible al hacer clic en _Ver y editar el carro_ desde el minicarrito
* Vista de cierre de compra: disponible al hacer clic en _Continuar con el cierre de compra_ desde el minicarrito o el carro de compras

>[!IMPORTANT]
>
>Se debe completar la incorporación de [!DNL Payment Services] antes de procesar los pagos.

## Experiencia de pagos estándar y avanzados

[!DNL Payment Services] proporciona las opciones de pago y los flujos de incorporación de **Advanced** (totalmente compatible) y **Standard** (Pago y envío exprés), según el país en el que opere.

* **Opciones avanzadas** - Todas las [opciones de pagos disponibles](../payment-services/payments-options.md) están disponibles para los [países con soporte total](../payment-services/overview.md#availability) actuales. Durante la incorporación para habilitar los pagos activos, selecciona la [opción de incorporación avanzada](../payment-services/production.md#advanced-onboarding).
* **Estándar** - Un subconjunto de opciones de pagos (Pago y envío exprés)—tarjetas de crédito y débito de PayPal—está disponible para otros países compatibles. [Los campos de tarjeta de crédito](#credit-card-fields) y [Apple Pay](#apple-pay-button) no están disponibles para esta opción de incorporación. Durante la incorporación para habilitar los pagos activos, selecciona la [opción de incorporación estándar](../payment-services/production.md#standard-onboarding).

Consulte [Habilitar [!DNL Payment Services] para producción](../payment-services/production.md#complete-merchant-onboarding) para obtener información sobre cómo completar la incorporación avanzada y estándar.

## [!UICONTROL Credit Card Fields]

[!UICONTROL Credit Card Fields] realiza un pago simple y seguro de los métodos de pago con tarjeta de crédito o débito. Cuando un comprador cierra la compra utilizando campos de tarjeta de crédito, introduce su nombre, dirección de facturación e información de la tarjeta de crédito o débito para realizar el pedido. La información de sus clientes se utiliza de forma segura durante la sesión de compra para guiarlos sin problemas a través del flujo de cierre de compra.

![Campos de tarjeta de crédito en cierre de compra](assets/credit-card-fields.png){width="500" zoomable="yes"}

Habilita [depósito de tarjetas de crédito](#vaulting) para tus tiendas a fin de permitir que los compradores guarden (guarden) la información de su tarjeta de crédito para un cierre de compra rápido más tarde.

Puede configurar [!UICONTROL Credit Card Fields] en la configuración de tienda o en la página de inicio de [!DNL Payment Services]. Consulte [Configuración](settings.md#credit-card-fields) para obtener más información.

También puede cambiar el diseño, la anchura, la altura y el estilo exterior de los campos de tarjeta de crédito. Consulte [Documentación de PayPal](https://developer.paypal.com/docs/checkout/advanced/customize/card-field-style/) para obtener más información.

## [!DNL Apple Pay] botón

Los clientes pueden usar [[!DNL Apple Pay]](https://www.apple.com/apple-pay/), que usa credenciales de pago de tarjeta de crédito y débito almacenadas en un dispositivo iOS o macOS, para realizar compras.

[!DNL Apple Pay] solo está disponible en el explorador Safari. Los comerciantes pueden añadir hasta 99 dominios por cuenta de comerciante.

![Botón Apple Pay en el minicart](assets/applepay-button.png){width="500" zoomable="yes"}

El botón [!DNL Apple Pay] está visible desde las vistas de página de producto, minicarrito, carro de compras y cierre de compra.

Para usar [!DNL Apple Pay] en tus tiendas, completa el registro automático de [con [!DNL Apple Pay]](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain) (_Registra tu dominio activo_ solo en la sección) y [configúrelo para tus tiendas en [!DNL Payment Services]](settings.md#payment-buttons).

>[!NOTE]
>
> Consulta [pago avanzado](https://www.paypal.com/us/cshelp/article/what-is-paypal-advanced-checkout-and-how-do-i-get-started-help953){target=_blank} en la documentación para desarrolladores de PayPal para saber cómo habilitar a los compradores para que paguen con Apple Pay en tu sitio.

Puede configurar [!UICONTROL Apple Pay] en la configuración de la tienda o en la página de inicio de Payment Services. Consulte [Configuración](settings.md#apple-pay) para obtener más información.

## [!DNL Google Pay] botón

Los clientes pueden usar [[!DNL Google Pay]](https://pay.google.com/about/) al agregar los detalles de pago a su cuenta de Google, donde se almacenan de forma segura para una experiencia de pago perfecta.

[!DNL Google Pay] solo está disponible en algunos países o regiones y en ciertos dispositivos. Consulte [[!DNL Google Pay] documentación](https://developer.paypal.com/docs/checkout/apm/google-pay/#link-googlepayintegration) para obtener más información.

![Botón Google Pay en el pago](assets/google-pay-button.png){width="500" zoomable="yes"}

El botón [!DNL Google Pay] está visible desde las vistas de página de producto, minicarrito, carro de compras y cierre de compra.

Puede configurar [!UICONTROL Google Pay] en la configuración de la tienda o en la página de inicio de Payment Services. Consulte [Configuración](configure-admin.md) para obtener más información.

>[!NOTE]
>
> La API [!DNL Google Pay] solo se puede usar en sitios web en un contexto seguro. Consulte la documentación de [Solución de problemas](https://developers.google.com/pay/api/web/support/troubleshooting) para obtener más información.

## [!DNL PayPal Payment Buttons]

[!DNL PayPal payment buttons], que usa PayPal para completar una compra, almacena la dirección de envío, las direcciones de facturación y los detalles de pago del comprador para su uso posterior. Los compradores pueden utilizar cualquier forma de pago previamente almacenada u ofrecida por PayPal.

![Botón PayPal](assets/paypal-button.png){width="350" zoomable="yes"}

Puede configurar [!UICONTROL PayPal payment buttons] en la configuración de tienda o en la página de inicio de [!DNL Payment Services]. Consulte [Configuración](settings.md#payment-buttons) para obtener más información.

Obtén información sobre la disponibilidad de métodos de pago por país en la [documentación de métodos de pago](https://developer.paypal.com/docs/checkout/payment-methods/) de PayPal.

### [!DNL PayPal] botón

Los clientes pueden pagar con facilidad y confianza usando el botón PayPal.

El botón [!DNL PayPal] está visible desde las vistas de página de producto, minicarrito, carro de compras y cierre de compra.

### [!DNL Venmo] botón

Los clientes pueden cerrar la compra con el botón [Venmo](https://venmo.com/).

El botón [!DNL Venmo] está visible desde las vistas de página de producto, minicarrito, carro de compras y cierre de compra.

### Botón de débito o tarjeta de crédito de PayPal

Los clientes pueden pagar con el botón de débito o tarjeta de crédito de PayPal.

El botón de débito o tarjeta de crédito de PayPal está visible desde la página de pago.

Esta opción se puede utilizar para presentar una opción de pago con tarjeta de crédito o débito a sus compradores con un botón alojado en PayPal como alternativa a una integración con tarjeta de crédito.

### [!DNL Pay Later] botón

Ofrezca a sus clientes pagos a corto plazo sin intereses y otras opciones de financiación para que puedan comprar ahora y pagar más tarde con el botón [!DNL Pay Later].

El botón [!DNL Pay Later] está visible desde las vistas de página de producto, minicarrito, carro de compras y cierre de compra.

Ver información acerca de las ofertas de Pago posterior en [Documentación de ofertas de Pago posterior de PayPal](https://developer.paypal.com/docs/checkout/pay-later/us/). Utilice la lista desplegable **País o región** para seleccionar una región de interés.

Obtenga información sobre cómo deshabilitar o habilitar la mensajería de [!DNL Pay Later] al actualizar la configuración de [Configuración](settings.md#payment-buttons).

## Usar sólo botones de pago de PayPal

Para que tu tienda entre en modo de producción rápidamente, puedes configurar _solo_ botones de pago de PayPal (Venmo, PayPal, etc.).—en lugar de utilizar también la opción de pago con tarjeta de crédito PayPal.

Esto le permite:

* Proporcione varias opciones de pago para sus clientes, incluidos los botones de pago Venmo y PayPal, con la opción de desactivar los campos de tarjeta alojados en PayPal y utilizar un proveedor de tarjeta de crédito existente.
* Utiliza tu proveedor de tarjetas de crédito existente para realizar pagos con tarjeta de crédito, al mismo tiempo que utilizas otras opciones de pago de PayPal.
* Utiliza los botones de pago de PayPal en las regiones donde PayPal no admite tarjetas de crédito como opción de pago.

Para **capturar pagos con _solo_ botones de pago de PayPal (_no_ la opción de pago con tarjeta de crédito de PayPal)**:

1. Asegúrese de que su tienda esté [en modo de producción](settings.md#enable-payment-services).
1. [Configura los botones de pago de PayPal que desees](settings.md#payment-buttons) en Configuración.
1. Desactive _1} la opción **[[!UICONTROL Show PayPal Credit and Debit card button]](settings.md#payment-buttons)**en la sección_[!UICONTROL Payment buttons]_._

Para **capturar pagos con tu proveedor de tarjetas de crédito _y_ botones de pago de PayPal**:

1. Asegúrese de que su tienda esté [en modo de producción](settings.md#enable-payment-services).
1. [Configurar los botones de pago de PayPal](settings.md#payment-buttons) deseados.
1. Desactive _1} la opción **[[!UICONTROL PayPal Show Credit and Debit card button]](settings.md#payment-buttons)**en la sección_[!UICONTROL Payment buttons]_._
1. Desactiva _1} la opción **[[!UICONTROL Show on checkout page]](settings.md#credit-card-fields)**de la sección_[!UICONTROL Credit card fields]_ y usa tu [cuenta de proveedor de tarjeta de crédito existente](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/payments/payments.html#payments)._

## Recalculación de pedidos

Cuando un cliente introduce el flujo de cierre de compra desde el minicarrito, el carro de compras o la página de producto, se le dirige a una página de revisión de pedidos donde puede ver la dirección de envío seleccionada en una ventana emergente de PayPal. Una vez que el cliente selecciona el método de envío, el importe del pedido se vuelve a calcular correctamente y el cliente puede ver los costes e impuestos de envío.

Cuando un cliente introduce el flujo de cierre de compra desde la página de cierre de compra, el sistema ya tiene conocimiento de la dirección de envío y de la cantidad calculada final, y los totales se representan correctamente.

Las vacaciones fiscales, los gastos de envío y los impuestos sobre las ventas pueden variar considerablemente de una ubicación a otra. Una vez que [!DNL Payment Services] recibe la dirección de envío y la tarifa, vuelve a calcular rápidamente todos los costos aplicables y los muestra correctamente durante las últimas etapas del cierre de compra.

## Bóveda de tarjetas de crédito

Los compradores pueden guardar la información de su tarjeta de crédito para futuras compras en el sitio web (cualquier tienda dentro de la cuenta del mismo comerciante).

Consulte [Avalúo de tarjetas de crédito](vaulting.md) para obtener más información.

## Seguridad

Consulte [Cumplimiento de PCI](security.md#pci-compliance) para obtener más información.
