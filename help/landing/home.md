---
title: Inicio de guías de servicios
description: Examine la documentación del producto de Adobe Commerce para Servicios SaaS de Commerce
seo-title: Services for Adobe Commerce
seo-description: Access the product documentation for hosted services that help Adobe Commerce merchants support key components of their business.
recommendations: noCatalog
exl-id: 507af1fa-9f3e-41bc-9aaf-cd89839aae0b
source-git-commit: b1c1fa143a9a3e61b3829b923a062b0cee2e5ae9
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---

# Guías de servicios de Adobe Commerce

Los servicios de Adobe Commerce ofrecen potentes funciones que amplían su tienda, optimizan las integraciones y optimizan la administración de datos.

## ¿Cómo se conecta Commerce a los servicios?

Todos los servicios de Commerce se conectan a su instancia de Commerce a través del [conector de servicios de Commerce](saas.md).

Cuando se configura el conector de Commerce Services, tiene acceso a las siguientes funciones:

- **Servicios de tienda**: funciones con tecnología de IA para la detección de productos, recomendaciones y pagos
- **Servicios de integración**: conexiones a Adobe Experience Platform, AEM Assets y otras soluciones de Adobe

Estos servicios le ayudan a aumentar las conversiones, ofrecer experiencias personalizadas y hacer un mejor uso de los datos comerciales en todo el ecosistema de Adobe.

![Nivel de servicios](./assets/services-layer.png)

>[!NOTE]
>
>Adobe recomienda actualizar a la última versión compatible de todos los servicios de Commerce. Ver las [notas de la versión](release-notes-all.md).

Además de estas funciones, hay herramientas que le permiten monitorizar el flujo de datos desde la instancia de Commerce a la plataforma SaaS. Estas herramientas de datos pueden sincronizar automáticamente los datos y ayudarle a optimizar el rendimiento.

## Servicios disponibles

>[!BEGINTABS]

>[!TAB Servicios de tienda]

Los servicios de tienda son un grupo de funciones con tecnología de IA que optimizan el descubrimiento de productos, personalizan las interacciones con los clientes y agilizan el procesamiento de pagos para aumentar la participación y las conversiones. Con los servicios de tienda, puede mejorar la experiencia de compra e impulsar el crecimiento del negocio.

<table style="table-layout:fixed">
<tr style="border: 0;">
   <td valign="top">
      <a href="../catalog-service/overview.md">
      <img alt="Datos de catálogo para servicios conectados" src="../assets/icons/DataBook.svg" width="40">
      </a>
      <div>
         <a href="../catalog-service/overview.md">
         <strong>Servicio de catálogo</strong>
         </a>
      </div>
      <p>
         <em>Ofrezca a sus clientes una experiencia de producto optimizada a la vez que aumenta el rendimiento, mejora la escalabilidad y aumenta las conversiones.</em>
      </p>
   </td>
   <td valign="top">
      <a href="../live-search/overview.md">
      <img alt="Buscar" src="../assets/icons/Magnify.svg" width="40">
      </a>
      <div>
         <a href="../live-search/overview.md">
         <strong>[!DNL Live Search]</strong>
         </a>
      </div>
      <p>
         <em>Implemente esta herramienta de búsqueda con tecnología de IA que ofrezca resultados más inteligentes, rápidos y relevantes para los compradores de B2C.</em>
      </p>
   </td>
   <td valign="top">
      <a href="../product-recommendations/overview.md">
      <img alt="ThumbsUp" src="../assets/icons/ThumbUp.svg" width="40">
      </a>
      <div>
         <a href="../product-recommendations/overview.md">
         <strong>Recomendaciones de productos</strong>
         </a>
      </div>
      <p>
         <em>Agregue recomendaciones impulsadas por IA en función del comportamiento del comprador, las tendencias populares, la similitud de productos y mucho más.</em>
      </p>
   </td>
   <td valign="top">
      <a href="../payment-services/guide-overview.md">
      <img alt="Pagos con tarjeta de crédito" src="../assets/icons/CreditCard.svg" width="40">
      </a>
      <div>
         <a href="../payment-services/guide-overview.md">
         <strong>Servicios de pago</strong>
         </a>
      </div>
      <p>
         <em>Mejore la satisfacción del cliente con diversos métodos de pago, incluidos pagos a plazos sin intereses y vistas optimizadas del procesamiento de pagos, pedidos y facturas.</em>
      </p>
   </td>
