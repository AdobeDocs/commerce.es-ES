---
title: Introducción a [!DNL Data Connection]
description: Obtenga información sobre cómo integrar datos de Adobe Commerce con Adobe Experience Platform mediante la extensión  [!DNL Data Connection] .
recommendations: noCatalog
exl-id: 660f9337-cad8-47fb-a959-0770f0fd813c
source-git-commit: 60a8e8f5cedff0c6fa56c563807b9604e3ae1d21
workflow-type: tm+mt
source-wordcount: '1761'
ht-degree: 0%

---

# Introducción a [!DNL Data Connection]

>[!IMPORTANT]
>
>Se cambió el nombre del conector Experience Platform a [!DNL Data Connection].

La extensión [!DNL Data Connection] conecta la instancia web de Adobe Commerce con Adobe Experience Platform y Edge Network. Para los desarrolladores de aplicaciones móviles, puede utilizar Adobe Experience Platform Mobile SDK con Commerce para capturar y enviar datos de Commerce a Experience Platform. [Más información](./mobile-sdk-epc.md).

Su tienda Commerce contiene una gran cantidad de datos. La información sobre cómo los compradores exploran, ven y finalmente compran los productos en el sitio puede revelar oportunidades para crear una experiencia de compra más personalizada. Aunque esos datos pueden informar a funciones nativas de Commerce, como reglas de precios del carro de compras y bloques dinámicos, los datos permanecen en silo en la instancia de Commerce.

Adobe Experience Platform proporciona un conjunto de tecnologías que, cuando se hidratan con datos de su tienda Commerce, pueden distribuir esos datos a través de Edge Network a otros productos Adobe DX para desbloquear perspectivas sobre el comportamiento de compra de su comprador. Con estas perspectivas profundas, puede crear una experiencia de compra más personalizada en todos los canales.

La siguiente imagen muestra cómo fluyen los datos de Commerce desde su tienda a otros productos DX de Adobe cuando se instala y configura la extensión [!DNL Data Connection].

![Flujo de datos al perímetro de Experience Platform](assets/commerce-edge.png)

En la imagen anterior, los datos de perfil del comportamiento, el back office y el cliente se envían al perímetro de Experience Platform mediante un SDK, una API y un conector de origen. No es necesario que comprenda completamente cómo funcionan estos fragmentos, ya que la extensión gestiona la complejidad del uso compartido de datos por usted. Cuando los datos de evento se encuentran en el límite, puede extraer esos datos en otras aplicaciones de Experience Platform. Por ejemplo:

