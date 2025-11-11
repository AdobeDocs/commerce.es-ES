---
title: Notas de la versión [!DNL Payment Services]
description: Revise las notas de la versión para obtener información acerca de todas las  [!DNL Payment Services] versiones.
exl-id: 104aa2c7-7735-4ac2-8ed1-a03cd9911273
feature: Payments, Release Notes
source-git-commit: a1c02122cd58234268ba9f07aaba96f83f929720
workflow-type: tm+mt
source-wordcount: '4332'
ht-degree: 0%

---


# Notas de la versión

Estas notas de la versión describen la versión inicial de [!DNL Payment Services] e incluyen:

![Nuevas](../assets/new.svg) nuevas características
![Se ha corregido un problema](../assets/fix.svg) Correcciones y mejoras
![Problema conocido](../assets/bug.svg) Problemas conocidos

Para ver los cambios y correcciones de características publicados fuera de la versión normal de la funcionalidad, consulte las secciones _Actualizaciones de servicios alojados_.

Obtenga más información acerca de las próximas versiones, soporte de productos y qué versiones de Adobe Commerce admiten la extensión [!DNL Payment Services]. Consulte los temas [Programación de versiones](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule) y [Disponibilidad del producto](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability) de Adobe Commerce.

## Actualizaciones de servicios alojados

Estas notas de la versión describen los cambios y correcciones de características que se produjeron y que se lanzaron fuera de las versiones de funciones normales para el servicio alojado.

+++Actualizaciones de servicios alojados

_25 de abril de 2025_

![Nuevo problema](../assets/new.svg)<!-- Issue PAY-6051 --> Ahora, el panel [!DNL Payment Services] muestra tanto la versión de la extensión actual como la versión del panel.

_30 de agosto de 2024_

![Nuevo problema](../assets/new.svg)<!-- Issue PAY-5658 --> Ahora, los comerciantes pueden filtrar las transacciones según los detalles de pago del [informe de transacciones](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html) para obtener datos de métodos de pago más detallados y precisos.

_15 de julio de 2024_

![Nuevo problema](../assets/new.svg)<!-- Issue PAY-5571 --> Ahora, los comerciantes pueden filtrar las transacciones por el correo electrónico del cliente de Commerce en el [informe de transacciones](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html). Introduzca el correo electrónico del cliente para filtrar las transacciones de ese correo electrónico específico.

_9 de julio de 2024_

![Nuevo problema](../assets/new.svg)<!-- Issue PAY-5488 --> Ahora, los comerciantes pueden ver el ID de cliente de Commerce como una columna en el [informe de transacciones](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html) para ayudar a identificar las transacciones que ha realizado un cliente en particular. Además, los comerciantes pueden filtrar el informe de transacciones por este ID de cliente de Commerce para los pedidos asociados.

_5 de marzo de 2024_

![Se ha corregido un problema](../assets/fix.svg)<!-- Issue PAY-5252 --> Ahora, los comerciantes pueden copiar datos de las cuadrículas de tableros seleccionando el contenido de una sola celda.

_10 de octubre de 2023_

![Nuevo problema](../assets/fix.svg)<!-- Issue PAY-4888 --> Ahora, los comerciantes pueden filtrar las transacciones de tarjetas de crédito y débito por los últimos cuatro dígitos del número de tarjeta en el [informe de transacciones](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html).

_12 de julio de 2023_

![Se ha solucionado un problema](../assets/fix.svg)<!-- Issue PAY-4587 --> que se introdujo en la versión [!DNL Payment Services] 2.1.0 y que impedía que las versiones de extensiones anteriores anularan la autorización. Los comerciantes que usen cualquier versión de [!DNL Payment Services] pueden anular las autorizaciones.

_9 de junio de 2023_