</tr>
</table>

>[!TAB Servicios de integración]

Los servicios de integración hacen referencia a funciones que conectan la instancia de Commerce a otros productos o servicios dentro de Adobe.

<table style="table-layout:fixed">
<tr style="border: 0;">
   <td valign="top">
      <a href="../data-connection/overview.md">
      <img alt="Transferencia de datos a la plataforma" src="../assets/icons/TransferToPlatform.svg" width="40">
      </a>
      <div>
         <a href="../data-connection/overview.md">
         <strong>[!DNL Data Connection]</strong>
         </a>
      </div>
      <p>
         <em>Aproveche la conexión entre Adobe Commerce y Adobe Experience Platform Edge para usar datos de Commerce para otros productos de Adobe Experience Cloud, como Adobe Analytics y Adobe Target.</em>
      </p>
   </td>
   <td valign="top">
      <a href="../aem-assets-integration/overview.md">
      <img alt="Visual" src="../assets/icons/images.svg" width="40">
      </a>
      <div>
          <a href="../aem-assets-integration/overview.md">
         <strong>Integración de AEM Assets</strong>
         </a>
      </div>
      <p>
         <em>Simplifique la administración de recursos digitales con un sistema que se integra con Adobe Experience Manager para administrar el contenido multimedia enriquecido.</em>
      </p>
   </td>
</tr>
</table>

>[!TAB Herramientas de datos]

Las herramientas de datos le ayudan a administrar y optimizar el flujo de información entre su instancia de Commerce y los servicios conectados. Estas herramientas garantizan una sincronización de datos eficaz, supervisan las operaciones de sincronización y mejoran el rendimiento descargando procesos que requieren muchos recursos.

<table style="table-layout:fixed">
<tr style="border: 0;">
   <td valign="top">
       <a href="../data-export/overview.md">
      <img alt="Administración de fuentes de exportación de datos SaaS" src="../assets/icons/FeedManagement.svg" width="40">
      </a>
      <div>
         <a href="../data-export/overview.md">
         <strong>[!DNL SaaS Data Export]</strong>
         </a>
      </div>
      <p>
         <em>Sincronizar automáticamente los datos de catálogo, pedido e inventario de Adobe Commerce con los servicios conectados. Use los comandos CLI de Commerce o el <strong>Tablero de administración de datos</strong> para administrar el procesamiento de sincronización.</em>
      </p>
   </td>
   <td valign="top">
      <a href="../price-index/price-indexing.md">
      <img alt="Precios de productos feed" src="../assets/icons/Feed.svg" width="40">
      </a>
      <div>
          <a href="../price-index/price-indexing.md">
         <strong>Indexador De Precios SaaS</strong>
         </a>
      </div>
      <p>
         <em>Optimice el rendimiento del sitio descargando tareas que requieren muchos recursos, como la indexación y el cálculo de precios, de la aplicación Commerce a la infraestructura en la nube de Adobe.</em>
      </p>
   </td>
   <td valign="top">
      <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard" target="_blank">
      <img alt="Monitorización de sincronización de datos" src="../assets/icons/Monitoring.svg" width="40">
      </a>
      <div>
          <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard" target="_blank">
         <strong>Panel de administración de datos</strong>
         </a>
      </div>
      <p>
         <em>Rastree fácilmente la sincronización de datos y la resincronización de déclencheur de Commerce desde un panel unificado en el administrador de Commerce. Obtenga información valiosa sobre la disponibilidad de datos para mostrarlos oportunamente a sus compradores.</em>
      </p>
   </td>
</table>

>[!NOTE]
>
>El tablero de administración de datos está disponible sin coste adicional para los comerciantes de Commerce que usan las recomendaciones de producto v6.0.0, Live Search v4.1.0 o el servicio de catálogo v1.17 con una licencia activa. Los comerciantes que usen versiones de servicio anteriores pueden usar [Sincronización de catálogos](../landing/catalog-sync.md) para administrar y rastrear la sincronización de datos.

