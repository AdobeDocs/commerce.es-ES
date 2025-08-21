---
title: Notas de la versión
description: La información de la versión más reciente para la extensión  [!DNL Data Connection] de Adobe Commerce.
feature: Personalization, Integration, Release Notes
exl-id: f3b92632-947d-40cd-89b7-24ed0680be51
source-git-commit: 90fcaa2cdd7c869ceddaeea7525cac00a41d94c5
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 1%

---

# Notas de la versión

>[!IMPORTANT]
>
>Se cambió el nombre del conector Experience Platform a [!DNL Data Connection].

Estas notas de la versión contienen actualizaciones para la extensión [!DNL Data Connection] e incluyen:

![Nuevo](../assets/new.svg) - Nuevas características
![Corrección](../assets/fix.svg): correcciones y mejoras
![Error](../assets/bug.svg): problemas conocidos

Para ver los cambios y correcciones de características relacionados con las extensiones utilizadas por la extensión [!DNL Data Connection], consulte **Actualizaciones de servicio compatibles**.

Consulte [Próximas versiones](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule) para obtener más información sobre las programaciones de versiones y la compatibilidad.

Consulte la documentación para desarrolladores para [saber qué versiones de Commerce admiten este módulo](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

## Actualizaciones de servicios compatibles

Estas notas de la versión describen cambios y correcciones de características relacionados con las extensiones utilizadas por la extensión [!DNL Data Connection].

+++Actualizaciones de servicios compatibles

_7 de agosto de 2025_

![Nuevo](../assets/new.svg): con la versión 3.3.0, ahora puede agregar [atributos personalizados a los perfiles](custom-identities.md).

_2 de agosto de 2024_

![Corregir](../assets/fix.svg) - Se corrigió la cantidad total de pagos cuando el total del pedido está configurado para incluir impuestos.
![Nuevo](../assets/new.svg) - Se agregó el campo `taxAmount` a los eventos de compra de pedidos.
![Nuevo](../assets/new.svg) - Se agregó la capacidad de agregar datos personalizados a los eventos. Consulte lo siguiente para ver un [ejemplo](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md).

_24 de enero de 2024_

![Nuevo](../assets/new.svg) - Se ha actualizado la extensión `data-services-b2b` para incluir un nuevo evento de solicitud denominado `deleteRequisitionList` para comerciantes B2B.

_16 de noviembre de 2023_

![Corrección](../assets/fix.svg): se corrigió un problema por el que aparecía incorrectamente un mensaje de error al realizar un pedido con varias direcciones de envío.
![Corrección](../assets/fix.svg): se corrigió un problema en el evento `productPageView` en el que el campo de evento `productListItems.priceTotal` no convertía el precio después de cambiar la moneda en la vista de la tienda.
![Corregir](../assets/fix.svg) - Se corrigió un problema en el campo de evento `productListItems` en el cual el código de moneda no se actualizaba cuando el comerciante cambió la vista de la tienda.

_10 de octubre de 2023_

![Nuevo](../assets/new.svg) - Se agregaron nuevos eventos de estado de pedidos: [Pedido facturado](events-backoffice.md#orderinvoiced), [Devolución de artículo de pedido iniciada](events-backoffice.md#orderitemsreturninitiated) y [Devolución de artículo de pedido completada](events-backoffice.md#orderitemreturncompleted).
![Corrección](../assets/fix.svg): se corrigió un problema en el cual los cambios de configuración de moneda no se reflejaban en los eventos después de actualizar la caché.
![Corregir](../assets/fix.svg): error corregido cuando el mensaje de confirmación de pedido no aparece si la colocación asincrónica de pedidos está habilitada.
![Nuevo](../assets/new.svg) - Se agregaron datos al evento `addToRequisitionList` para productos simples en la página de vista de categoría.
![Corregir](../assets/fix.svg) - Se corrigió un problema en los datos de `selectedOptions` en el evento `addToRequisitionList` cuando los productos se agregan desde la página de confirmación de pedido.
![Nuevo](../assets/new.svg): se agregaron datos de producto al evento `addToRequisitionList` cuando los productos se agregan a la lista de solicitudes desde la página de vista de categoría.
![Nuevo](../assets/new.svg) - Se agregó el evento `addToRequisitionList` cuando los productos configurables se agregan a la lista de solicitudes desde la página de vista de productos.
![Nuevo](../assets/new.svg) - Se agregaron `addToRequisitionList` y `removeFromRequisitionList` eventos cuando la cantidad de productos aumenta o disminuye desde una lista de solicitudes.

_10 de junio de 2023_

![Corrección](../assets/fix.svg): se corrigió un problema que se producía cuando `orderId` no pasaba en el contexto debido a los prefijos del identificador de pedido de Commerce.
![Corrección](../assets/fix.svg) - Configuraciones actualizadas de la directiva de seguridad de contenido.

_30 de marzo de 2023_

![Nuevo](../assets/new.svg) - Se ha agregado una extensión denominada `data-services-b2b` que incluye [eventos de lista de solicitudes](events.md#b2b-events) para comerciantes B2B.
![Nuevo](../assets/new.svg) - Se agregó el campo `uniqueIdentifier` a los eventos [search](events.md#search-events). Este nuevo campo permite a los comerciantes hacer referencias cruzadas entre solicitudes de búsqueda y respuestas de búsqueda.

_12 de octubre de 2022_

![Nuevo](../assets/new.svg) - Se agregaron dos [eventos de tienda](events.md), `openCart` y `removeFromCart`, al SDK y al Recopilador de eventos de tienda de Adobe Commerce.
![Nuevo](../assets/new.svg): Se agregó compatibilidad con una [tienda AEM](overview.md#aem-support).

+++

## 3.3.0

_21 de marzo de 2025_

[!BADGE Compatibilidad]{type=Informative tooltip="Compatibilidad"} con versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) agregó compatibilidad con PHP 8.4.

## 3.2.1.

_17 de enero de 2025_

[!BADGE Compatibilidad]{type=Informative tooltip="Compatibilidad"} con versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) - Se agregó la [extensión compatible con HIPAA](hipaa-readiness.md) a [!DNL Data Connection] para que los comerciantes puedan compartir [!DNL Commerce] datos de evento de back office con Experience Platform y mantener el cumplimiento de HIPAA.
![Corrección](../assets/fix.svg) - Se corrigió un problema en el cual la extensión [!DNL Data Connection] sobrescribía datos de `eventForwarding` y establecía la marca `HIPAA` para todos los clientes. Ahora, la extensión solo establece el indicador para los clientes de HIPAA.

## 3.2.0

_7 de octubre de 2024_

[!BADGE Compatibilidad]{type=Informative tooltip="Compatibilidad"} con versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) - Se ha agregado la capacidad de crear [atributos de pedidos personalizados](custom-attributes.md) para los datos de la oficina trasera.
![Nuevo](../assets/new.svg) - Se ha agregado la nueva tabla [Atributos de pedidos personalizados](connect-data.md#data-customization) para ayudarle a ver los atributos personalizados configurados en [!DNL Commerce] y enviados a Experience Platform.
![Nuevo](../assets/new.svg) - Se ha agregado la capacidad para [recopilar y enviar registros de perfil](connect-data.md#send-customer-profile-data) y datos a Experience Platform.

## 3.2.0-beta3

_27 de agosto de 2024_

[!BADGE Compatibilidad]{type=Informative tooltip="Compatibilidad"} con versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) - Si participa en la versión beta, asegúrese de que el archivo `composer.json` tenga lo siguiente en el nivel raíz: ` "minimum-stability": "beta"`. Además, agregue `composer require "magento/customers-connector: ^1.2.0"` para enviar perfiles de clientes desde su instancia de Commerce a SaaS.
![Nuevo](../assets/new.svg): Esta versión contiene las revisiones publicadas en 3.1.1, 3.1.2, 3.1.3 y 3.1.4.

## 3.1.4.

_9 de agosto de 2024_

[!BADGE Compatibilidad]{type=Informative tooltip="Compatibilidad"} con versiones de Adobe Commerce 2.4.4 y posteriores

![Corrección](../assets/fix.svg): se ha actualizado el metapackage `experience-platform-connector` para quitar los exportadores e indexadores de datos adicionales que no se usan.

## 3.1.3.

_22 de julio de 2024_

[!BADGE Compatibilidad]{type=Informative tooltip="Compatibilidad"} con versiones de Adobe Commerce 2.4.4 y posteriores

![Corrección](../assets/fix.svg): se ha actualizado el metapackage `experience-platform-connector` para quitar los exportadores e indexadores de datos que no se usan.

## 3.1.2

_5 de junio de 2024_

[!BADGE Compatibilidad]{type=Informative tooltip="Compatibilidad"} con versiones de Adobe Commerce 2.4.4 y posteriores

![Corrección](../assets/fix.svg) - Se corrigió un problema en el cual se estaba usando un formato de fecha incorrecto al iniciar una [sincronización histórica](connect-data.md#specify-order-history-date-range).
![Corrección](../assets/fix.svg): se ha corregido un problema por el que el evento `startCheckout` no se enviaba en Adobe Commerce 2.4.7.

## 3.1.1.

_4 de abril de 2024_

[!BADGE Compatibilidad]{type=Informative tooltip="Compatibilidad"} con versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) - Se agregó compatibilidad con PHP 8.3 para todas las extensiones de [!DNL Data Connection].
![Nuevo](../assets/new.svg) - Se agregó un artículo sobre cómo [integrar](mobile-sdk-epc.md) Adobe Experience Platform Mobile SDK con Commerce.

## 3.2.0-beta2

_4 de marzo de 2024_

[!BADGE Compatibilidad]{type=Informative tooltip="Compatibilidad"} con versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) - Si participa en la versión beta, asegúrese de que el archivo `composer.json` tenga lo siguiente en el nivel raíz: ` "minimum-stability": "beta"`. Además, agregue `composer require "magento/customers-connector: ^1.2.0"` para enviar perfiles de clientes desde su instancia de Commerce a SaaS.
![Nuevo](../assets/new.svg) - Se agregó la capacidad para [agregar atributos personalizados](custom-attributes.md).
![Nuevo](../assets/new.svg) - Se ha agregado la capacidad para [recopilar y enviar registros de perfil](connect-data.md#send-customer-profile-data) y datos a Experience Platform.

## 3.1.0

_16 de noviembre de 2023_

[!BADGE Compatibilidad]{type=Informative tooltip="Compatibilidad"} con versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) - Se cambió el nombre del conector Experience Platform a [!DNL Data Connection].
![Corrección](../assets/fix.svg): Se ha agregado la capacidad de registrar la respuesta de error si Adobe IMS no puede generar el token de acceso.
![Corrección](../assets/fix.svg) - Se agregó un mensaje de notificación si intenta sincronizar pedidos históricos pero no ha especificado credenciales de cuenta.

## 3.0.0

_10 de octubre de 2023_

[!BADGE Compatibilidad]{type=Informative tooltip="Compatibilidad"} con versiones de Adobe Commerce 2.4.4 y posteriores

Esta es una versión principal. [Editar](install.md#update-the-data-connection) el archivo root composer.json de su proyecto.

![Nuevo](../assets/new.svg): disponibilidad general para [enviar datos y estado de pedidos históricos](connect-data.md#send-historical-order-data) a Experience Platform.
![Nuevo](../assets/new.svg): Se agregó compatibilidad con OAuth 2.0 al [configurar](connect-data.md#connect-commerce-data-to-adobe-experience-platform) la extensión [!DNL Data Connection].
![Nuevo](../assets/new.svg): fin de la compatibilidad con Adobe Commerce 2.4.3.

## 2.3.0

_27 de junio de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.3 y posteriores

![Nuevo](../assets/new.svg) - Se ha agregado la capacidad para [desactivar el envío de eventos de tienda](connect-data.md#data-collection) a Experience Platform.
![Corrección](../assets/fix.svg) - Configuraciones actualizadas de la directiva de seguridad de contenido.
![Corrección](../assets/fix.svg): Se ha corregido la compatibilidad con eventos de back office en la versión 2.4.7 de Commerce.
![Nuevo](../assets/new.svg) - Se agregó un mensaje de notificación sobre la invalidación de la caché al guardar los cambios en el formulario de extensión [!DNL Data Connection].

## 3.0.0-beta1 (solo interno)

_13 de junio de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.3 y posteriores

![Nuevo](../assets/new.svg) - (Beta) Se ha agregado la capacidad para [enviar datos y estado de pedidos históricos](connect-data.md#beta-send-historical-order-data) a Experience Platform.

## 2.2.0

_30 de marzo de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.3 y posteriores

![Nuevo](../assets/new.svg) - Agrupó las dependencias `commerce-data-export` y `saas-export` con la extensión `experience-platform-connector`. Anteriormente, tenía que instalar estas dependencias por separado. Estas dependencias, junto con la configuración del comerciante, permiten el procesamiento en el servidor de [eventos de back office](events-backoffice.md).
![Nuevo](../assets/new.svg) - Se agregó un nuevo evento de back office denominado [`orderShipmentCompleted`](events-backoffice.md#ordershipmentcompleted).

## 2.1.1

_28 de febrero de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.3 y posteriores

![Nuevo](../assets/new.svg) - Se agregó compatibilidad con PHP 8.2 para todas las extensiones de [!DNL Data Connection].

## 2.1.0

_17 de enero de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.3 y posteriores

![Nuevo](../assets/new.svg) - Se ha actualizado [[!DNL Data Connection] el administrador de la extensión](connect-data.md) para que pueda especificar su propio AEP Web SDK (alloy).
![Corrección](../assets/fix.svg) se cambió al uso de `identityMap` en lugar de `personID` al establecer la identidad principal para cualquier dato insertado en el perímetro de.

## 2.0.1

_10 de noviembre de 2022_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.3 y posteriores

![Corrección](../assets/fix.svg): Ahora el contexto de Adobe Experience Platform solo se establece después de que el Recopilador de eventos de tienda y el SDK de eventos de tienda se carguen correctamente.

## 2.0.0

_12 de octubre de 2022_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.3 y posteriores

![Nuevo](../assets/new.svg): Se ha agregado la capacidad de especificar su propio AEP Web SDK al [conectar](connect-data.md) su instancia de Adobe Commerce a Experience Platform.
![Corrección](../assets/fix.svg): Se ha actualizado el requisito de ámbito de secuencia de datos para que los identificadores de secuencia de datos deban crearse en el sitio web en lugar de en la vista de tienda.

## 1.0.0

_9 de agosto de 2022_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.3 y posteriores

![Nuevo](../assets/new.svg): versión de disponibilidad general.