![Nuevo](../assets/new.svg)<!-- Issue PAY-4288 --> Ahora, los comerciantes pueden [configurar _solo_ botones de pago de PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#use-only-paypal-payment-buttons)—y _no_ usar la opción de pago con tarjeta de crédito de PayPal. Esto permite a los comerciantes proporcionar varias opciones de pago, incluidos los botones de pago Venmo y PayPal, y utilizar un proveedor de tarjetas de crédito existente en lugar de la opción de pago con tarjeta de crédito PayPal.

![Nuevo](../assets/new.svg)<!-- Issue PAY-4050 --> agregó una [vista de visualización de datos](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#order-payment-status-data-visualization-view), que aparece en la página de inicio de Payment Service, para el informe de estado de pago del pedido.

![Se ha corregido un problema](../assets/fix.svg)<!-- Issue PAY-4486--> Anteriormente, el botón PayPal Paylater no aparecía en el cierre de compra de los comerciantes del Reino Unido. Ese problema está resuelto.

![Se ha corregido un problema](../assets/fix.svg)<!-- Issue PAY-4485--> Las vistas de visualización de datos de informe ahora aparecen en la página de inicio de [!DNL Payment Services] cuando [!DNL Payment Services] está deshabilitado.

_25 de enero de 2023_

![Problema conocido](../assets/bug.svg)<!-- Issue PAY-4102 --> Las nuevas instalaciones de [!DNL Payment Services] no pueden configurar los servicios de Commerce, lo que hace que [!DNL Payment Services] no funcione. Para solucionar este problema, actualice la extensión [!DNL Payment Services] a la versión 1.5.3.

_12 de septiembre de 2022_

![Nuevo](../assets/new.svg)<!-- Issue PAY-3705 --> `increment_id` ya está disponible para su uso en la reconciliación de pagos en sistemas ERP externos. Se propaga a [`custom_id` _y_ `invoice_id`](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/data.html#reconcile-with-erp-system), visibles tanto en el webhook de PayPal como en el detalle de la actividad del comerciante para un pago.

_31 de agosto de 2022_

![Problema corregido](../assets/fix.svg)<!-- Issue PAY-3629 --> Cuando un nuevo comerciante accede a la página de inicio de [!DNL Payment Services] por primera vez, la página ahora se carga inmediatamente para mostrar el contenido en lugar de requerir una actualización de la página.

_9 de agosto de 2021_

![Nuevo](../assets/new.svg)<!-- Issue PAY-3420 --> Apple Pay ya está disponible como botón inteligente de PayPal. Esta [opción de pago](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-options.html#apple-pay-button) permite que los clientes usen la función Touch ID en su dispositivo iOS o macOS para seleccionar Apple Pay. Apple Pay procesa el pago mediante las credenciales de pago de la tarjeta de crédito y débito almacenadas en el dispositivo.

_28 de junio de 2021_

![Nuevas](../assets/new.svg)<!-- Issue PAY-1720 --> disputas por pedidos de tienda ya están disponibles en [el informe de estado de pago del pedido](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#view-disputes). Puedes resolver disputas navegando directamente al Centro de resolución de PayPal desde [!DNL Payment Services].

![Nuevas](../assets/new.svg)<!-- Issue PAY-2854 --> mejoras en la experiencia del usuario desde la página de inicio de [!DNL Payment Services] incluyen la posibilidad de modificar una configuración en el nivel de herencia actual y mejoras en la visualización del encabezado y la navegación.

![Nuevo](../assets/new.svg)<!-- Issue PAY-2854 --> Ahora puede ver advertencias cuando cambie del modo de zona protegida al modo de producción y cuando intente salir de una vista con actualizaciones que no se hayan guardado.

![Nuevo](../assets/new.svg)<!-- Issue PAY-2761 --> Ahora puede personalizar los datos que se muestran en el [informe de estado de pago del pedido](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#show-and-hide-columns) y en el [informe Pagos](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/payouts.html#show-and-hide-columns) mostrando u ocultando columnas mediante el control Configuración de columna.

+++

>[!NOTE]
>
> Las versiones se producen con frecuencia para ofrecer nuevas funciones y correcciones según sea necesario. La programación de versiones no está fija.

## Versión 2.13.0

_10 de noviembre de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg)<!-- PAY-xxxx --> Ahora, [!DNL Payment Services] admite el modal **Pago único (OTC)** de PayPal, que incluye información de contacto y envío integrada.

![Nueva](../assets/new.svg)<!-- PAY-xxxx --> experiencia móvil mejorada mediante **autenticación mediante conmutador de aplicación PayPal**, junto con una integración de API mejorada para recorridos de usuario más suaves. Esta característica solo está disponible para los clientes de EE. UU. basados en [!DNL Payment Services].

![Nuevo](../assets/new.svg)<!-- PAY-xxxx --> agregó compatibilidad con **Autenticación 3D segura (3DS)** para Fastlane para cumplir con los requisitos de **Autenticación sólida del cliente (SCA)**. Esto permite a los comerciantes de [!DNL Payment Services] del Reino Unido y la UE procesar transacciones con **autenticación 3DS**, lo que mejora la prevención del fraude y garantiza el cumplimiento de las regulaciones regionales.

![Nuevo](../assets/new.svg)<!-- PAY-xxxx --> Ahora, [!DNL Payment Services] comerciantes pueden elegir entre **temas claros y oscuros** para el componente de cierre de compra de Fastlane, lo que permite que las páginas de cierre de compra coincidan con el diseño de su sitio. Si los estilos personalizados no cumplen los estándares de accesibilidad, el sistema vuelve automáticamente a la configuración predeterminada.

![Se corrigió un problema](../assets/fix.svg)<!-- PAY-xxxx --> en el cargador durante el cierre de compra de **admin con desafío 3DS**.

![Se ha solucionado un problema](../assets/fix.svg)<!-- PAY-xxxx --> Se ha mejorado la validación de **al almacenar la configuración de pago** mediante la API.

## Versión 2.12.2

_23 de septiembre de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Problema corregido](../assets/fix.svg)<!-- PAY-6275 -->: se rechazaron [!DNL Fastlane] transacciones en modo de captura y ya no se crean pedidos en Commerce.

## Versión 2.12.1

_18 de septiembre de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Problema corregido](../assets/fix.svg)<!-- PAY-6164 --> Ahora, [!DNL Payment Services] usa la moneda base para los métodos de envío disponibles en la **devolución de llamada de envío de PayPal del lado del servidor (SSSC)**.

![Se ha corregido un problema](../assets/fix.svg)<!-- PAY-6267 --> El bloque **Enviar a** está oculto en la página de pago cuando se selecciona **Recogida en tienda (ISPU)**.

![Problema corregido](../assets/fix.svg)<!-- PAY-6271 --> Ahora, [!DNL Payment Services] muestra los detalles guardados de la tarjeta de crédito desde PayPal PayFlow en la sección **Cuenta de cliente** > **Métodos de pago almacenados**.

## Versión 2.12.0

_20 de agosto de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg)<!-- PAY-6022 --> [Fastlane](https://experienceleague.adobe.com/en/docs/commerce/payment-services/payments-checkout/payments-options) ofrece una compra más rápida durante los pagos de los huéspedes.

![Nuevo](../assets/new.svg)<!-- PAY-6168 --> agregó la mutación [`addProductsToNewCart`](https://developer.adobe.com/commerce/webapi/graphql/payment-services-extension/mutations/) a [!DNL Payment Services] para permitir transiciones más suaves y una mejor reutilización del carro de compras.

![Nuevo](../assets/new.svg)<!-- PAY-6169 --> agregó la mutación [`setCartAsInactive`](https://developer.adobe.com/commerce/webapi/graphql/payment-services-extension/mutations/) a [!DNL Payment Services] para mejorar la administración del ciclo de vida de las ofertas.

![Nuevo](../assets/new.svg)<!-- PAY-6227 --> Al cerrar la compra con PayPal, [!DNL Payment Services] omite la ventana emergente de confirmación de pedido para agilizar el proceso de compra.

![Nuevo](../assets/new.svg)<!-- PAY-6234 --> agregó una nueva característica para la opción de pago [Pagar más tarde](https://experienceleague.adobe.com/en/docs/commerce/payment-services/payments-checkout/payments-options). Ahora, el configurador de mensajería BNPL proporciona más flexibilidad para mostrar la mensajería BNPL de pago posterior en las páginas de cierre de compra de los clientes.

![Problema corregido](../assets/fix.svg)<!-- PAY-5505 --> Ahora, [!DNL Payment Services] establece el presupuesto como inactivo cuando se cierra una ventana emergente de Google Pay o PayPal en la página del producto.

![Problema corregido](../assets/fix.svg)<!-- PAY-5754 --> [!DNL Payment Services] ya no permite crear pedidos a partir de comillas vacías.

## Versión 2.11.1

_14 de marzo de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Problema corregido](../assets/fix.svg)<!-- PAY-5849 --> Se corrigió un problema que afectaba a [Elementos de línea](line-items.md) durante el cierre de compra. Ahora, [!DNL Payment Services] ha mejorado la confiabilidad del proceso de cierre de compra de **elementos de línea**. Si encuentra un problema similar, póngase en contacto con su representante de ventas de [!DNL Payment Services] para obtener ayuda.

## Versión 2.11.0

_13 de marzo de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores


![Nuevo](../assets/new.svg)<!-- PAY-5938 --> Ahora, [!DNL Payment Services] permite que los comerciantes administren la configuración de pagos para maximizar la flexibilidad de su negocio. Esta versión mejora la capacidad de adjuntar [varias cuentas de PayPal](https://experienceleague.adobe.com/en/docs/commerce/payment-services/configure/settings#use-multiple-paypal-accounts) para las regiones y marcas que admite un comerciante. Nuestro equipo de ventas puede proporcionar un vínculo de incorporación para configurar su sitio web y los ámbitos de visualización de la tienda.

![Nuevo](../assets/new.svg)<!-- PAY-5968 --> Ahora, [!DNL Payment Services] actualiza la configuración del administrador con los valores de **ID de comerciante de PayPal** y **Estado de comerciante de PayPal**. Estos valores proporcionan a los comerciantes una mejor visibilidad del estado de su cuenta PayPal.

![Se ha corregido un problema](../assets/fix.svg)<!-- PAY-5816 --> que restauraba la funcionalidad de pedido normal en [!DNL Payment Services] al resolver un problema que estaba causando errores en todas las ubicaciones de pedidos con la versión v2.9.0.

![Se ha corregido un problema](../assets/fix.svg)<!-- PAY-5825 --> que causaba que el minicarrito de Apple Pay usara una dirección URL de totales estimados incorrecta para los clientes que iniciaron sesión. Ahora, [!DNL Payment Services] garantiza cálculos totales precisos.

![Se ha corregido un problema](../assets/fix.svg)<!-- PAY-5826 --> que mejoraba la confiabilidad de la administración de pedidos al resolver un problema que causaba un error HTTP 500 al cambiar el estado del presupuesto a `inactive`.

![Problema corregido](../assets/fix.svg)<!-- PAY-5849 --> Se corrigió un problema en el cual `LineItemProvider` arrojaba excepciones para cantidades decimales por debajo de 1. Ahora, [!DNL Payment Services] proporciona una mejor compatibilidad con las cantidades fraccionarias.

![Se corrigió un problema](../assets/fix.svg)<!-- PAY-5868 --> Se corrigió un error en la cantidad de la tarjeta regalo durante el cierre de compra. [!DNL Payment Services] ahora garantiza valores precisos durante el proceso de cierre de compra.

![Se corrigió un problema](../assets/fix.svg)<!-- PAY-5911 --> que resolvió errores durante la creación del envío para los pedidos realizados con métodos de pago en línea que no son [!DNL Payment Services], lo que mejoró la confiabilidad general.

![Problema corregido](../assets/fix.svg)<!-- PAY-5954 --> [!DNL Payment Services] ahora ofrece una experiencia de pago y envío más fluida al resolver un problema en el cual Apple Pay no pudo realizar un pedido cuando se seleccionó una tarjeta de crédito diferente en la cartera.

![Problema corregido](../assets/fix.svg)<!-- PAY-5971 --> [!DNL Payment Services] ya no redirige a los clientes a la página de revisión de pedidos cuando Apple Pay falla, lo que evita interrupciones innecesarias en el pago y envío.

## Versión 2.10.3

_24 de febrero de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Se corrigió un problema](../assets/fix.svg)<!-- PAY-xxxx --> que mejoró la estabilidad y el rendimiento general.

![Se corrigió un problema](../assets/fix.svg)<!-- PAY-xxxx -->: mejoras generales y optimizaciones. Se han corregido errores críticos de la versión 2.10.2.

## Versión 2.10.2

_21 de febrero de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Problema conocido](../assets/bug.svg)<!-- PAY-xxxx --> Contiene errores críticos que pueden afectar la estabilidad y el rendimiento. Adobe recomienda actualizar a la versión 2.10.3 en lugar de utilizar esta versión (v2.10.2).

## Versión 2.10.1

_5 de febrero de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg)<!-- PAY-5813 --> agregó compatibilidad con Adobe Commerce 2.4.8 y PHP 8.4.

## Versión 2.10.0

_13 de diciembre de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg)<!-- PAY-5702 --> [!DNL Payment Services] ahora admite puntos finales de GraphQL para el almacenamiento sin compra, lo que permite a los clientes guardar sus métodos de pago sin completar una transacción.

![Nuevo](../assets/fix.svg)<!-- PAY-5789 --> [!DNL Payment Services] ahora admite la autenticación segura [3D con Google Pay](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/security-compliance/security#3ds), lo que mejora la seguridad de los comerciantes y clientes durante las transacciones de pago.

![Corrección](../assets/fix.svg)<!-- PAY-5703 --> [!DNL Payment Services] agrega la capacidad para que [los clientes guarden tarjetas directamente en su **Mi cuenta**](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting), lo que mejora la comodidad y simplifica los cierres de compra futuros. `Vault without purchase functionality might not be 100% compatible with Adobe Commerce 2.4.4 due to a known issue with` [`GraphQL authorization mechanisms`](https://developer.adobe.com/commerce/webapi/graphql/usage/authorization-tokens/).

![Corregir](../assets/fix.svg)<!-- PAY-5762 --> Se corrigió un problema en el cual los códigos de cupones no se aplicaban en la página de revisión de pedidos cuando el pedido se iniciaba desde la página de detalles del producto (PDP).

![Corrección](../assets/fix.svg)<!-- PAY-5792 --> [!DNL Payment Services] ahora muestra descripciones y direcciones de facturación para las tarjetas [abovedadas en la página de cierre de compra](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting), lo que da a los clientes más visibilidad sobre sus métodos de pago guardados.

![Corrección](../assets/fix.svg)<!-- PAY-5793 --> [!DNL Payment Services] permite que los comerciantes almacenen la dirección de facturación de las tarjetas de débito directamente desde la página de pago, lo que garantiza información de pago precisa y completa.

## Versión 2.9.0

_7 de noviembre de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg)<!-- PAY-5629 --> [!DNL Payment Services] ahora admite una **URL de SDK actualizada para Apple Pay**, lo que mejora la integración para los comerciantes que usan Apple Pay. Esta función es compatible con macOS 14 y versiones posteriores, los dispositivos que ejecuten versiones anteriores de macOS no mostrarán esta funcionalidad.

![Nuevo](../assets/new.svg)<!-- PAY-5630 --> actualizó las páginas de **Pago y envío**, **Producto**, **Carro** y **Minicarrito** para admitir la URL de SDK **actualizada para Apple Pay**, lo que mejora la experiencia del usuario para los comerciantes que ofrecen Apple Pay como opción de pago.

![Nuevo](../assets/new.svg)<!-- PAY-5635 --> Se mejoraron las estimaciones de envío **según la dirección de Apple Pay**, lo que permite a los clientes ver los costos de envío precisos durante el cierre de compra.

![Corregir](../assets/fix.svg)<!-- PAY-5661 --> Se corrigieron varios **[!DNL Payment Services]problemas en el cierre de compra**, lo que mejora la confiabilidad del proceso de pago para comerciantes y compradores.

![Corregir](../assets/fix.svg)<!-- PAY-5692 --> Se ha corregido un problema por el que los nombres y apellidos del **cliente** no se agregaban al pedido al usar **botones inteligentes para la desprotección rápida**.

![Corrección](../assets/fix.svg)<!-- PAY-5712 --> Resolvió un problema en el cual los comerciantes no podían completar el cierre de compra mediante la opción de pago Subtotal cero del cierre de compra **cuando la cantidad total era gratuita.**

## Versión 2.8.1

_13 de septiembre de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Se ha corregido](../assets/fix.svg)<!-- PAY-5644 --> un problema con la memoria caché de los parámetros de SDK al usar varios ámbitos en [!DNL Payment Services]. La configuración de SDK ahora se almacena en caché por separado para cada ámbito en lugar de en una sola clave. Esto garantiza que la caché de cada ámbito se invalide de forma independiente, lo que mejora la fiabilidad al administrar varios ámbitos.

## Versión 2.8.0

_13 de septiembre de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg)<!-- PAY-5499 --> [!DNL Payment Services] admite ahora el envío de información de número de seguimiento a PayPal cuando se introduce un [número de seguimiento](track-shipment.md) en Adobe Commerce.

![Corrección](../assets/fix.svg)<!-- PAY-5626 --> [!DNL Payment Services] ha optimizado el proceso de solicitud en el registro de comerciantes cuando los clientes visitan la página de cierre de compra de Commerce. Anteriormente, se realizaban solicitudes independientes para cada forma de pago (campos alojados, Google Pay, Apple Pay y botones inteligentes). Esta mejora reduce el número de llamadas, lo que mejora el rendimiento y la eficacia durante el proceso de cierre de compra.

![Corrección](../assets/fix.svg)<!-- PAY-5645 --> [!DNL Payment Services] evita ahora que se abra la ventana emergente PayPal/Google Pay si el comprador no ha aceptado que el comerciante cree términos y condiciones personalizados en la página de pago.

![Corrección](../assets/fix.svg)<!-- PAY-5648 -->  [!DNL Payment Services] ha solucionado un problema relacionado con el desglose de impuestos por elemento de línea en el portal de PayPal. Si el coste de envío de un pedido tiene impuestos asociados, el impuesto se incluirá como parte del coste de envío y se podrá ver de esta manera en los detalles del artículo de línea que se muestran en el portal de PayPal.

## Versión 2.7.0

_2 de agosto de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg)<!-- PAY-4844 --> [!DNL Payment Services] ahora admite [datos de elemento de línea en el nivel de pedido](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/payments-checkout/manage/line-items). Esta función permite a los comerciantes ver información detallada sobre los artículos de un pedido, como detalles del producto, cantidad y precio (incluidos impuestos, descuentos y otra información relevante).

