---
title: Migrar a  [!DNL Adobe Commerce as a Cloud Service]
description: Obtenga información sobre cómo migrar a  [!DNL Adobe Commerce as a Cloud Service].
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 34057c1e55ff117ea7aab4407f31548ce826691b
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---

# Migrar a [!DNL Adobe Commerce as a Cloud Service]

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service] proporciona la mayor parte de la configuración de forma predeterminada. Sin embargo, si está migrando desde una instancia existente de Adobe Commerce en la nube o local, deberá realizar diferentes acciones de migración según la configuración específica.

## Rutas de migración

[!DNL Adobe Commerce as a Cloud Service] admite varias rutas de migración, según la cronología, la tienda y las personalizaciones.

Como alternativa a una migración completa, [!DNL Adobe Commerce as a Cloud Service] admite una migración por fases mediante Commerce Optimizer o un método incremental.

* **Migración incremental**: este enfoque implica migrar los datos, las personalizaciones y las integraciones por fases. Este enfoque es ideal para grandes comerciantes con muchas personalizaciones que deseen realizar una transición gradual de sus personalizaciones y datos complejos a [!DNL Adobe Commerce as a Cloud Service] a su propio ritmo.

![migración incremental](./assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer**: este enfoque le permite migrar de forma iterativa, utilizando Commerce Optimizer como una fase de transición para mover personalizaciones y datos complejos a [!DNL Adobe Commerce as a Cloud Service] a su propio ritmo. Commerce Optimizer proporciona acceso a servicios de comercialización ofrecidos por canales y directivas de catálogo, Commerce Storefront con tecnología de Edge Delivery y productos visuales ofrecidos por AEM Assets.

![migración iterativa](./assets/optimizer.png){width="600" zoomable="yes"}

* **Migración completa**: este enfoque implica migrar todos los datos, las personalizaciones y las integraciones a la vez. Este enfoque es ideal para comerciantes más pequeños con pocas personalizaciones que deseen realizar una transición rápida a [!DNL Adobe Commerce as a Cloud Service].

La siguiente tabla proporciona información general del proceso de migración para diferentes tiendas y configuraciones:

|                    | Tienda de LUMA | PWA Storefront | Tienda Commerce con tecnología de Edge Delivery | Headless |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| Migración de datos | Requerido | Requerido | Requerido | Requerido |
| Tienda | Migrar a Commerce Storefront con tecnología de Edge Delivery | Migrar a Commerce Storefront con tecnología Edge Delivery o Mantener | Sin impacto | Sin impacto |
| API Mesh | Crear nueva malla | Crear nueva malla o volver a configurar la existente | Crear nueva malla o volver a configurar la existente | Crear nueva malla o volver a configurar la existente |
| Integraciones | Aproveche el Starter Kit de integración | Aproveche el Starter Kit de integración | Aproveche el Starter Kit de integración | Aproveche el Starter Kit de integración |
| Personalizaciones | Paso a App Builder y API Mesh | Paso a App Builder y API Mesh | Paso a App Builder y API Mesh | Paso a App Builder y API Mesh |
| Administración de Assets | Migración necesaria si se utiliza OOTB | Migración necesaria si se utiliza OOTB | Migración necesaria si se utiliza OOTB | Migración necesaria si se utiliza OOTB |
| Extensiones | Migrar a App Builder | Migrar a App Builder | Migrar a App Builder | Migrar a App Builder |

Como se indica en la tabla, las mitigaciones para cada migración consistirán en:

* **Migración de datos**: Se están utilizando las herramientas de migración proporcionadas para migrar datos de la instancia existente a [!DNL Adobe Commerce as a Cloud Service].
* **Storefront**: las tiendas EDS y sin encabezado existentes no requieren mitigación, pero las tiendas LUMA requieren migrar a Commerce Storefront con tecnología Edge Delivery. Las tiendas de PWA Studio se pueden migrar a Commerce Storefront con tecnología de Edge Delivery o se pueden mantener en su estado actual. Adobe proporcionará aceleradores para ayudar con la migración de tiendas.
* **[Mesh de API](https://developer.adobe.com/graphql-mesh-gateway)**: cree una nueva malla o modifique la existente. Adobe proporcionará mallas preconfiguradas para ayudarle con este proceso.
* **Integraciones**: todas las integraciones deben aprovechar [integration starter kit](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) o [[!DNL Adobe Commerce as a Cloud Service] REST API](https://developer.adobe.com/commerce/services/reference/cloud-service/core-admin/).
* **Personalizaciones**: todas las personalizaciones deben moverse a App Builder y a la malla de API.
* **Administración de Assets**: la administración de todos los recursos requiere migración. Si ya utiliza AEM Assets, no es necesario realizar la migración.
* **Extensiones**: todas las extensiones en proceso deben volver a crearse como extensiones fuera de proceso. A finales de 2025, Adobe proporcionará acceso a nuestras extensiones más populares para minimizar los tiempos de compilación.

## Fases de migración

La migración de la instancia actual de Adobe Commerce a una nueva instancia de [!DNL Adobe Commerce as a Cloud Service] implica principalmente las fases siguientes:

* **[Preparación](#readiness-phase)**: Comience por determinar si la implementación está lista para moverse a ACCS. En esta fase también deberá familiarizarse con los cambios introducidos por ACCS&#x200B;
* **[Implementación](#implementation-phase)**: a continuación, prepare su código, tienda, extensiones e integraciones para la migración. Para facilitar la transición, Adobe permite [enfoques iterativos a corto y largo plazo](#migration-paths).&#x200B;
* **[Publicar](#go-live-phase)**: compruebe y confirme que todo está listo y, a continuación, realice la migración de datos.
* **[Publicar lanzamiento](#post-go-live-phase)**: en colaboración con Adobe, supervise los problemas y mejore el rendimiento según sea necesario una vez completada la migración.

### Fase de preparación

1. Comience por revisar la arquitectura de [!DNL Adobe Commerce as a Cloud Service], el marco de trabajo de extensibilidad y las capacidades de la tienda:

   * [Arquitectura de Adobe Commerce en Cloud Services](./overview.md): revise la arquitectura de la plataforma y en qué se diferencia de la instancia de Adobe Commerce actual.
   * [Marco de trabajo de extensibilidad de Adobe Commerce](https://developer.adobe.com/commerce/extensibility/): identifique cómo desea realizar la transición de las personalizaciones actuales.
   * [Tienda Commerce con tecnología Edge Delivery](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=es): revisa la solución de tienda recomendada.

1. Auditoría de la compatibilidad de personalización:

   * Identifique los módulos personalizados actuales y las integraciones de terceros.
   * Evalúe las personalizaciones que necesitan reimplementación con App Builder.
   * Asigne las personalizaciones actuales a sus equivalentes de extensiones de App Builder.

1. Confirme los requisitos de la tienda y asegúrese de que se alinean con las capacidades de Adobe Edge Delivery.

1. Revise las integraciones actuales de terceros y confirme la compatibilidad de la API con la plataforma [!DNL Adobe Commerce as a Cloud Service].

### Fase de implementación

Los siguientes pasos describen el proceso de desarrollo y ejecución de la migración:

1. Crear una nueva instancia de [!DNL Adobe Commerce as a Cloud Service] en [Commerce Cloud Manager](./getting-started.md#create-an-instance).

1. Instale las aplicaciones y personalizaciones necesarias. [!DNL Adobe Commerce as a Cloud Service] tiene acceso a nuestras aplicaciones más populares. Si necesita aplicaciones o personalizaciones adicionales, puede volver a implementarlas con App Builder.

1. Configure una de las siguientes tiendas basadas en GraphQL:

   * [Crear una tienda Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=es)
   * [Usa PWA Studio para crear una tienda personalizada basada en GraphQL](https://developer.adobe.com/commerce/pwa-studio/)

1. Migre los datos de la instancia anterior de Commerce a ACCS:

   * Migrar datos nativos de Adobe Commerce mediante las herramientas de migración de datos.
   * Migración de extensiones y personalizaciones de terceros
   * Migrar datos de configuración e integración:
      * Transfiera configuraciones de malla de API, servicios de terceros e integraciones de sistemas usando [Adobe Commerce Integration Starter Kit](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/).

### Fase de lanzamiento

Antes de iniciar, valide y pruebe la nueva instancia de [!DNL Adobe Commerce as a Cloud Service] mediante un entorno de zona protegida:

* **Pruebas funcionales**: Asegúrese de que los datos migrados, la funcionalidad de la tienda y las personalizaciones funcionen sin problemas.

* **Pruebas de rendimiento**: evalúe la velocidad y la escalabilidad de sus tiendas para garantizar un rendimiento óptimo a nivel global.

* **Auditoría de seguridad**: revise las medidas de seguridad, incluido el control de acceso a la API y las posibles vulnerabilidades.

Una vez validada y probada la nueva instancia de zona protegida [!DNL Adobe Commerce as a Cloud Service], puede iniciar la instancia de producción.

### Fase de Publicar Go-Live

Después del lanzamiento, realice estas actividades posteriores al lanzamiento:

1. Seguimiento del lanzamiento

   * Redirija el tráfico a la nueva plataforma y supervise el rendimiento.
   * Deshabilite la instancia de Adobe Commerce anterior.

1. Monitorización posterior al lanzamiento

   * Utilice herramientas de monitorización para garantizar operaciones estables y abordar cualquier problema posterior al lanzamiento.
