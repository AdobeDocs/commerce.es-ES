---
title: Migrar a  [!DNL Adobe Commerce as a Cloud Service]
description: Obtenga información sobre cómo migrar a  [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
role: Developer
level: Intermediate
autotag-review: '2026-06-18T16:12:28.840Z'
TQID: 'https://experienceleague.adobe.com/GmxaQdGKvAIDpZ2jvmlLFSYw0IFQysIMOT0lUnsJBsI'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: bd989d82-1e15-4534-88db-f1f51dd77ffaid: c1256247-af4b-46d8-9dca-0c654ecfa157id: c18ed297-2187-4aec-affb-9d9654eca6fcid: c32adafa-ed01-4b31-997e-2413013911b0id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2: id: e91a50b1-0b31-436e-9033-00e4776e94cbid: f56d26ed-050b-4fb7-b29b-8e6e994e80a2id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: addc3a3a-2b1c-4fdf-aea4-4b1eb2931ba6id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: d095671a-1355-40aa-8b5f-06c33c68080bid: eb30f47f-d87a-400f-8f78-63ce7979ff56id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: bef6657cdf6703b6a0a1109bd6582ecbe4e19930
workflow-type: tm+mt
source-wordcount: 3302
ht-degree: 0%

---

# Migrar a [!DNL Adobe Commerce as a Cloud Service]

Esta guía ayuda a los desarrolladores a pasar de [!DNL Adobe Commerce on Cloud] o locales a [!DNL Adobe Commerce as a Cloud Service] (SaaS). Este modelo SaaS ofrece rendimiento, escalabilidad e integración mejorados con [!DNL Adobe Experience Cloud].

>[!NOTE]
>
>Para obtener más información sobre las herramientas de migración, consulte [herramienta de migración de datos en lotes](./bulk-data/migration-tool.md).

## Información general

Migrar un almacén de [!DNL Adobe Commerce] establecido a [!DNL Adobe Commerce as a Cloud Service] es más que mover datos. Una migración real abarca las siguientes áreas:

- Aplicación: personalizaciones y extensiones creadas para [!DNL Adobe Commerce on Cloud] o instalaciones locales
- Datos: catálogos, pedidos, clientes y configuración
- Tienda
- Integraciones con sistemas externos

[!DNL Adobe Commerce as a Cloud Service] es una plataforma SaaS sin versiones, lo que significa que ninguna de estas áreas se puede migrar sin adaptarlas. Las personalizaciones se modernizan en aplicaciones de [!DNL App Builder], las tiendas se reconstruyen en Edge Delivery Services (EDS), los datos se migran al nuevo inquilino de [!DNL Adobe Commerce as a Cloud Service] y las integraciones se restablecen usando patrones SaaS.

En lugar de considerar la migración como un único proyecto monolítico, Adobe proporciona un flujo de trabajo de migración integrado basado en [tres herramientas de migración](#migration-tools-workflow).

Este flujo de trabajo compartido consolida el descubrimiento, alinea los equipos de ingeniería y entrega y proporciona un plan de migración coherente.

![diagrama de flujo de migración](../assets/migration-flow.png)

### Comparación de PaaS y SaaS

[!DNL Adobe Commerce on Cloud] o en línea (PaaS) y [!DNL Adobe Commerce as a Cloud Service] (SaaS) difieren en la forma en que se administran y en la forma en que los comerciantes interactúan con la plataforma.

**Diferencias clave**

- [!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."}
- **[!DNL Adobe Commerce on Cloud Infrastructure]**: el comerciante administra el código de la aplicación, las actualizaciones, los parches y la configuración de la infraestructura.
- **[!DNL Adobe Commerce]local**: El comerciante administra el código de la aplicación, las actualizaciones, los parches y la configuración de la infraestructura en el entorno alojado de Adobe.

  >[!NOTE]
  >
  >[Modelo de responsabilidad compartida](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility) para servicios (MySQL, Elasticsearch y otros).

- [!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."} **SaaS (Nuevo — [!DNL Adobe Commerce as a Cloud Service])**: Adobe administra completamente la aplicación, la infraestructura y las actualizaciones principales. Los comerciantes se centran en la personalización a través de puntos de extensibilidad (API, App Builder, SDK de IU). Código de la aplicación principal bloqueado.

**Implicaciones arquitectónicas**

- **Plataforma sin versiones**: las actualizaciones continuas significan que no habrá más actualizaciones de versiones principales para el núcleo.
- **Microservicios y API-First**: mayor dependencia de las API para la extensibilidad y la integración.
- **Sin encabezado de forma predeterminada (opcional)**: Compatibilidad sólida con escaparates disociados (por ejemplo, Commerce Storefront con tecnología Edge Delivery Services).
- **Edge Delivery Services**: Impacto en el rendimiento y la implementación del front-end.

**Nuevas herramientas y conceptos**

- [Adobe Developer App Builder](https://developer.adobe.com/app-builder/) y [API Mesh para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/)
- [Commerce Optimizer](../../optimizer/overview.md)
- [Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/)
- Aprovisionamiento de autoservicio con [Commerce Cloud Manager](../getting-started.md#create-an-instance)

### El recorrido de migración

Una migración se desplaza por las siguientes fases:

- **Evaluar**: analice la implementación existente y tenga en cuenta lo siguiente: personalizaciones de inventario, integraciones, características de tienda y estructuras de datos. Después de analizar, cree una hoja de ruta con recomendaciones de migración, puntuación de complejidad y estimaciones de esfuerzo.
- **Modernizar la aplicación y migrar datos**: vuelva a generar personalizaciones como [!DNL App Builder] aplicaciones al migrar datos profesionales a [!DNL Adobe Commerce as a Cloud Service].
- **Modernizar la tienda**: reconstruye la tienda en Edge Delivery Services (EDS) para Commerce.
- **Interrumpir y operar**: cambie el tráfico a [!DNL Adobe Commerce as a Cloud Service], elimine los sistemas heredados y realice la transición a una operación en curso.

La migración suele ser iterativa, no lineal. Las organizaciones pueden evaluar varios entornos, validar las recomendaciones, modernizarse gradualmente y refinar los planes de implementación antes de la migración final de la producción.

### Flujo de trabajo de herramientas de migración

Cada uno de los flujos de trabajo siguientes tiene su propia herramienta. Utilícelos juntos para completar la migración. La evaluación de la migración sirve como modelo común utilizado durante toda la migración.

| Flujo de trabajo | Herramienta | Descripción |
| --- | --- | --- |
| [Evaluación](#migration-assessment-tool) | **Herramienta de evaluación de la migración** | Evaluación basada en IA de la implementación existente que inventarie módulos personalizados, extensiones de terceros, integraciones, observaciones de tienda, esquema de base de datos, tablas personalizadas, recomendaciones de migración, puntuación de complejidad y estimaciones de esfuerzo de modernización. |
| [Modernización de aplicaciones y tiendas](#code-and-storefront-migration-commerce-developer-mcp) | **Commerce Developer MCP** | Modernización asistida por IA de la aplicación Commerce, que acelera la migración de las personalizaciones a [!DNL App Builder], admite la transformación de tiendas a Edge Delivery Services (EDS) y guía a los desarrolladores a través del recorrido más amplio de modernización de aplicaciones con implementación revisada y validada por equipos de ingeniería. |
| [Migración de datos](#data-migration-commerce-data-migration-service) | **Servicio de migración de datos de Commerce** | Extracción, carga y verificación de integridad de datos de catálogo, cliente y pedido en [!DNL Adobe Commerce as a Cloud Service]. |

Estas pistas no son independientes. El uso conjunto en el orden correcto minimiza la reutilización.

- **Ejecute primero la evaluación**: al ejecutar primero la evaluación se identifican las personalizaciones no admitidas, se estima el esfuerzo de migración, se exponen las consideraciones sobre la migración de datos y se resaltan las dependencias de la integración antes de que comience la implementación. La evaluación se convierte en el modelo de migración utilizado por los flujos de trabajo de modernización de aplicaciones y migración de datos.
- **Modernización de aplicaciones**: el MCP para desarrolladores de Commerce usa la evaluación de migración para determinar qué personalizaciones modernizar y cómo hacerlo. A continuación, el MCP genera las [!DNL App Builder] aplicaciones y componentes de tienda correspondientes.
- **Migración de datos**: el cuestionario de ámbito de la migración de datos captura el ámbito, los volúmenes y las tablas personalizadas que surgieron en la evaluación.
- **Datos personalizados y de terceros**: los datos que contienen las extensiones de terceros en tablas personalizadas se identifican durante la evaluación, pero no se gestionan mediante la migración de datos estándar y requieren una personalización de [!DNL App Builder].

La modernización de tiendas no es solo una migración de IU. Además de migrar la funcionalidad empresarial, debe tener en cuenta la arquitectura de la experiencia, la modernización de componentes reutilizables, la optimización del rendimiento y la adopción de patrones de Edge Delivery Services.

Las integraciones se evalúan como parte de la evaluación de la migración, pero su implementación varía según el escenario. Las integraciones pueden aprovechar las API [!DNL App Builder], [!DNL API Mesh], Adobe I/O Events y [!DNL Adobe Commerce as a Cloud Service].

Estas herramientas de migración siguen ampliándose y manteniendo un flujo de trabajo de migración unificado centrado en la evaluación de la migración.

### Pasos siguientes

Cuando esté listo para migrar, comience creando una evaluación. La evaluación de la migración establece el plan que sigue el resto de la migración.

La herramienta de evaluación de la migración y el MCP para desarrolladores de Commerce utilizan IA para ayudarle con la detección, la planificación y la implementación. Al igual que con cualquier flujo de trabajo de ingeniería, las recomendaciones e implementaciones generadas por IA deben ser revisadas y validadas cuidadosamente por su equipo como parte de la arquitectura estándar, las pruebas y los procesos de garantía de calidad.

## Herramienta de evaluación de migración

Antes de comenzar el desarrollo o la migración, debe tener en cuenta el tamaño de la migración y determinar los elementos que requieren desarrollo. Es probable que un almacén de [!DNL Adobe Commerce] en [!DNL Adobe Commerce on Cloud] o local tenga módulos personalizados, integraciones, personalizaciones de tienda y estructuras de datos, lo cual podría no ser obvio hasta que alguien analice la implementación. La Herramienta de evaluación de la migración analiza automáticamente el código base para identificar estos elementos para su desarrollo.

### Resumen de evaluación

La herramienta de evaluación de la migración realiza una evaluación de IA de la implementación existente y produce una evaluación de modernización estructurada y una hoja de ruta de migración de [!DNL Adobe Commerce as a Cloud Service]. También crea una vista completa de la migración mediante la evaluación de las personalizaciones de las aplicaciones, las integraciones, las estructuras de datos, las características de la tienda y otros detalles de implementación que influyen en la modernización. Convierte el descubrimiento en un proceso rápido y repetible que le permite evaluar el esfuerzo, el riesgo y la secuencia antes de contraer compromisos.

La evaluación que produce la Herramienta de evaluación de la migración no es solo un informe. La evaluación se convierte en un artefacto de migración compartida que informa la planificación, la implementación y la validación a lo largo del ciclo de vida de la migración. Como primera fase del recorrido de migración, sus conclusiones se refieren tanto a la modernización de las aplicaciones como a los esfuerzos de migración de datos que siguen.

Para obtener más información sobre qué se incluye en un informe de evaluación de migración y cómo utilizarlo, consulte [Evaluación de migración](./assessment.md).

### Fases de evaluación

Se realiza una evaluación de la implementación existente y se procede a través de una serie de etapas automatizadas:

- **Inventario** — Cataloga la implementación. Incluye: módulos personalizados, dependencias del Compositor, extensiones de terceros, configuración, componentes de tienda (cuando corresponda), archivos, puntos de extensibilidad, eventos, complementos, API, trabajos cron, colas, esquema de base de datos y tablas de base de datos personalizadas.
- **Analizar**: realiza un análisis estático para identificar las personalizaciones del almacén, la divergencia con respecto a una instalación estándar de [!DNL Adobe Commerce] y cómo interactúan esas personalizaciones en toda la aplicación.
- **Clasificar**: utiliza IA para interpretar cada personalización, resumiendo lo que hace la personalización, agrupando las capacidades relacionadas, identificando patrones de implementación y proporcionando recomendaciones de migración contextual.
- **Asignar y recomendar**: asigna cada capacidad a su equivalente [!DNL Adobe Commerce as a Cloud Service], incluidas: capacidades predeterminadas, [!DNL App Builder] aplicaciones o servicios de Adobe. A continuación, la evaluación recomienda una ruta de modernización y evalúa la complejidad, las dependencias y el esfuerzo de implementación.
- **Informe**: genera una hoja de ruta exportable para la planificación de la ejecución de la migración, que le permite comunicar el riesgo a las partes interesadas. También identifica prioridades, dependencias, deuda técnica y riesgos de implementación.

### Valor de evaluación

El valor de una evaluación es la cantidad de confianza que puede tener antes de comprometerse con los aspectos específicos del desarrollo. En lugar de estimar una migración con prácticas de ámbito regulares, la evaluación proporciona una comprensión basada en pruebas de la implementación. Esto incluye qué personalizaciones son sencillas de migrar, cuáles requieren rediseño y cuáles se pueden retirar por completo. Las evaluaciones aparecen de forma rutinaria como funciones obsoletas o no utilizadas, lo que le permite reducir la deuda técnica.

Cada recomendación incluye pruebas de apoyo junto con citas de la implementación subyacente, lo que permite a los arquitectos e ingenieros validar durante la planificación. Dado que cada evaluación sigue la misma metodología, puede comparar varias necesidades de desarrollo mediante un marco de trabajo coherente de puntuación y planificación.

La evaluación no es sólo un punto de partida. La herramienta de migración descendente utiliza los resultados de la evaluación para acelerar la implementación y mantener la coherencia con el plan de migración aprobado. El análisis de personalización se convierte en el modelo para la modernización de aplicaciones, mientras que la evaluación de datos abarca el esfuerzo de migración de datos analizando el tamaño de la base de datos, el inventario de entidades y las tablas personalizadas.

### Ámbito de evaluación

La herramienta de evaluación de la migración se centra en comprender el panorama completo de la migración. Analiza módulos personalizados, complementos, eventos, API, trabajos cron, colas, integraciones con sistemas externos, características de tienda y el esquema de base de datos del que dependen esas personalizaciones. La evaluación asigna lo que detecta a las capacidades disponibles de [!DNL Adobe Commerce as a Cloud Service] e identifica dónde debe rediseñar para la arquitectura SaaS o modernizar la funcionalidad mediante [!DNL App Builder].

La evaluación es más una herramienta de planificación que de ejecución. Identifica lo que debe modernizarse, estima la complejidad de la implementación y proporciona recomendaciones. Las decisiones de implementación y la validación de arquitectura siguen siendo actividades de colaboración entre Adobe, socios y equipos de ingeniería de clientes.

Los datos almacenados en tablas personalizadas por extensiones de terceros se muestran como una consideración de migración. La migración de datos estándar no migra estos datos automáticamente. Se podrían requerir aplicaciones [!DNL App Builder] personalizadas para admitir estos escenarios. Consulte [Guía de migración de datos](#data-migration-commerce-data-migration-service) para obtener más información.

La evaluación proporciona un análisis de los flujos de trabajo de personalización y migración de datos de la tienda:

- Migración de código y tienda: el análisis de aplicaciones de la evaluación se convierte en el modelo para el MCP de desarrollador de Commerce
- Migración de datos: el inventario de entidades de la evaluación, el análisis de características de la base de datos y el análisis de tablas personalizado establecen el ámbito del servicio de migración de datos de Commerce.

También puede volver a ejecutar las evaluaciones a medida que evolucionen las aplicaciones. Esto permite a sus equipos validar el trabajo de corrección, medir el progreso de modernización y refinar continuamente los planes de migración a lo largo de la participación.

### Pasos siguientes

Cada migración de [!DNL Adobe Commerce as a Cloud Service] comienza con una evaluación. Es una forma rentable de establecer el ámbito, reducir la incertidumbre y crear un modelo de migración compartida antes de que comience la implementación.

Para obtener más información sobre las herramientas de evaluación y el flujo de trabajo para desarrolladores descendente, consulte [Adobe Commerce Developer MCP](https://developer.adobe.com/commerce/extensibility/developer-agent/).

## Migración de código y tienda (Commerce Developer MCP)

En [!DNL Adobe Commerce on Cloud] o las personalizaciones locales pueden utilizar PHP en proceso: módulos, complementos y observadores de eventos que se ejecutan dentro de la aplicación. [!DNL Adobe Commerce as a Cloud Service] es una plataforma SaaS sin versiones y ese modelo ya no se aplica. Las personalizaciones se ejecutan como aplicaciones [!DNL Adobe Developer App Builder] fuera de proceso que se integran con Commerce a través de eventos y API. Modernizar las personalizaciones de una tienda para esta arquitectura suele ser el esfuerzo de ingeniería más significativo de una migración de [!DNL Adobe Commerce as a Cloud Service].

### Resumen de migración de código

A partir de la evaluación de la migración, el MCP para desarrolladores de Commerce proporciona una experiencia IDE conversacional para modernizar las personalizaciones de PHP heredadas en [!DNL App Builder] aplicaciones. También proporciona asistencia para la reconstrucción de tiendas en Edge Delivery Services (EDS). Al consumir directamente los resultados de la Herramienta de evaluación de la migración, el MCP para desarrolladores de Commerce mantiene la implementación alineada con la hoja de ruta de migración aprobada al reducir la interpretación manual, mantener la trazabilidad y garantizar la coherencia en todo el proceso.

Aunque la migración es el caso de uso principal, Commerce Developer MCP está diseñado como agente de desarrollo de IA completo para [!DNL Adobe Commerce]. El MCP admite modernización, nuevo desarrollo, flujos de trabajo operativos y todas las actualizaciones de [!DNL Adobe Commerce as a Cloud Service]. Este nivel de flexibilidad permite a los equipos seguir creando y ampliando aplicaciones de Commerce mucho después de la migración.

### Commerce Developer MCP

Utilizando los resultados de la [evaluación de la migración](#migration-assessment-tool), el MCP para desarrolladores de Commerce transforma las personalizaciones identificadas en [!DNL App Builder] aplicaciones a través de un flujo de trabajo de desarrollo iterativo. Tenga en cuenta las siguientes directrices al desarrollar con estas herramientas:

- **Empiece con el modelo**: el MCP para desarrolladores de Commerce consume la evaluación de la migración, utilizando sus personalizaciones, recomendaciones y prioridades de migración identificadas como base para la planificación de la implementación.

- **Planificar cada personalización**: para cada personalización, el MCP para desarrolladores de Commerce desarrolla una especificación que describe la arquitectura de [!DNL Adobe Commerce as a Cloud Service] recomendada, los patrones de integración necesarios y cualquier rediseño necesario para la transición a una aplicación fuera de proceso.

- **Generar de forma colaborativa**: en lugar de generar código inicialmente, el MCP para desarrolladores de Commerce le ayuda a lo largo del ciclo de vida de desarrollo mediante la planificación de implementaciones, la descripción de la arquitectura, la generación y el refinamiento del código, la validación de patrones recomendados y la provisión de directrices de implementación. Los desarrolladores pueden refinar de forma iterativa las implementaciones generadas a través del lenguaje natural, lo que permite que los detalles del proyecto evolucionen de forma colaborativa a lo largo del esfuerzo de modernización.

  - Las implementaciones generadas están diseñadas para acelerar la entrega mientras los equipos de ingeniería siguen siendo totalmente revisables, comprobables y ampliables.

- **Integrar e implementar**: el MCP para desarrolladores de Commerce conecta las aplicaciones con Commerce a través de los patrones de integración adecuados, ayuda con los flujos de trabajo de implementación y valida las implementaciones con los patrones de arquitectura recomendados antes de la implementación, lo que mejora la coherencia y reduce el esfuerzo duplicado.

  - El MCP para desarrolladores de Commerce contiene el MCP [!DNL Adobe Commerce App Builder], que proporciona conocimientos de dominio, patrones de implementación, guía de arquitectura, experiencia contextual en productos y prácticas de codificación validadas directamente en el flujo de trabajo de desarrollo. Esto garantiza que las recomendaciones de MCP sigan estando alineadas con las prácticas recomendadas de Adobe, ya sea que los desarrolladores trabajen directamente con el MCP del desarrollador de Commerce o en combinación con otros agentes, como Claude, Cursor o Copilot.

### Modernización de tiendas

En el front-end, el MCP para desarrolladores de Commerce moderniza [tiendas](https://experienceleague.adobe.com/developer/commerce/storefront/) en Edge Delivery Services (EDS) para Commerce mediante la plantilla de Adobe Commerce, los componentes integrados y los bloques EDS.

El MCP para desarrolladores de Commerce carga proyectos de tienda existentes basados en la plantilla de Commerce. Moderniza tu tienda al:

- Generación de bloques EDS interactivos
- Generación de datos de página según Commerce (inicio, PLP, PDP, carro de compras, cierre de compra, cuenta)
- Composición y ampliación de componentes desplegables
- Traducción de diseños en implementaciones de EDS
- Conversión de escaparates monolíticos heredados en una arquitectura de bloques de EDS componible

El MCP también ayuda con:

- Modernización de componentes
- Composición de bloque reutilizable
- Optimización de experiencias
- Alineación con las prácticas recomendadas actuales de Edge Delivery Services

### Valor MCP del desarrollador

Pasar de personalizaciones de PHP en proceso a aplicaciones [!DNL App Builder] componibles representa un cambio de arquitectura significativo. El MCP para desarrolladores de Commerce cierra esa brecha al incrustar el conocimiento de [!DNL Adobe Commerce], los patrones de implementación de [!DNL App Builder] y las prácticas recomendadas de productos directamente en el flujo de trabajo de desarrollo.

La inclusión de este contexto proporciona una mayor coherencia tanto en la velocidad de entrega como en la calidad de la ingeniería. Los equipos pueden modernizar las aplicaciones más rápido a la vez que producen implementaciones que siguen una guía arquitectónica coherente.

Al integrar los patrones de implementación recomendados, el MCP para desarrolladores de Commerce reduce la dependencia en los conocimientos individuales y ayuda a las organizaciones a escalar los esfuerzos de modernización de forma coherente entre los proyectos.

El proceso de migración también ofrece la oportunidad de mejorar la implementación existente. Los equipos pueden simplificar las personalizaciones heredadas, retirar la funcionalidad obsoleta, adoptar las capacidades de SaaS y modernizar la arquitectura de las aplicaciones en lugar de arrastrar la deuda técnica histórica hacia adelante.

Dado que el MCP para desarrolladores de Commerce consume directamente la evaluación de la migración, cada esfuerzo de modernización mantiene la trazabilidad hasta la evaluación original, lo que garantiza que la implementación siga estando alineada con la hoja de ruta de migración aprobada.

El MCP para desarrolladores de Commerce también promueve el diseño de aplicaciones componibles al alentar las aplicaciones modulares [!DNL App Builder] que pueden evolucionar de manera independiente a medida que cambian los requisitos comerciales.

### Ámbito de MCP del desarrollador

En segundo plano, Commerce Developer MCP moderniza el nivel de personalización e integración al transformar módulos PHP, complementos y observadores de eventos en aplicaciones [!DNL App Builder] y establece patrones de integración para conectarlos con Adobe Commerce. También acelera el desarrollo en el proceso de pago y envío, en los pagos y en la IU del administrador.

En el front-end, el MCP para desarrolladores de Commerce [moderniza las tiendas de Commerce](#storefront-modernization) en Edge Delivery Services.

El MCP no gestiona la migración de datos. Los datos profesionales se migran a través del [Servicio de migración de datos de Commerce](#data-migration-commerce-data-migration-service). El MCP admite las aplicaciones [!DNL App Builder] necesarias cuando la lógica empresarial o las tablas personalizadas requieren la modernización de las aplicaciones.

### Pasos siguientes

La modernización de códigos y tiendas comienza una vez que la hoja de ruta de la Herramienta de evaluación de la migración ha establecido el alcance y las prioridades de la migración.

Para obtener más información sobre cómo instalar y usar el MCP, consulte la [documentación de Commerce Developer MCP](https://developer.adobe.com/commerce/extensibility/developer-agent/).

## Migración de datos (servicio de migración de datos de Commerce)

La migración a [!DNL Adobe Commerce as a Cloud Service] requiere migrar años de datos, incluidos catálogos, pedidos, clientes y configuración.

El servicio de migración de datos de Commerce sustituye a la migración manual por un proceso único, repetible y automatizado. Hace que las migraciones de bases de datos complejas sean más predecibles y eficientes.

### Servicio de migración de datos de Commerce

Una migración utiliza un flujo de trabajo guiado, impulsado por una herramienta de línea de comandos Docker (`./bin/console migration`). Un integrador de sistemas u operador ejecuta este flujo de trabajo en el almacén de origen.

La migración de datos principales está automatizada, pero la mayoría de las migraciones implican esquemas, extensiones y casos extremos no estándar, por lo que todas las migraciones comienzan con una [evaluación](#migration-assessment-tool) del almacén de origen. Después de validar las credenciales y la conectividad, registrar la migración y establecer una línea de base de verificación, puede continuar con la migración de datos.

La herramienta de servicio de migración realiza los siguientes pasos de administración de datos:

1. **Extraer y transformar**: extrae todos los datos relevantes del origen en paralelo y cambia su forma para [!DNL Adobe Commerce as a Cloud Service]. Los datos incompatibles se filtran, y los atributos personalizados y otras estructuras se reasignan.
1. **Cargar**: transfiere los datos extraídos al servicio de migración de datos de Commerce. El servicio carga los datos en [!DNL Adobe Commerce as a Cloud Service] y, a continuación, vuelve a compilar los índices e ingiere el catálogo.
1. **Verificar**: compara los datos de origen y destino en el nivel de base de datos. A continuación, el servicio valida una muestra de registros activos a través de las API de REST de administrador y GraphQL de tienda para comprobar los datos.
1. **Informe**: consolida los resultados de cada paso en un informe de migración final.

Estas fases de transferencia de datos requieren un periodo de mantenimiento, pero durante la fase de preparación, la tienda permanece operativa, lo que reduce al mínimo el tiempo de inactividad.

### Valor del servicio de migración

El servicio de migración de datos de Commerce preserva la integridad de los datos mediante el uso de pruebas. Cada migración se verifica comparando los datos de origen y destino y validando una muestra de registros activos a través de las API. Los datos que no se asignan claramente a [!DNL Adobe Commerce as a Cloud Service], como los atributos personalizados, se filtran y se vuelven a asignar automáticamente durante la extracción.

El servicio de migración está diseñado para bases de datos a escala empresarial. La migración de datos se divide y procesa de forma asíncrona, lo que permite migrar catálogos grandes y extensos historiales de pedidos de forma fiable. Varias migraciones se pueden ejecutar en paralelo a medida que la canalización crece. Si se interrumpe una migración, se reanuda desde la última fase completada y los trabajos paralizados se detectan y se vuelven a intentar automáticamente.

El tiempo de inactividad se minimiza de las siguientes maneras:

- La mayor parte del trabajo se realiza mientras la tienda permanece activa, lo que significa que solo el corte final requiere una ventana de mantenimiento.
- La migración de datos utiliza SQL directo y altamente eficaz que lee y escribe y omite tablas y registros que no necesitan migrarse.

Dado que las migraciones implican que los datos de producción se muevan a través de la infraestructura de Adobe, toda la ruta está segura:

- Todas las cargas se analizan en busca de malware antes de llegar al destino
- La capa de entrada valida los tipos de archivo y bloquea las operaciones de base de datos no seguras
- Cada solicitud se autentica mediante Adobe IMS y la verificación de firma de puerta de enlace

El servicio de migración de datos de Commerce está activo en todo el mundo y ya ha realizado varias migraciones empresariales.

### Datos personalizados y de terceros

El servicio de migración solo admite datos de comercio principales de origen. El servicio de migración no gestiona entidades personalizadas de terceros.

Los datos de terceros se pueden migrar por caso, lo que requiere una personalización correspondiente de la herramienta de extracción Docker. Después de crear las herramientas personalizadas, los datos se pueden extraer del origen y escribirse en la base de datos de [!DNL App Builder] o de terceros.

Dado que cada extensión modela sus datos de forma diferente, solo se puede diseñar una ruta de migración para los datos de terceros después de determinar el esquema y las ubicaciones del almacenamiento de origen y destino. Las migraciones de datos de terceros deben identificarse antes de tiempo para dar tiempo a la creación de ámbitos.

### Pasos siguientes

Cuando esté listo para la migración, complete el [cuestionario de ámbito de migración de datos](../assets/data-migration-scoping-questionnaire.xlsx), que requiere la topología de origen, el ámbito de entidad, los volúmenes, las restricciones de conformidad, la mecánica de migración y cualquier [tabla personalizada](#custom-and-third-party-data) necesaria para planificar la migración. Completar este cuestionario permite a Adobe evaluar su entorno y planificar una ventana de migración.

Revise la documentación de la [Guía de la herramienta de migración masiva de datos](bulk-data/migration-tool.md) para obtener más información sobre el flujo de trabajo, los datos compatibles y la verificación.

Los integradores de sistemas que preparen un entorno de origen también pueden utilizar la [CLI de Adobe Commerce Cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview) y la [Adobe Developer Console](https://developer.adobe.com) para las credenciales de IMS.