![Nuevo](../assets/new.svg)<!-- PAY-5380 --> [!DNL Payment Services] mejora la configuración de [en la experiencia del administrador](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/configure/configure-admin#general-configuration) para los comerciantes con el fin de lograr un proceso de incorporación más fácil e intuitivo. Esta característica permite a los comerciantes restablecer sus [!DNL Payment Services] ID.

![Nuevo](../assets/new.svg)<!-- PAY-5255 --> [!DNL Payment Services] incluye una [notificación de error en el pago](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-payment-failed-emails). Esta función proporciona notificaciones casi en tiempo real de errores de pago a los comerciantes, de modo que los pedidos se pueden guardar poniéndose en contacto con el comprador y mejorando potencialmente la resolución del problema.

![Corrección](../assets/fix.svg)<!-- PAY-5469 --> Se ha corregido un problema por el que Safari bloqueaba la ventana emergente de **Google Pay**. Los compradores ahora pueden completar sus transacciones de pago de Google Pay en Safari.

![Corregir](../assets/fix.svg)<!-- PAY-5492 --> Se corrigió un problema que se producía cuando un comerciante agrega términos y condiciones personalizados a la página de cierre de compra. Durante un [pago y envío exprés](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options#standard-vs-advanced-payments-experience), un comprador ahora puede aceptar estos términos y condiciones para completar el pago y envío sin problemas.

![Corrección](../assets/fix.svg)<!-- PAY-5532 --> mejoró las funciones de recogida en tienda (ISPU) con **InstantPurchase**. Los **métodos de entrega ISPU** ya no se muestran cuando un comprador realiza un pedido con **InstantPurchase**.

![Corrección](../assets/fix.svg)<!-- PAY-5606 --> Se ha corregido un problema en el selector de país de **Página de configuración** que se producía cuando el país del comerciante está establecido en **Alemania**.

## Versión 2.6.0

_4 de junio de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg)<!-- PAY-4877 --> Ahora, [!DNL Payment Services] admite [funciones de precios L2/L3](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/levels-card-payment-transactions.html). Esta función solo está disponible para [!DNL Payment Services] clientes con los precios de IC++ habilitados. Si desea usar datos de procesamiento L2/L3 para [!DNL Payment Services], póngase en contacto con el administrador de cuentas de [!DNL Payment Services].

![Corrección](../assets/fix.svg)<!-- PAY-5455 -->[!DNL Payment Services] le permite habilitar Apple Pay directamente desde la extensión sin descargar ni alojar el [archivo de asociación de dominios](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain).

## Versión 2.5.0

_23 de abril de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Corrección](../assets/fix.svg)<!-- Issue PAY-5396 -->[!DNL Payment Services] ahora admite [directrices de Adobe Commerce para el parámetro `--db-prefix`](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/advanced#install-from-the-command-line) para las versiones 2.4.7 y posteriores de Adobe Commerce.

## Versión 2.4.3

_16 de abril de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Corregir](../assets/fix.svg)<!-- Issue PAY-5106 --> Se ha corregido un problema que llenaba incorrectamente los totales de la cantidad del pedido durante el cierre de compra entre PayPal y Adobe Commerce. Ahora, los comerciantes pueden asegurarse de que los totales de la cantidad del pedido son correctos al realizar un pedido.