>[!ENDTABS]

## ¿Qué problemas pueden resolver los servicios de Commerce?

Tanto si desea escalar su negocio, mejorar las experiencias de los clientes o tomar decisiones basadas en datos, los servicios de Adobe Commerce ofrecen soluciones para los desafíos comunes de Commerce:

| Problema | Desafío | Solución |
|---------|-----------|----------|
| Mejore la detección y conversión de productos | Los compradores no pueden encontrar lo que están buscando, lo que conduce a altas tasas de devolución y pérdidas de ventas. | Use [Live Search](../live-search/overview.md) y [Product Recommendations](../product-recommendations/overview.md) para ofrecer búsquedas con tecnología de IA y tolerancia a errores tipográficos, resultados instantáneos de &quot;búsqueda mientras escribe&quot;, facetas dinámicas y recomendaciones personalizadas de productos basadas en el comportamiento de compradores en tiempo real. |
| Creación de experiencias personalizadas omnicanal | Los datos de comercio están en silo, lo que impide ofrecer experiencias personalizadas en todos los canales. | Use [Conexión de datos](../data-connection/overview.md) para enviar datos de comportamiento, transaccionales y de perfil a Adobe Experience Platform. Genere segmentos de clientes sofisticados, cree campañas de carros de compras abandonados, dirija audiencias similares y analice las tendencias estacionales en todo el recorrido de clientes. |
| Administración de recursos digitales optimizada | La administración de imágenes de productos y medios enriquecidos en varios sistemas es una tarea laboriosa y propensa a errores. | La integración de [AEM Assets](../aem-assets-integration/overview.md) proporciona administración de recursos centralizada al conectar Adobe Commerce a un proyecto de Adobe Experience Manager Assets, simplificar los flujos de trabajo y garantizar experiencias de marca coherentes en todos los puntos de contacto. |
| Optimizar procesamiento de pagos | Las opciones de pago limitadas y las malas experiencias de pago están afectando la satisfacción y la conversión del cliente. | [Servicios de pago](../payment-services/guide-overview.md) ofrece varios métodos de pago, incluidos pagos a plazos sin intereses, con un tablero unificado para administrar pagos, pedidos y facturas. |
| Administrar la sincronización de datos a escala | La indexación con uso intensivo de recursos está ralentizando el sitio y no puede rastrear fácilmente los problemas de sincronización de datos. | [SaaS Data Export](../data-export/overview.md), [SaaS Price Indexer](../price-index/price-indexing.md) y [Data Management Dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) sincronizan automáticamente los datos de catálogo, pedido e inventario, descargan cálculos de precios a la infraestructura en la nube de Adobe y proporcionan visibilidad en tiempo real del estado de sincronización. |
| Recuperar clientes perdidos y reducir los retornos | Las altas tasas de pérdida de clientes y de devolución de productos están afectando a la rentabilidad. | Combine [Conexión de datos](../data-connection/overview.md) con Adobe Journey Optimizer y Real-Time CDP para identificar patrones de retorno, crear campañas de recuperación, segmentar clientes por comportamiento y enviar campañas de participación personalizadas por correo electrónico y SMS. |
| Toma de decisiones de comercialización basadas en datos | No está seguro de qué productos promocionar o cuándo ejecutar promociones. | [Live Search](../live-search/overview.md) proporciona perspectivas de rendimiento de búsqueda y herramientas de comercialización para acceder a métricas clave, analizar términos de búsqueda y usar reglas de comercialización inteligentes para impulsar o enterrar productos basados en el comportamiento real de los clientes y los objetivos comerciales. |
| Mantener el cumplimiento de los datos confidenciales | Debe gestionar los datos confidenciales de los clientes y, al mismo tiempo, mantener el cumplimiento de HIPAA. | [La conexión de datos](../data-connection/overview.md) está preparada para HIPAA, lo que le permite compartir datos del back-office con Experience Platform al tiempo que mantiene el cumplimiento y gestiona sistemáticamente las solicitudes de privacidad. |

{{$include /help/_includes/templated/whats-new.md}}

<!-- Last updated from includes: 2025-12-19 22:44:55 -->
