---
title: Información general de [!DNL Adobe Commerce as a Cloud Service]
description: Obtenga información acerca de las características y ventajas principales de  [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Architect, Developer, User, Leader
exl-id: 1b7e2731-4a10-4c2b-9bfc-8945729ed523
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 31d1f1fe784247d6db8a26f8a9e6ae0291e416b5
workflow-type: tm+mt
source-wordcount: '1406'
ht-degree: 0%

---


# Información general de [!DNL Adobe Commerce as a Cloud Service]

[!DNL Adobe Commerce as a Cloud Service] ofrece flexibilidad, escalabilidad y eficiencia al permitir que las empresas ofrezcan y escalen rápidamente operaciones digitales y aceleren la innovación. La infraestructura nativa en la nube de Adobe ajusta automáticamente los recursos para satisfacer las demandas máximas de tráfico, pedidos y administración de catálogos.

En la tabla siguiente se destacan los productos que alimentan [!DNL Adobe Commerce as a Cloud Service]:

<table style="table-layout:auto">
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="marca de verificación" align="center"> <strong>Tienda Commerce</strong>
    </td>
    <td align="left">
      Interfaz orientada al cliente donde los compradores examinan y compran productos
    </td>
  </tr>
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="marca de verificación" align="center"> <strong>Servicios de comercialización</strong>
    </td>
    <td align="left">
      Servicios back-end que administran catálogos de productos, precios e inventario
    </td>
  </tr>
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="marca de verificación" align="center"> <strong>Imágenes del producto</strong>
    </td>
    <td align="left">
      Administración de activos digitales para imágenes y medios de productos
    </td>
  </tr>
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="marca de verificación" align="center"> <strong>Plataforma de desarrollador</strong>
    </td>
    <td align="left">
      Herramientas principales de desarrollo y API para crear funcionalidades personalizadas
    </td>
  </tr>
</table>

## Arquitectura

Vea el siguiente vídeo para obtener una breve introducción a la arquitectura de [!DNL Adobe Commerce as a Cloud Service]. A continuación, se proporcionan diagramas que ilustran la arquitectura del vídeo.

>[!VIDEO](https://video.tv.adobe.com/v/3443270?learn=on&captions=spa)

Este diagrama ilustra el flujo de datos entre [!DNL Adobe Commerce as a Cloud Service] y todas las soluciones de Adobe Experience Cloud.

![[!DNL Adobe Commerce as a Cloud Service] diagrama de arquitectura](./assets/data-flow.svg){zoomable="yes"}

## Commerce Storefront

Usa [Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront?lang=es) de Adobe con tecnología de Edge Delivery Services para crear experiencias enriquecidas en minutos con una sencilla creación basada en documentos o edición visual con Storefront Builder.

Commerce Storefront carece totalmente de encabezado con una arquitectura disociada que proporciona todos los servicios de comercialización y datos a través de una capa de API de GraphQL. Esta arquitectura permite a los equipos desarrollar sus front-end de forma independiente de Commerce Foundation, lo que proporciona la agilidad para crear y probar nuevos puntos de contacto con tecnologías emergentes.

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service] no admite tiendas Luma. Si está migrando desde Adobe Commerce en la nube o local, consulte [escaparates existentes](https://experienceleague.adobe.com/developer/commerce/storefront/discovery/?lang=es#existing-storefronts) para obtener instrucciones sobre la transición.

## Servicios de comercialización y servicios de pago

Adobe proporciona un completo conjunto de servicios de comercialización inteligentes y componibles para ayudarle a lograr sus objetivos comerciales clave. Estos servicios también proporcionan API esenciales para optimizar el rendimiento a escala.

- [Live Search](../live-search/overview.md): ofrece resultados más inteligentes, rápidos y relevantes a los compradores con esta herramienta de búsqueda con tecnología de IA.
- [Recomendaciones de productos](../product-recommendations/overview.md): agregue recomendaciones impulsadas por IA en función del comportamiento del comprador, las tendencias populares, la similitud del producto y mucho más.
- [Servicios de comercialización con tecnología de vistas y directivas de catálogo](../optimizer/setup/catalog-view.md): administre catálogos de productos grandes y complejos con modelado de datos flexible para ofrecer catálogos de comercio flexibles y de alto rendimiento alineados con la estructura empresarial y las estrategias de comercialización. Úselo con [Commerce Optimizer](../optimizer/overview.md) para optimizar el rendimiento del catálogo y mejorar las tasas de conversión.
- [Servicios de pago](../payment-services/guide-overview.md): Mejore la satisfacción del cliente ofreciendo varios métodos de pago, incluidos pagos a plazos sin intereses, y una sola vista del procesamiento de pagos, pedidos y facturas.

## Imágenes de productos con tecnología de AEM Assets

La visualización de productos ayuda a simplificar la administración de recursos mediante un sistema de administración de recursos digitales (DAM) que se integra con Adobe Experience Manager para administrar contenido con medios enriquecidos.

La integración garantiza que los recursos digitales, como las imágenes de los productos o el contenido de marketing, se vinculen dinámicamente a las entidades de comercialización adecuadas, incluidos los productos y las categorías de Adobe Commerce, en función del SKU u otros atributos clave.

Los elementos visuales del producto están disponibles de forma predeterminada con [!DNL Adobe Commerce as a Cloud Service], lo que proporciona algunas de las capacidades de los AEM Assets.

Como alternativa, las capacidades nativas de [!DNL Adobe Commerce as a Cloud Service] proporcionan herramientas básicas de administración de recursos para almacenar y administrar recursos digitales.

### Visuales o AEM Assets del producto

La siguiente comparación le ayuda a seleccionar la mejor opción para sus necesidades de cadena de suministro de contenido:

<table>
  <tr>
    <td align="left">
      <strong>Imágenes de productos con tecnología de AEM Assets</strong>
      <ul>
        <li>Imagen de producto y vídeo integrados y automatizados Digital Asset Manager (DAM)</li>
        <li>Cambiar el tamaño, recortar y convertir imágenes</li>
        <li>Entrega de vídeo e imagen de alta velocidad</li>
        <li>Optimizar los formatos, tamaños y calidad de la imagen en función de las funciones del explorador del cliente</li>
        <li>Acceso a Adobe Express y Adobe Firefly</li>
        <li>Límites de uso para la capacidad de entrega de imágenes/vídeo y el acceso del usuario</li>
        <li>Selector de recursos integrado</li>
      </ul>
    </td>
    <td align="center">
      <br><br><br><br><br><br><br><br><br><br><br>
      <img src="../assets/icon-double-chevron-right.svg" alt="cheurón" width="100">
    </td>
    <td align="left">
      <strong>AEM Assets</strong>
      <ul>
        <li>Todas las funciones de las imágenes del producto</li>
        <li>Digital Asset Manager de marketing completo (DAM)</li>
        <li>Usuarios ilimitados (pago por usuario)</li>
        <li>Entrega de imágenes y vídeos ilimitada</li>
        <li>Funcionalidad avanzada de administración de recursos:</li>
        <ul>
          <li>Conjuntos de giros de 360° y visores interactivos</li>
          <li>Compatibilidad con modelos 3D y contenido envolvente</li>
          <li>Compatibilidad con PDF</li>
          <li>Recorte inteligente con tecnología de IA</li>
          <li>Plantillas de imagen dinámicas</li>
          <li>Etiquetado inteligente</li>
          <li>Seguimiento y análisis del rendimiento de los recursos</li>
        </ul>
      </ul>
    </td>
  </tr>
    <tr>
    <td align="center" colspan="3">
      La integración de <strong>marca Adobe está disponible para facilitar la migración entre ofertas.</strong>
    </td>
  </tr>
</table>

Consulte la guía de integración de [AEM Assets](../aem-assets-integration/overview.md) para obtener más información sobre cómo integrar elementos visuales de productos con tecnología de AEM Assets con [!DNL Adobe Commerce as a Cloud Service].

## Plataforma de desarrollador

Adobe proporciona a los desarrolladores puntos de extensión y herramientas completos para crear aplicaciones que amplíen las capacidades de Commerce Foundation y se integren con sistemas de terceros (como CRM, ERPS y PIMS). Estas herramientas reducen el coste total de propiedad de la plataforma de las siguientes maneras:

- **Escalabilidad**: las aplicaciones se pueden escalar por separado del software principal, lo que permite una mayor eficiencia y actualizaciones simplificadas.
- **Aislamiento**: un entorno aislado significa que los desarrolladores pueden actualizar o modificar sus extensiones a su discreción sin depender de una versión principal.
- **Independencia tecnológica**: los desarrolladores pueden elegir entre pilas de tecnología y lenguajes de codificación que se ajusten a sus necesidades.

>[!TIP]
>
>Las aplicaciones creadas por el proveedor también se pueden instalar en [Adobe Exchange](https://exchange.adobe.com/).

Adobe proporciona las siguientes herramientas para desarrolladores para crear integraciones y personalizaciones:

- [**Mesh de API para Adobe Developer App Builder**](https://developer.adobe.com/graphql-mesh-gateway/): coordina y combina varias fuentes de API, GraphQL, REST y otras en un único extremo de GraphQL consultable.
- [**App Builder**](https://developer.adobe.com/app-builder/docs/overview/): cree e implemente aplicaciones web seguras y escalables que amplíen la funcionalidad de Commerce y se integren con soluciones de terceros.
- [**Eventos**](https://developer.adobe.com/commerce/extensibility/events/): utilice déclencheur de eventos personalizados para interactuar con otras herramientas de desarrollo ampliables.
- [**Webhooks**](https://developer.adobe.com/commerce/extensibility/webhooks/): utilice los webhooks para almacenar en déclencheur automáticamente las interacciones entre Commerce y sistemas de terceros.
- [**IU de administración SDK**](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/): personalice y mejore la administración de Commerce con nuevas páginas y características para sus comerciantes.
- [**Kit de inicio de integración**](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/): acelere las integraciones de back-office con integraciones de referencia, scripts de incorporación y una arquitectura estandarizada.

## Commerce Foundation

Commerce Foundation proporciona una plataforma de alojamiento automatizada segura y funciones de autoservicio para administrar su aplicación de Commerce en un entorno nativo de la nube.

Las funciones principales incluyen:

- Incorporación simplificada
- Actualizaciones sin problemas
- Integraciones de terceros

### Incorporación simplificada

Inicie las instancias de zona protegida y producción en minutos con el portal de aprovisionamiento de autoservicio [!UICONTROL Commerce Cloud Manager]. Todo lo que necesita, incluidos los servicios de comercialización, una instancia de Commerce sin encabezado y App Builder, se configura e integra automáticamente en sus instancias.

Consulte [Introducción](getting-started.md) para aprender a crear y administrar instancias de Commerce.

### Actualizaciones sin problemas

Acceda a las últimas funciones y mejoras sin necesidad de realizar actualizaciones manuales. El envío continuo de nuevas funciones y actualizaciones elimina la necesidad de aplicar parches manualmente, lo que garantiza que siempre tenga acceso a las funciones más recientes con un bajo coste total de propiedad.

El proceso de actualización típico de Adobe Commerce en la nube implicaba la creación de copias de seguridad, la clonación de instancias, la ejecución de herramientas de compatibilidad y la corrección de conflictos de código. Ya no es necesario con [!DNL Adobe Commerce as a Cloud Service]. Adobe le envía notificaciones en la aplicación cuando se publican nuevas funciones y actualizaciones de seguridad. Tiene un periodo de 30 días para evaluar las nuevas funciones en las instancias de la zona protegida antes de que las actualizaciones se apliquen automáticamente a los entornos de producción.

>[!NOTE]
>
>Adobe garantiza la compatibilidad con versiones anteriores de todas las actualizaciones. Esto significa que, cuando se aplican actualizaciones, no se rompen la funcionalidad o las personalizaciones existentes que se adhieren al modelo de extensibilidad [API-First](https://developer.adobe.com/commerce/extensibility/).

### Integraciones de terceros

Los desarrolladores pueden usar las API [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/) y [REST](https://developer.adobe.com/commerce/webapi/rest/) completas para integrar Commerce Foundation con sistemas de terceros y ampliar las capacidades de Commerce.

<!-- ## Experience Cloud integration

[!DNL Adobe Commerce as a Cloud Service] integrates with all Experience Cloud solutions to deliver [personalized commerce experiences at scale](https://experienceleague.adobe.com/es/docs/commerce-admin/customers/customers-menu/personalize-scale#customers-menu).

[Data Connection](../data-connection/overview.md) unlocks insights about your shoppers' buying behavior so that you can create personalized shopping experiences across all channels with other Adobe Digital Experience products. -->

## Ventajas

Las secciones siguientes proporcionan información sobre los beneficios que [!DNL Adobe Commerce as a Cloud Service] proporciona a los líderes empresariales y de TI.

### Líderes empresariales

- **Aumentar los ingresos**: Impulse el tráfico orgánico con una tienda de alto rendimiento que impulse el SEO. Cree experiencias personalizadas que impulsen la conversión mediante datos enriquecidos.
- **Escalar operaciones**: Los servicios de escalado automático satisfacen las demandas máximas de su empresa con una disponibilidad del 99,9%. Despliegue varias marcas y regiones y admita B2B y B2C desde una sola instancia. Admitir catálogos de productos grandes y complejos con modelado de datos flexible.
- **Aumentar la productividad de los comerciantes**: use los servicios de comercialización con tecnología de IA para mejorar la conversión. Experimente de forma nativa, directamente en la tienda. Administre la experiencia de la tienda para crear experiencias enriquecidas en minutos con la creación sencilla basada en documentos o un editor visual.
- **Reducción del coste total de propiedad (TCO) y aceleración de la innovación**: Los servicios siempre actualizados le proporcionan acceso inmediato a las nuevas funciones. Active nuevas funcionalidades instalando fácilmente aplicaciones desde el mercado. Libere recursos del tedioso mantenimiento para centrarse en la creación de nuevas funciones.

### Líderes en tecnología de la información (TI)

- **Aprovisionamiento rápido**: Empiece rápidamente con el aprovisionamiento de autoservicio en minutos. Todos los servicios están preconfigurados para funcionar juntos sin problemas para comenzar más rápido. Aprovisionar zonas protegidas para la experimentación del desarrollador según sea necesario.
- **Bajo costo de propiedad**: No más actualizaciones con servicios siempre actualizados. Manténgase seguro y cumpla con los parches de seguridad más recientes aplicados automáticamente. Escalar automáticamente para satisfacer las cargas de trabajo más exigentes.
- **Tienda de alto rendimiento**: crea experiencias enriquecidas en minutos con la creación simple basada en documentos o un editor visual. Utilice servicios de comercialización con tecnología de IA para mejorar la conversión. Experimentación nativa integrada en la tienda.
- **Innovación más rápida**: Libere recursos de un mantenimiento tedioso para centrarse en crear nuevas capacidades que ofrezcan valor empresarial. Utilice tecnologías completas basadas en estándares y extensibilidad (JavaScript, HTML, CSS y herramientas de código bajo) para crear experiencias diferenciadas. Instale aplicaciones de terceros con un clic para agregar nuevas funciones a su plataforma de comercio.