## Versión 2.4.2

_11 de abril de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg)<!-- Issue xxx --> agregó compatibilidad con Adobe Commerce 2.4.7.

## Versión 2.4.1

_4 de abril de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Corregir](../assets/fix.svg)<!-- PAY-5322 --> Se corrigió un problema de compatibilidad con PCI en las versiones más recientes de Adobe Commerce. Ahora, [!DNL Payment Services] está adaptado a los requisitos de cierre de compra en Adobe Commerce como opción de pago.

![Corregir](../assets/fix.svg)<!-- PAY-5323 --> Paylater y Venmo se muestran correctamente en Adobe Commerce. Se ha corregido un error que impedía que el administrador mostrara las opciones de alternancia PayAfter y Venmo.

## Versión 2.4.0

_20 de marzo de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Los nuevos comerciantes](../assets/new.svg)<!-- PAY-4868 --> pueden [configurar Google Pay correctamente durante toda la experiencia de compra](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html), de forma similar a otros botones de pago en [!DNL Payment Services] a través del administrador.

![Nuevo](../assets/new.svg)<!-- PAY-4381 --> [Payment Services admite Google Pay a través de GraphQL](https://developer.adobe.com/commerce/webapi/graphql/payment-services/), lo que permite a los comerciantes tener una experiencia Commerce sin encabezado con el método de pago Google Pay.

![Nuevo](../assets/new.svg)<!-- PAY-4878 --> Ahora, la característica de cierre de compra básica de [!DNL Payment Services] está incluida para los comerciantes de Adobe Commerce y Magento Open Source.[!DNL Payment Services] ahora puede admitir comerciantes con negocios en cualquiera de las 200 regiones geográficas de todo el mundo.El proceso de pago y envío básico de [!DNL Payment Services] proporciona opciones de débito/crédito, PayPal, Venmo (cuando esté disponible) y PayAfter (cuando esté disponible) en una incorporación de autoservicio.

![Corregir](../assets/fix.svg)<!-- PAY-5291 --> Es posible que se retrase la recepción de la confirmación de pago de algunas transacciones. En ese caso, ahora los comerciantes pueden obtener un estado de pago actualizado para un pedido. [Servicios de pago detecta el estado pendiente de una transacción de pago](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html) en un pedido mediante la detección de transacciones pendientes, la supervisión proactiva de estas transacciones y la actualización cuando se ha capturado el estado pendiente.

## Versión 2.3.4

_1 de marzo de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg)<!-- PAY-5244 -->: se corrigió la compatibilidad de desprotección asincrónica.

