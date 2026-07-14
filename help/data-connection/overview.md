---
title: Introducción a [!DNL Data Connection]
description: Obtenga información sobre cómo integrar datos de Adobe Commerce con Adobe Experience Platform mediante la extensión  [!DNL Data Connection] .
recommendations: noCatalog
exl-id: 660f9337-cad8-47fb-a959-0770f0fd813c
TQID: https://experienceleague.adobe.com/-wfkGM2isTVmAaJokndxVy0-UtZ4pM9msYXmh2IE-Hc
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 5ba5dfa23580b5eefa8271277e78c6ea67879b90
workflow-type: tm+mt
source-wordcount: 1373
ht-degree: 1%

---

# Introducción a [!DNL Data Connection]

>[!IMPORTANT]
>
>Se cambió el nombre del conector Experience Platform a [!DNL Data Connection].

La extensión [!DNL Data Connection] conecta la instancia web de Adobe Commerce con Adobe Experience Platform y Edge Network. Para los desarrolladores de aplicaciones móviles, puede utilizar Adobe Experience Platform Mobile SDK con Commerce para capturar y enviar datos de Commerce a Experience Platform. [Más información](./mobile-sdk-epc.md).

Los comerciantes de varios sitios web pueden establecer la configuración de [!DNL Data Connection] aplicable por sitio web, incluida la selección de la zona protegida de Experience Platform. Consulte [Conectar datos de Commerce a Adobe Experience Platform](connect-data.md#configuration-scope) para campos globales frente a campos con ámbito de sitio web.

Su tienda Commerce contiene una gran cantidad de datos. La información sobre cómo los compradores exploran, ven y finalmente compran los productos en el sitio puede revelar oportunidades para crear una experiencia de compra más personalizada. Aunque esos datos pueden informar a funciones nativas de Commerce, como reglas de precios del carro de compras y bloques dinámicos, los datos permanecen en silo en la instancia de Commerce.

Adobe Experience Platform proporciona un conjunto de tecnologías que, cuando se hidratan con datos de su tienda Commerce, pueden distribuir esos datos a través de Edge Network a otros productos Adobe DX para desbloquear perspectivas sobre el comportamiento de compra de su comprador. Con estas perspectivas profundas, puede crear una experiencia de compra más personalizada en todos los canales.

La siguiente imagen muestra cómo fluyen los datos de Commerce desde su tienda a otros productos DX de Adobe cuando se instala y configura la extensión [!DNL Data Connection].

![Flujo de datos al perímetro de Experience Platform](assets/commerce-edge.png)

En la imagen anterior, los datos de perfil del comportamiento, el back office y el cliente se envían al perímetro de Experience Platform mediante un SDK, una API y un conector de origen. No es necesario que comprenda completamente cómo funcionan estos fragmentos, ya que la extensión gestiona la complejidad del uso compartido de datos por usted. Cuando los datos de evento se encuentren en el límite, podrá usarlos en productos Adobe DX de flujo descendente, como [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=es), [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html), [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/admin-overview/analytics-overview.html) y [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html). Para ver ejemplos guiados, consulte [Usar Adobe Journey Optimizer para enviar un correo electrónico de carro de compras abandonado](using-ajo.md) y [Crear una audiencia en Real-Time CDP con datos de evento de Commerce](create-audience.md).

## Extracción de datos de Experience Platform de nuevo en Commerce

El envío de los datos de Commerce a Experience Platform mediante la extensión [!DNL Data Connection] es una de las características de Commerce para compartir datos. El otro lado, que es una extensión opcional, se llama [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html). Esta extensión le permite crear audiencias en Real-Time CDP e implementarlas en su tienda de Commerce para informar las reglas de precios del carro de compras, las reglas de productos relacionadas y los bloques dinámicos.

En un nivel superior, el flujo de datos desde la tienda de Commerce a Experience Platform y a través de la extensión de Audience Activation tiene el siguiente aspecto:

![[!DNL Data Connection] flujo](assets/data-connection.png)

Después de configurar la conexión entre Commerce a Experience Platform y Experience Platform a Commerce, los datos siguen fluyendo. No es necesario que vuelva a conectarse, a menos que así lo requiera una actualización.

## Conceptos

Para compartir datos entre estos dos sistemas, es necesario comprender varios conceptos.

- **Tipos de datos** — [!DNL Data Connection] recopila datos de **comportamiento (tienda)** del explorador, datos de **back office** de servidores de Commerce y datos de **perfil**. El administrador etiqueta la colección de tiendas **Eventos de tiendas**. Consulte [Tipos de datos de Commerce](data-ingestion.md) para obtener la taxonomía completa.

- **Datos de comportamiento (tienda)**: capturados a partir de interacciones de compradores en el sitio, como `addToCart`, `pageView`, `startCheckout` y `completeCheckout`. Ver [eventos de tienda](events.md#storefront-events).

- **Datos de la oficina central**: capturados en servidores de Commerce, incluidos eventos de [estado de pedidos](events-backoffice.md#order-status) como [`orderPlaced`](events-backoffice.md#orderplaced) y [`orderShipped`](events-backoffice.md#ordershipmentcompleted). Ver [eventos de back office](events-backoffice.md).

- **Registros de perfil**: datos de instantánea enviados cuando se crea un perfil de comprador en Commerce. Ver [registros de perfil](events-profilerecord.md) y [Actualizar esquema de registro de perfil](profile-data.md).

- **Eventos de perfil**: eventos de serie temporal para cambios de ciclo de vida de perfil en el servidor. Ver [eventos de perfil de cliente](events-backoffice.md#customer-profile-events).

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

## Habilitar la extensión {#enable-extension}

En un nivel superior, habilitar la extensión [!DNL Data Connection] implica los siguientes pasos:

1. [Instalar](install.md) la extensión [!DNL Data Connection].
1. [Inicia sesión](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html) en tu cuenta de Adobe y [consulta para confirmar](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255) tu ID de organización. El identificador de organización es el ID asociado con la empresa que ha seleccionado en Experience Cloud. Se trata de una cadena alfanumérica de 24 caracteres seguida de `@AdobeOrg` (que debe incluirse).
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
- [Entradas de soporte técnico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket){target="_blank"} — Envíe un ticket para recibir ayuda adicional.
