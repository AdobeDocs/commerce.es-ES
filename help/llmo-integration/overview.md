---
title: Integrar [!DNL Adobe Commerce] con [!DNL Adobe LLM Optimizer]
description: Conéctese [!DNL Adobe Commerce] a [!DNL Adobe LLM Optimizer] para supervisar las señales del catálogo en LLM e implementar las optimizaciones del catálogo aprobadas.
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Integrar [!DNL Adobe Commerce] con [!DNL Adobe LLM Optimizer]

>[!IMPORTANT]
>
>El acceso a esta integración está restringido. Póngase en contacto con el administrador de cuentas técnico para obtener más información.

[!DNL Adobe LLM Optimizer] es una solución empresarial que ayuda a las marcas a supervisar, analizar y optimizar el aspecto de su contenido en las respuestas de modelos de lenguaje grande (LLM) y asistentes de IA. A medida que los compradores utilizan cada vez más las herramientas de IA para la investigación y el descubrimiento de productos, LLM Optimizer ayuda a garantizar que su marca y catálogo se citen con precisión y aparezcan en contexto.

En esta guía se describe cómo se adapta **[!DNL Adobe Commerce]** a ese flujo de trabajo cuando el catálogo de productos se almacena en Commerce. Aprenderá qué funciones están disponibles, qué configuración se requiere y cómo se comportan las optimizaciones implementadas en el administrador y en los canales de ingesta.

>[!NOTE]
>
>[!DNL Adobe LLM Optimizer] es una solución independiente de Adobe. Los flujos de trabajo de oportunidad y supervisión principales no requieren [!DNL Adobe Experience Manager] (AEM) u otras aplicaciones de Adobe. Las acciones de implementación específicas de Commerce solo se aplican cuando el catálogo está conectado a LLM Optimizer y usted decide insertar los cambios aprobados en [!DNL Adobe Commerce].

## Qué habilita la integración {#what-integration-enables}

Conectar LLM Optimizer a su catálogo [!DNL Adobe Commerce] le permite pasar de perspectivas de contenido generales a **recomendaciones según el catálogo**:

- **Identifique** lagunas e incoherencias en los datos del catálogo (como títulos, descripciones y señales estructuradas) que afectan la interpretación que hacen los LLM de sus productos.
- **Revisar** sugirió mejoras con contexto de soporte, incluyendo justificaciones y comparaciones de antes y después.
- **Implementar** las optimizaciones seleccionadas (como las actualizaciones de nombre y descripción del producto) directamente en el catálogo de Commerce, lo que garantiza que los flujos de trabajo de administración, las cuadrículas y los datos de la tienda permanezcan alineados.

Cuando el origen del catálogo es [!DNL Adobe Commerce], Adobe puede admitir el flujo de trabajo completo de extremo a extremo: identificar automáticamente las oportunidades, sugerir cambios y aplicar correcciones aprobadas. En el caso de los catálogos que se originan fuera de Commerce, LLM Optimizer puede seguir analizando y sugiriendo mejoras, pero la aplicación de los cambios depende del modelo de integración (por ejemplo, un catálogo duplicado o actualizaciones manuales). Consulte [Límites y límites de integración](boundaries-limits.md).

## Para quién es esto {#who-this-is-for}

- **Comerciantes y especialistas en marketing digital** que desean que los datos de los productos sean precisos y coherentes en las respuestas basadas en LLM y que necesitan una forma controlada de mejorar la copia del catálogo a escala.
- **Administradores de Commerce** propietarios de la integridad del catálogo, los procesos de administración y las integraciones (API, CSV, PIM) que alimentan los atributos del producto.

## Requisitos previos {#prerequisites}

Los siguientes requisitos previos se aplican cuando tiene **acceso** a la integración de Adobe Commerce con Adobe LLM Optimizer. Póngase en contacto con el administrador de cuentas técnico para obtener más información.

- La tienda se puede rastrear mediante bots agénticos y orientados a LLM, donde esta capacidad de rastrear forma parte de la estrategia de optimización y medición de LLM Optimizer (un requisito previo general para las perspectivas según el catálogo).
- Para los flujos de trabajo de implementación respaldados por Commerce, los servicios Commerce y la conectividad del catálogo necesarios están habilitados y en buen estado. La configuración de nivel de tarea se describe en [Conectar Adobe Commerce a LLM Optimizer](get-started/connect-to-llmo.md).