![Corrección](../assets/fix.svg)<!-- PAY-5253 --> Se ha corregido un error por el que no se pudo eliminar un token de Vault que no pertenecía a [!DNL Payment Services].

## Versión 2.3.3

_14 de febrero de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg)<!-- PAY-5048 --> agregó compatibilidad con PHP 8.3

![Corregir](../assets/fix.svg)<!-- PAY-5048 --> Se corrigió un error con el marcador `is_deleted`. Ahora, los pedidos no fallan debido al estado `Rejected` enviado desde la extensión.

## Versión 2.3.2

_26 de enero de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Corregir](../assets/fix.svg)<!-- PAY-5183 --> problemas de rendimiento de REST/GraphQL corregidos. Ahora, el botón de tarjeta de crédito se procesa cuando se obtiene a través de la API.

## Versión 2.3.1

_7 de diciembre de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg)<!-- PAY-5047 --> El tipo de método de pago o marca de tarjeta de crédito/débito ya está disponible en las siguientes ubicaciones:

- la página pedido del cliente en la tienda
- el correo electrónico de confirmación del pedido enviado al comprador
- desde la [vista de detalles del pedido](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/order-management/orders/order-processing.html#view-an-order) en el administrador de Commerce.

## Versión 2.3.0

_1 de diciembre de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg)<!-- PAY-4381 --> [Servicios de pago ahora admite la integración con GraphQL](https://developer.adobe.com/commerce/webapi/graphql/payment-services/). Con la compatibilidad de GraphQL con los botones de pago de PayPal, los campos hospedados y Apple Pay,[!DNL Payment Services] ahora admite una configuración de Commerce sin encabezado.

## Versión 2.2.1

_27 de septiembre de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Se ha corregido un problema](../assets/fix.svg)<!-- Issue PAY-4870 --> que causaba que el nuevo atributo de encabezado se rellenara incorrectamente en Storefront al enviar la versión de extensión con la última versión. Anteriormente, con la versión `1.3.0` del conector de servicios de Commerce, no se podía extender `User-Agent header` desde la extensión [!DNL Payment Services].