| Aplicación | Finalidad | Casos de uso |
|---|---|---|
| [Adobe [!DNL Real-Time CDP]](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=es) | Administración de perfiles y servicio de segmentación | **Segmentación del historial de compras**: los comerciantes pueden identificar a los clientes que compran un artículo en función de un período de tiempo específico (mensual, trimestral, anual, etc.). Los comerciantes pueden crear segmentos para estos clientes y segmentarlos para promociones, campañas y como _parte superior de los datos de funnel_ para posibles clientes de los servicios de suscripción.<br> **Segmentación basada en categorías**: los comerciantes pueden ver qué categoría de productos se compró.<br> **Segmentación basada en ofertas**: los comerciantes pueden identificar a los clientes que devuelven productos de forma consistente. Las ofertas y descuentos que se les ofrecen ahora pueden ser más inteligentes. Por ejemplo, se puede eliminar el envío gratuito para un cliente que devuelve productos todo el tiempo.<br> **Segmentación por similitud**: una _audiencia por similitud_ es una metodología que usa un comerciante para que sus promociones lleguen a nuevas personas que probablemente estén interesadas en su negocio porque comparten características similares con sus clientes actuales. Los segmentos de similitud se pueden crear en función de los datos transaccionales y de comportamiento.<br> **Tendencia del cliente**: los cambios en el comportamiento del cliente se pueden identificar como resultado de perfiles de cliente más profundos que se pueden crear a partir de los datos transaccionales. Habrá una mayor confianza en la puntuación de tendencia, ya que hay más datos fluyendo hacia los cálculos, como devoluciones de productos y configuraciones de productos.<br> **Venta cruzada**: un comerciante puede identificar oportunidades de venta cruzada y de mejora de ventas a partir de la información granular recopilada en Commerce. |
| [Cliente [!DNL Journey Analytics]](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html) | Análisis profundo del recorrido completo de Commerce | **Tendencias estacionales**: un comerciante puede identificar las tendencias estacionales, lo que le ayuda a prepararse para el cambio periódico en la demanda de determinados productos. Además, los comerciantes pueden identificar cambios en la popularidad general de cualquier producto a lo largo de los años.<br> **Análisis de conversión**: al saber cuándo se compró un producto, junto con el acceso a los eventos de impresión de la tienda, los comerciantes pueden generar un perfil enriquecido del cliente para realizar el análisis de conversión. |
| [Adobe [!DNL Analytics]](https://experienceleague.adobe.com/docs/analytics/analyze/admin-overview/analytics-overview.html) | Análisis profundo del comportamiento del cliente y el rendimiento de la campaña | **Devoluciones de pedidos**: los comerciantes pueden identificar a los clientes y a los segmentos de clientes más grandes que tienen un patrón de devolución de productos. Esto ayuda a los comerciantes a mejorar su estrategia comercial a medida que comprenden el aspecto de su comportamiento de base de clientes.<br> **Dirección del pedido**: en función de la dirección de envío, un comerciante puede saber si los pedidos los realizan los propios clientes o si se trata de otra persona o entidad.<br> **Tendencias de estacionalidad**: un comerciante puede identificar tendencias estacionales, lo que le ayuda a prepararse para el cambio periódico en la demanda de productos específicos. Además, los comerciantes pueden identificar cambios en la popularidad general de cualquier producto a lo largo de los años.<br> **Análisis de conversión**: al saber cuándo se compró un producto, junto con el acceso a los eventos de impresión de la tienda, los comerciantes pueden generar un perfil enriquecido del cliente para realizar el análisis de conversión. **Nota**: Adobe Analytics solo admite datos de eventos de comportamiento (tienda). Adobe Analytics no admite datos de evento transaccionales (de back-office). |
| [Adobe [!DNL Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html) | Organización de campañas en varios canales | **recorridos basados en el comportamiento**: Los comerciantes pueden dirigirse a un cliente que compró un teléfono móvil hace dos años sugiriendo que compre el nuevo modelo. Los comerciantes pueden crear campañas y promociones personalizadas para estos clientes y utilizar la funcionalidad de correo electrónico y SMS para ponerse en contacto con. Además, los comerciantes pueden utilizar datos de comportamiento y orden históricos para identificar tendencias. Por ejemplo, un cliente que compró un artículo con una configuración determinada en el pasado y ahora quiere comprar de nuevo el mismo producto, puede mejorar su recorrido de compra ofreciéndole visibilidad y acceso a las mismas configuraciones de producto.<br> **Personalization**: con acceso a la información del perfil del cliente, [!DNL Journey Optimizer] puede desbloquear recorridos altamente personalizados, lo que permite que los comerciantes se comuniquen con los clientes en diferentes canales.<br> **Nuevo perfil creado**: los correos electrónicos de bienvenida y las actividades promocionales pueden alentar e influir en los nuevos clientes en sus recorridos de compra.<br> **Perfil eliminado**: los comerciantes pueden optar por dejar de enviar correos electrónicos promocionales a los clientes que hayan cerrado su cuenta. Como alternativa, los comerciantes también pueden crear campañas para recuperar clientes perdidos. |

## Extracción de datos de Experience Platform de nuevo en Commerce

El envío de los datos de Commerce a Experience Platform mediante la extensión [!DNL Data Connection] es una de las características de Commerce para compartir datos. El otro lado, que es una extensión opcional, se llama [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html). Esta extensión le permite crear audiencias en Real-Time CDP e implementarlas en su tienda de Commerce para informar las reglas de precios del carro de compras, las reglas de productos relacionadas y los bloques dinámicos.

En un nivel superior, el flujo de datos desde la tienda de Commerce a Experience Platform y a través de la extensión de Audience Activation tiene el siguiente aspecto:

![[!DNL Data Connection] flujo](assets/data-connection.png)

Después de configurar la conexión entre Commerce a Experience Platform y Experience Platform a Commerce, los datos siguen fluyendo. No es necesario que vuelva a conectarse, a menos que así lo requiera una actualización.

## Conceptos

Para compartir datos entre estos dos sistemas, es necesario comprender varios conceptos.

- **Datos**: los datos que se comparten con Experience Platform son los datos recopilados de los eventos del explorador en la tienda, los eventos del back office en el servidor y los datos del registro de perfil. Los eventos de tienda se capturan a partir de las interacciones de los compradores en el sitio e incluyen eventos como `addToCart`, `pageView`, `createAccount`, `editAccount`, `startCheckout`, `completeCheckout`, `signIn`, `signOut`, etc. Consulta [eventos de tienda](events.md#storefront-events) para ver la lista completa de eventos de tienda. Los eventos del lado del servidor o de back office incluyen información sobre el estado de los pedidos [1&rbrace;, como &#x200B;](events-backoffice.md#order-status), [`orderPlaced`](events-backoffice.md#orderplaced), [`orderReturned`](events-backoffice.md#orderitemreturncompleted), [`orderShipped`](events-backoffice.md#ordershipmentcompleted), etc. [`orderCancelled`](events-backoffice.md#ordercancelled) Consulte [eventos de back office](events-backoffice.md) para obtener la lista completa de eventos de back office. Los datos de registro de perfil contienen información cuando se crea, actualiza o elimina un perfil nuevo. Consulte [datos de registro de perfil](events-profilerecord.md) para obtener más información.

- **Experience Platform y Edge Network**: el almacén de datos para la mayoría de los productos Adobe DX. Los datos enviados a Experience Platform se propagan a los productos Adobe DX a través de Experience Platform Edge Network. Por ejemplo, puede iniciar Journey Optimizer, recuperar los datos de evento específicos de Commerce desde Edge y crear un correo electrónico de carro de compras abandonado en Journey Optimizer. A continuación, Journey Optimizer puede enviar ese correo electrónico si hay carros de compras abandonados en la tienda Commerce. Más información sobre [Experience Platform y Edge Network](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/overview.html).

- **Esquema**: el esquema describe la estructura de los datos que se están enviando. Para que Experience Platform pueda introducir los datos de Commerce, debe crear un esquema para describir la estructura de los datos y proporcionar restricciones para el tipo de datos que se pueden contener en cada campo. Los esquemas constan de una clase base y cero o más grupos de campos de esquema. El esquema utiliza la estructura XDM, que pueden leer todos los productos Adobe DX. El esquema garantiza que los datos enviados a Experience Platform se comprendan en todos los productos DX. Más información sobre [esquemas](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html).

- **Conjunto de datos**: una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla que contiene un esquema (columnas) y campos (filas). Los conjuntos de datos también contienen metadatos que describen varios aspectos de los datos que almacenan. Todos los datos que se incorporan correctamente a Adobe Experience Platform están contenidos en conjuntos de datos. Más información sobre [conjuntos de datos](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html).

- **Flujo de datos** - ID que permite que los datos fluyan de Adobe Experience Platform a otros productos Adobe DX. Este ID debe estar asociado a un sitio web específico dentro de la instancia de Adobe Commerce específica. Cuando cree este flujo de datos, especifique el esquema XDM que ha creado anteriormente. Más información sobre [flujos de datos](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html).

## Arquitectura admitida

La extensión [!DNL Data Connection] está disponible en las siguientes arquitecturas:

- PHP/Luma
- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/integrations/adobe-commerce/aep/)
- [AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/aep.html)

>[!BEGINSHADEBOX]

## Requisitos previos

Para usar la extensión [!DNL Data Connection], debe tener lo siguiente:

- Adobe Commerce 2.4.4 o posterior
- Adobe ID e ID de organización
- [Capa de datos del cliente de Adobe (ACDL)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html), que es necesaria para recopilar datos de evento de tienda
- Derechos a otros productos Adobe DX.

>[!ENDSHADEBOX]

## Pasos de incorporación

En un nivel superior, habilitar la extensión [!DNL Data Connection] implica los siguientes pasos:

1. [Instalar](install.md) la extensión [!DNL Data Connection].
1. [Inicia sesión](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html) en tu cuenta de Adobe y [consulta para confirmar](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255) tu ID de organización. El ID de organización es el ID asociado con la empresa de Experience Cloud aprovisionada. Se trata de una cadena alfanumérica de 24 caracteres seguida de `@AdobeOrg` (que debe incluirse).
1. Asegúrese de que tiene [permiso para recopilar datos en Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).
1. Revise los [tipos de datos](data-ingestion.md) que puede recopilar y enviar.
1. Cree o actualice su [esquema de evento de serie temporal](update-xdm.md) o [esquema de datos de registro de perfil](profile-data.md) con grupos de campos específicos de Commerce.
1. [Crear un conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset) basado en el esquema que creó o actualizó. Este conjunto de datos contiene los datos de Commerce enviados a Experience Platform Edge.
1. [Cree una secuencia de datos](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) y seleccione el esquema XDM que contiene los grupos de campos específicos de Commerce.
1. [Conectarse a los servicios de Commerce](../landing/saas.md).
1. [Conectarse a Adobe Experience Platform](connect-data.md).

El resto de esta guía le explica todos estos pasos con más detalle para que pueda ponerse al día y comenzar a utilizar la potencia de los productos Adobe DX en su tienda Commerce.

>[!NOTE]
>
>Para desarrolladores móviles, aprenda a [integrar](./mobile-sdk-epc.md) Adobe Experience Platform Mobile SDK con Commerce.

## Preparación para HIPAA

La extensión [!DNL Data Connection] le permite compartir datos del back office [!DNL Commerce] con Experience Platform y mantener el cumplimiento de la HIPAA. [Más información](hipaa-readiness.md).

## Público

Esta guía está diseñada para el comerciante de Adobe Commerce que desea enriquecer y personalizar su tienda Commerce para mejorar la experiencia de compra de sus clientes.

## Asistencia

Si necesita información o tiene preguntas que no se tratan en esta guía, utilice los siguientes recursos:

- [Centro de ayuda](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/overview.html){target="_blank"}
- [Entradas de soporte técnico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket){target="_blank"}: envía un ticket para recibir ayuda adicional.