También debe comprender cómo se mueven los datos entre sistemas:

### Flujo de datos de alto nivel {#high-level-data-flow}

Conceptualmente, las optimizaciones del catálogo siguen dos patrones (el proyecto puede utilizar uno o ambos, según la capacidad):

| Dirección | Finalidad |
| --- | --- |
| **catálogo de Commerce -> LLM Optimizer** | Las oportunidades y sugerencias de fuentes de señales de catálogo y URL en la IU de LLM Optimizer. |
| **LLM Optimizer -> Commerce** | Después de aprobar una acción de implementación, las actualizaciones del nombre y la descripción del producto se escriben en el catálogo principal de Commerce para que el administrador y la tienda reflejen los valores optimizados. |

### [!DNL Adobe Commerce] comparado con catálogos de terceros {#commerce-vs-third-party}

| Origen del catálogo | Cobertura típica de LLM Optimizer |
| --- | --- |
| **[!DNL Adobe Commerce]** | Gran compatibilidad con la identificación y las sugerencias, además de implementar las actualizaciones de campo de catálogo aprobadas que configure. |
| **Comercio de terceros** | Se admiten sugerencias e identificación; la implementación automatizada en el sistema de comerciantes depende de la exportación, la duplicación o los flujos de trabajo de socios, en lugar de las escrituras directas en el catálogo de origen del comerciante. |

## Agente de catálogo, MCP de tienda y LLM Optimizer {#catalog-agent-and-mcp}

Su [!DNL Adobe Commerce] **catálogo de productos** es el sistema de registro de datos de productos: nombres, descripciones, atributos, precios e inventario. Para impulsar la detección y optimización asistidas por IA, **Adobe Commerce Storefront MCP** (Model Context Protocol) es una interfaz estructurada entre los datos del catálogo de Commerce activos y las experiencias de Adobe AI.

**Agente de catálogo** se encuentra en la parte superior del MCP de Storefront. El agente de catálogo permite que [!DNL Adobe LLM Optimizer] consulte, enriquezca y actúe en el contexto del catálogo y de la PDP al identificar lagunas, proponer mejoras e implementar cambios cuando los apruebe. Estas funcionalidades aparecen en los flujos de trabajo de LLM Optimizer descritos en [Usar LLM Optimizer con Adobe Commerce](get-started/use-llmo-with-commerce.md).

## Cómo mejora el agente de catálogo Commerce para LLM {#catalog-agent-optimizations}

El agente de catálogo aborda la capacidad de detección mediante dos optimizaciones complementarias: enriquecimiento de la página de detalles del producto y enriquecimiento del catálogo del producto.

### Enriquecimiento de página de detalles del producto {#pdp-enrichment-overview}

El enriquecimiento de la **página de detalles del producto (PDP)** sugiere refinamientos en el contenido de la página del producto para que la mercancía se lea más claramente cuando los compradores descubren los productos a través de asistentes de IA y herramientas similares. El objetivo es mejorar la claridad y la coherencia sin cambiar el diseño de la tienda que su equipo ya comercializó. Puede revisar las sugerencias en LLM Optimizer e implementarlas cuando esté listo.

Después de la implementación, consulte la página de productos en directo para confirmar que la experiencia de compra sigue teniendo el aspecto esperado.

### Enriquecimiento del catálogo de productos {#catalog-enrichment-overview}

**El enriquecimiento del catálogo de productos** sugiere **nombres de productos** y **descripciones de productos** más claros en los que la copia es delgada, vaga o incoherente. Cada sugerencia incluye un contexto para que su equipo pueda decidir qué cambiar. Cuando aprueba una actualización, se puede aplicar al catálogo [!DNL Adobe Commerce] para que el administrador, la tienda y otras experiencias que usen esos campos reflejen la misma redacción.

Puesto que estos campos se encuentran en Commerce, mejorar un nombre o una descripción una vez puede beneficiar a todos los canales que lean los datos del producto (según cómo y cuándo se actualicen los sistemas).

## Temas relacionados {#related-topics}

- [Conectar Adobe Commerce a LLM Optimizer](get-started/connect-to-llmo.md)
- [Uso de LLM Optimizer con Adobe Commerce](get-started/use-llmo-with-commerce.md)
- [Límites y límites de integración](boundaries-limits.md)