## Versión 2.2.0

_30 de agosto de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg)<!-- PAY-4638 --> agregó una integración de [con Signifyd](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/security-compliance/fraud-protection.html), que proporciona servicios automatizados de protección contra fraudes.

![Nuevo](../assets/new.svg)<!-- PAY-3981 --> [Se ha promocionado Apple Pay a una opción de pago independiente](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html?lang=en#apple-pay-button), fuera de los botones de pago de PayPal, para aumentar la visibilidad del comprador de la opción de pago y para permitir que los comerciantes controlen la colocación y el estilo de Apple Pay.

![Nuevo](../assets/new.svg)<!-- PAY-4002 -->: se ha mejorado la experiencia del usuario con el pago de los campos de tarjeta de crédito, incluidas mejoras de estilo como la adición de iconos de pago, para reducir la carga cognitiva del comprador y aumentar las conversiones.

![Nueva](../assets/new.svg)<!-- PAY-4002 --> funcionalidad agregada para permitir que los comerciantes [ordenen el orden de sus opciones de pago](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#payment-buttons) para priorizar ciertas opciones de pago. Esta funcionalidad promueve una mayor tasa de conversación de cierre de compra.

Los ![nuevos](../assets/new.svg)<!-- PAY-4035 --> comerciantes ahora pueden supervisar de manera eficaz el estado de sus tiendas e identificar cualquier problema de transacción mediante el nuevo [informe de transacciones](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html) disponible en la página de inicio del administrador de [!DNL Payment Services]. El informe también presenta datos sobre las tasas de autorización de transacciones y las tendencias negativas de las transacciones.

## Versión 2.1.0

_9 de junio de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg)<!-- Issue xxx --> agregó compatibilidad con Adobe Commerce 2.4.7-beta1.

![Nuevo](../assets/new.svg)<!-- Issue xxx --> agregó [disponibilidad en los siguientes países y monedas asociadas](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html#availability): Australia, Francia, Reino Unido.

![Nuevo](../assets/new.svg)<!-- Issue PAY-4296 --> agregó [recursos ampliados para roles de administrador](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#configure-roles) para garantizar que los usuarios administradores puedan crear y administrar pedidos para clientes y puedan ver[!DNL Payment Services] en el menú Ventas.

![Nuevo](../assets/new.svg)<!-- Issue PAY-4236 --> agregó [anulación automática para pedidos que incurren en errores durante el cierre de compra](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/checkout.html#order-auto-voided-if-error).

![Nueva](../assets/new.svg)<!-- Issue PAY-4183 --> funcionalidad creada para [mostrar el botón de opción de pago con tarjeta de crédito/débito](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#debit-or-credit-card-button) en la página de pago.

## Versión 2.0.0

_10 de marzo de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg)<!-- Issue PAY-4152 --> agregó compatibilidad con PHP 8.2 y Adobe Commerce 2.4.6. No compatible con PHP 7.x.

## Versión 1.6.1

_10 de marzo de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Corregir](../assets/fix.svg)<!-- Issue PAY-4226 --> Se ha corregido un problema que impedía que los nuevos comerciantes de [!DNL Payment Services] usaran el cierre de compra en el Administrador.[!DNL Payment Services] estaba usando anteriormente el ID de cliente de Commerce, que no existe para los clientes nuevos.

![Corregir](../assets/fix.svg)<!-- Issue PAY-4205 --> Se ha corregido un problema que causaba que el estado de la dirección de envío especificada se reemplazara por el estado de la configuración de impuestos predeterminada durante el cierre de compra mediante la [opción PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#paypal-smart-buttons). Ahora, los clientes pueden enviar sus pedidos a un estado distinto del configurado como predeterminado en la configuración de impuestos del comerciante.

![Corregir](../assets/fix.svg)<!-- Issue PAY-4202 --> Se ha corregido un problema que impedía a los clientes usar el depósito de tarjetas para completar una compra o eliminar un método de pago abovedado para una tienda [mediante la acción de pago `Authorize and Capture`](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/production.html#set-payment-services-as-payment-method). Anteriormente, aparecía el error &quot;No se encontró el ID de Provider Vault&quot; cuando el cliente intentaba utilizar o modificar sus tarjetas de crédito abovedadas.

## Versión 1.6.0

_17 de febrero de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.0 y posteriores

![Nuevo](../assets/new.svg)<!-- Issue PAY-3540 --> agregó [característica de cumplimiento de PCI 3DS para comerciantes que realizan transacciones en la Unión Europea (UE) y Gran Bretaña](security.md#3ds). Este nivel adicional de seguridad, que requiere que los compradores se autentiquen con el emisor de su tarjeta de crédito, ayuda a evitar el fraude en línea y es necesario como parte de las regulaciones de cumplimiento de la Unión Europea (UE).

![Nuevo](../assets/new.svg)<!-- Issue PAY-3609 --> agregó la capacidad para [habilitar el almacenamiento de tarjetas en el administrador](vaulting.md#use-vaulting-in-the-admin). Esto permite a los comerciantes crear un pedido para los clientes en Admin mediante sus métodos de pago abovedados.

## Versión 1.5.4

_29 de enero de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.0 y posteriores

![Se ha solucionado un problema](../assets/fix.svg)<!-- Issue PAY-4110 --> que impedía a los compradores realizar un pedido con botones de pago en la página del producto, el minicarrito y el carrito. Los compradores ahora pueden completar los pedidos correctamente.

## Versión 1.5.3

_25 de enero de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.0 y posteriores

![Se corrigió un problema](../assets/fix.svg)<!-- Issue PAY-4102 --> que liberó una corrección de un problema conocido incompatible con versiones anteriores. Esta versión bloquea la versión de la extensión de ID de servicio a la última versión estable, que vuelve a habilitar las nuevas instalaciones de [!DNL Payment Services] para configurar los servicios de Commerce.

## Versión 1.5.2

_22 de diciembre de 2022_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.0 y posteriores

![Se corrigió un problema](../assets/fix.svg)<!-- Issue PAY-3992 --> Se mejoró la facturación en [!DNL Payment Services] cuando se rechazó un método de pago.

![Se ha corregido un problema](../assets/fix.svg)<!-- Issue PAY-3999 -->[!DNL Payment Services] que ahora muestra correctamente los botones de pago de PayPal para los comerciantes que usan la plantilla personalizada [Fire Checkout](https://commercemarketplace.adobe.com/swissup-firecheckout.html){target=_blank} para la página de pago. Anteriormente, la minicart mostraba los botones de forma intermitente.

## Versión 1.5.1

_23 de noviembre de 2022_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.0 y posteriores

![Nuevo](../assets/new.svg)<!-- Issue PAY-3923 -->[!DNL Payment Services] ahora incluye el número de versión en el encabezado del agente de usuario para que las solicitudes puedan rastrear, filtrar o eliminar los extremos no utilizados.

![Problema corregido](../assets/fix.svg)<!-- Issue PAY-3968 -->[!DNL Payment Services] ahora muestra correctamente los datos del pedido cuando se realiza un pedido desde la página del producto mediante botones de pago.

## Versión 1.5.0

_18 de noviembre de 2022_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.0 y posteriores

![Nuevo](../assets/new.svg)<!-- Issue PAY-3880 --> Un comprador ahora puede [guardar (guardar) la información de su tarjeta de crédito durante el cierre de compra](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting.html) para usarla en una compra posterior para la misma tienda o para otra dentro de la misma cuenta de comerciante.

Los comerciantes de ![New](../assets/new.svg)<!-- Issue PAY-3950 --> ahora pueden habilitar la función [Instant Purchase Commerce](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/checkout-instant-purchase.html) para sus tiendas, de modo que los compradores puedan (usar [información de tarjeta de crédito abovedada](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting.html)) adelantar el cierre de compra.

## Versión 1.4.1

_14 de octubre de 2022_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.0 y posteriores

![Corregir](../assets/fix.svg)<!-- Issue PAY-3766 --> Cuando se rechaza el método de pago de un cliente, el mensaje de error visible es más descriptivo. Aconseja al cliente que vuelva a introducir la información de pago y vuelva a intentarlo, pruebe otra forma de pago o que se ponga en contacto con su banco para informarle de la transacción rechazada.

## Versión 1.4.0

_30 de septiembre de 2022_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.0 y posteriores

![Nuevo](../assets/new.svg)<!-- Issue PAY-784 -->[!DNL Payment Services] ahora incluye la capacidad de configurar una cuenta comercial para [usar varias cuentas comerciales de PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#use-multiple-paypal-accounts). Esto permite al comerciante operar sus tiendas en varios países utilizando diferentes monedas, o usar Adobe Commerce para una parte de su negocio.

![Nuevos](../assets/new.svg)<!-- Issue PAY-3231 --> Comerciantes pueden [agregar un [!UICONTROL Soft Descriptor]](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#add-soft-descriptor) a sitios web o a configuraciones de vistas de tiendas individuales que se muestran en los extractos bancarios de las transacciones de los clientes para delinear marcas, tiendas o líneas de productos.

![Nuevo](../assets/new.svg)<!-- Issue PAY-3707 --> [Activar o desactivar los campos de tarjeta de crédito y los botones de pago de PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#configure-payment-options) para el cierre de compra en la configuración de [!DNL Payment Services].

![Problema corregido](../assets/fix.svg)<!-- Issue PAY-3546 --> Cuando un cliente hace clic en **[!UICONTROL Edit cart]**, la página redirige a la página del carro y muestra los elementos actualizados en lugar de mostrar un carro vacío.

## Versión 1.3.1

_6 de septiembre de 2022_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.0 y posteriores

![Problema corregido](../assets/fix.svg)<!-- Issue PAY-3663 --> Ahora, cuando un almacén de un comerciante está capturando un pedido autorizado con una moneda no global, el proceso de captura se completa y no se muestra ningún error.

## Versión 1.3.0

_9 de agosto de 2022_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.0 y posteriores

![Nueva](../assets/new.svg)<!-- Issue PAY-XX --> versión de disponibilidad general—[!DNL Payment Services] ahora es [compatible con [!DNL Adobe Commerce] y [!DNL Magento Open Source] versiones 2.4.0 a 2.4.5](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

![Se ha corregido un problema](../assets/fix.svg)<!-- Issue PAY-x --> Apple Pay ahora es compatible con el navegador Safari versión 15.5 en equipos móviles y de escritorio.

## Versión 1.2.0

_29 de junio de 2022_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.0 y posteriores

![Problema conocido](../assets/bug.svg)<!-- Issue PAY-x -->: Apple Pay no es compatible con el navegador Safari v15.5 en dispositivos móviles y de escritorio. Al utilizar la versión 15.5 de Safari, no puedes completar el proceso de pago y envío con Apple Pay.

![Se ha corregido un problema](../assets/fix.svg)<!-- Issue PAY-3264 --> Anteriormente, cuando un usuario que iniciaba sesión seleccionaba una dirección de facturación/envío distinta de la predeterminada para su cuenta, se producía un error al realizar la desprotección. Ahora, se envía la dirección de facturación/envío seleccionada (en lugar de la dirección guardada predeterminada) y el cierre de compra se completa correctamente.

![Problema corregido](../assets/fix.svg)<!-- Issue PAY-3314 --> Si deshabilita los botones de pago de PayPal para el cierre de compra, no se mostrarán errores.

![Problema corregido](../assets/fix.svg)<!-- Issue PAY-3330 --> Los pagos ya no fallan durante el cierre de compra cuando un usuario invitado introduce un número de teléfono que incluye guiones.

![Se ha corregido un problema](../assets/fix.svg)<!-- Issue PAY-3338 PAY-2502 -->. Cuando las credenciales de los servicios de Commerce no son válidas,[!DNL Payment Services] ahora le alerta mostrándole un error de credenciales desde la página de inicio de [!DNL Payment Services] en el Administrador.

![Problema conocido](../assets/bug.svg)<!-- Issue PAY-0 --> [!DNL Payment Services] es incompatible con `commerce-data-export` v101.20 y versiones posteriores, lo que lo hace incompatible con la [[!DNL Channel manager] extensión](https://experienceleague.adobe.com/docs/commerce-channels/channel-manager/guide-overview.html).

## Versión 1.1.0

_31 de marzo de 2022_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.0 y posteriores

![Nueva](../assets/new.svg)<!-- Issue PAY-2127 --> versión de disponibilidad general—[!DNL Payment Services] ahora es [compatible con [!DNL Adobe Commerce] y [!DNL Magento Open Source] versiones 2.4.0 a 2.4.4](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

![Nuevo](../assets/new.svg)<!-- Issue PAY-2682 --> La extensión [!DNL Payment Services] para [!DNL Adobe Commerce] y [!DNL Magento Open Source] ya está disponible para los comerciantes canadienses. Los comerciantes pueden ver la configuración de pagos en [francés](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html?lang=fr#carte-de-cr%C3%A9dit-et-devises-accept%C3%A9es) o [inglés](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html#accepted-credit-cards-and-currencies).

![Nuevo](../assets/new.svg)<!-- Issue PAY-2681 --> [!DNL Payment Services] admite [dólares canadienses (CAD)](introduction.md#accepted-credit-cards-and-currencies) para tarjetas de crédito y transacciones de PayPal.

![Nuevos](../assets/new.svg)<!-- Issue PAY-2680 --> comerciantes pueden [incorporar [!DNL Payment Services]](onboard.md) extensión en inglés o francés.

Los comerciantes ![Nuevos](../assets/new.svg)<!-- Issue PAY-2678 --> ahora pueden ver informes financieros, tanto el [estado de pago del pedido](order-payment-status.md) como los [informes de pagos](payouts.md), en dólares canadienses (CAD).

![Se ha corregido un problema](../assets/fix.svg)<!-- Issue PAY-2710 -->[!DNL Payment Services] que ahora es compatible con [PHP 8.1](https://www.php.net/releases/8.1/en.php).

![Se ha corregido un problema](../assets/fix.svg)<!-- Issue PAY-3017 -->. Se mejoró la alerta del modo de espacio aislado para mostrar las alertas adecuadas con varias tiendas.

![Problema corregido](../assets/fix.svg)<!-- Issue PAY-2742 --> Ahora puede habilitar y deshabilitar los métodos de pago disponibles, como Venmo, en el nivel de vista de tienda. Anteriormente, solo se podían configurar métodos de pago por sitio web.

![Problema corregido](../assets/fix.svg)<!-- Issue PAY-2277 --> Ahora puedes [habilitar o deshabilitar de forma selectiva botones de pago de PayPal](configure-admin.md#payment-buttons).

![Se ha corregido un problema](../assets/fix.svg)<!-- Issue PAY-2561 --> Los productos eliminados anteriormente no aparecen en el carro de compras en la página _Revisar pedido_.

![Problema conocido](../assets/bug.svg)<!-- Issue PAY-2842 --> Las transacciones de tarjetas de crédito de prueba [pueden fallar con PayPal](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html) al procesar pagos en un entorno de zona protegida.

## Versión 1.0.0

_29 de noviembre de 2021_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.0 y posteriores

![Nueva](../assets/new.svg)<!-- Issue PAY-2127 --> versión de disponibilidad general—[[!DNL Payment Services]](https://commercemarketplace.adobe.com/magento-payment-services.html) ahora es compatible con [!DNL Adobe Commerce] y [!DNL Magento Open Source] versiones 2.4.0 a 2.4.3-p1.

![Nuevo](../assets/new.svg)<!-- Issue PAY-124 --> La extensión [!DNL Payment Services] para [!DNL Adobe Commerce] y [!DNL Magento Open Source] se puede instalar para [[!DNL Adobe Commerce] instancias de infraestructura en la nube](install.md#adobe-commerce-on-cloud-infrastructure) o [locales](install.md#on-premises). Estos métodos requieren el uso de una interfaz de línea de comandos.

![Nuevo](../assets/new.svg)<!-- Issue PAY-1986 --> [!DNL Payment Services] admite una [cuenta de zona protegida](sandbox.md) que permite a los comerciantes evaluar la extensión en modo de prueba.

Los comerciantes de ![New](../assets/new.svg)<!-- Issue PAY-666 --> pueden [configurar la extensión de Payment Services](configure-admin.md) con comportamientos de pago básicos, como usar [`Authorize and Capture`](production.md#set-payment-services-as-payment-method) para cambiar entre entornos de zona protegida o de producción.

![Nuevo](../assets/new.svg)<!-- Issue PAY-780 --> Tus compradores pueden pagar con [!DNL Payment Services] o a través de [creación manual de pedidos](create-order.md).

![Los informes completos de ](../assets/new.svg)<!-- Issue PAY-1856 -->New[Order payment status](order-payment-status.md) y [Payouts](payouts.md) están disponibles para que [!DNL Payment Services] te dé una visión clara de los pedidos de tu tienda y los pagos relacionados.

![Nuevo](../assets/new.svg)<!-- Issue PAY-311 --> [!DNL Payment Services] admite precios por niveles flexibles, basados en el volumen total de procesamiento, adaptados a cualquier comerciante.

![Nuevo](../assets/new.svg)<!-- Issue PAY-1443 --> Puedes [personalizar fácilmente el aspecto](payments-options.md) de los botones de pago y los campos de tarjeta de crédito de PayPal para la extensión [!DNL Payment Services].

![Problema conocido](../assets/bug.svg)<!-- Issue PAY-2473 -->: el uso de [claves de composición incorrectas](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html) durante la instalación de la extensión impide que el usuario [se autentique](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) con el `MAGEID` correcto.

![Problema conocido](../assets/bug.svg)<!-- Issue PAY-2474 --> [!DNL Payment Services] informes [puede que no se sincronicen inmediatamente](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html).

![Problema conocido](../assets/bug.svg)<!-- Issue PAY-2475 -->: tu [cuenta de zona protegida de PayPal](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html) para [!DNL Payment Services] no se puede comprobar si creas esa cuenta durante la incorporación.
