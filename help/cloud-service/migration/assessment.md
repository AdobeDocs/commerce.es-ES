---
title: Evaluación de migración
description: Obtenga información sobre cómo leer un informe de evaluación de migración de Adobe Commerce PaaS, interpretar las señales de complejidad de tienda y back-end, y utilizar las herramientas para desarrolladores de Adobe AI para empezar a crear extensiones para Adobe Commerce as a Cloud Service.
feature: Cloud, Migration
role: Developer, Admin
level: Intermediate
TQID: 'https://experienceleague.adobe.com/-OrsBVtHRcEV5EzgHzzP0JVf0aQWfSO2Fu1R5F5jtAw'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: c32adafa-ed01-4b31-997e-2413013911b0id: cc250cf1-34eb-4863-80d0-d170d45ea067id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: fcbf661a05f5d7ff33a885e3f86dbb3a551d09df
workflow-type: tm+mt
source-wordcount: 2505
ht-degree: 0%

---


# Evaluación de migración

>[!IMPORTANT]
>
> La evaluación de migración solo está disponible cuando se migran [!DNL Adobe Commerce on Cloud Infrastructure] o [!DNL Adobe Commerce on-premises] proyectos a [!DNL Adobe Commerce as a Cloud Service].

Una evaluación de la migración de Commerce es un análisis automatizado de la implementación de Adobe Commerce existente. Las herramientas de Adobe analizan el código base de Commerce y generan un informe estructurado que crea un inventario de todo lo creado, personalizado o modificado. A continuación, el informe indica cómo afectan las personalizaciones realizadas en la base de código a la migración a [!DNL Adobe Commerce as a Cloud Service].

El informe se entrega como un archivo HTML que se puede abrir con cualquier explorador. No se requiere acceso al entorno de producción, excepto que inicialmente se compartió el código base del proyecto.

>[!TIP]
>
>Póngase en contacto con el administrador de cuentas de su solución para solicitar una evaluación de migración de su instancia existente.

**La evaluación proporciona:**

- Un inventario completo de cada módulo personalizado de su tienda, organizado por tipo y nivel de impacto
- Una clasificación de complejidad de la migración (alta, Medium o baja) calculada a partir de métricas predictivas de riesgo
- Una vista priorizada de las áreas de servidor y tienda de mayor impacto que requieren planificación de la migración
- Una descripción de cada módulo personalizado, que puede utilizar como entrada directa para las herramientas para desarrolladores de IA de Adobe

## Comprender el informe de evaluación de migración

El informe está organizado en tres fichas: **[!UICONTROL Summary]**, **[!UICONTROL Module Reports]** y **[!UICONTROL Report Reliability]**.

>[!NOTE]
>
>No todas las secciones del informe se aplican a todos los almacenes. La evaluación está diseñada para ser exhaustiva en todos los tipos de personalización y controladores de complejidad posibles, pero su tienda solo tiene un subconjunto de las secciones que se enumeran aquí.

## Pestaña Resumen

La ficha **[!UICONTROL Summary]** proporciona una descripción general de las señales clave organizadas en estas áreas:

- Complejidad de migración
- Desglose de tipo de archivo
- Módulos de mayor impacto
- Controladores de migración
- Desglose de personalización

### Complejidad de migración

La sección Complejidad de la migración contiene la clasificación de evaluación de la tienda en general. Explica cómo se calculó la puntuación y resalta los factores de riesgo principales.

**Puntuación de complejidad y complejidad de la migración**

![Sección de complejidad de la migración que muestra la puntuación ponderada, los controladores de riesgo principales y las métricas clave](../assets/assessment-migration-complexity.png){width="600" zoomable="yes"}

La puntuación de complejidad pondera cada entrada según lo difícil que sea migrar. La puntuación se asigna a una clasificación de complejidad de la migración mediante umbrales fijos:

| Clasificación | Intervalo de puntuación | Enfoque de migración habitual |
| --- | --- | --- |
| Baja | 150 o menos | Migración estándar: migración directa con coordinación de proveedores de pagos y migración de datos como flujos de trabajo paralelos. |
| Medium | 151 - 375 | Migración modular: se migra en segmentos mediante la prueba de módulos personalizados de alto impacto. |
| Alta | Por encima de 375 | Una migración por fases, que probablemente dure entre 12 y 24 meses. |

**Proporción de módulo personalizado**

![Fila de métricas de proporción de módulos personalizados que muestra porcentaje de módulos personalizados, módulos de terceros, recuento de temas personalizados, enlaces críticos, archivos totales y tamaño de base de código PHP](../assets/assessment-custom-module-ratio.png){width="600" zoomable="yes"}

El porcentaje de los módulos creados específicamente para su implementación. Una proporción mayor significa que se debe auditar y migrar más código personalizado. La proporción de módulos personalizados del cliente promedio es de aproximadamente el 62 %.

>[!TIP]
>
>La proporción de módulos personalizados es una señal de ámbito, no de complejidad. Una tienda con módulos personalizados al 80 % aislados y de bajo riesgo podría ser más fácil de migrar que una tienda con módulos personalizados con un 40 % de riesgo más alto. Utilice la puntuación de complejidad y el número de conflictos en cadena para evaluar la dificultad. Utilice la proporción de módulos personalizados para calcular el volumen.

**Desglose de tipo de archivo**

![Tabla de desglose de tipos de archivos que enumera las extensiones de archivo con recuentos de archivos y líneas de código](../assets/assessment-file-type-breakdown.png){width="600" zoomable="yes"}

Una lista del número de archivos de la base de código, organizados por tipo.

**Módulos de mayor impacto**

![Lista de módulos de mayor impacto que muestra nombres de módulos, descripciones, clasificaciones de impacto y recuentos de ganchos](../assets/assessment-highest-impact-modules.png){width="600" zoomable="yes"}

Una lista revisada de los módulos específicos de su tienda que requieren la mayor atención de la migración. Estos módulos suelen ser módulos que interactúan con el cierre de compra, los pagos o la gestión de pedidos. Cada módulo de alto impacto necesita su propio plan de migración. Esta lista es el mejor punto de partida para las conversaciones con su equipo técnico.

### Complejidad de tienda

![Sección Complejidad de la tienda que muestra áreas de nombres de temas personalizados, recuento total de bloques, archivos XML de diseño, invalidaciones de controladores principales y señales procesables](../assets/assessment-storefront-complexity.png){width="600" zoomable="yes"}

La sección Complejidad de la tienda presenta el esfuerzo necesario para migrar la capa de presentación del front-end de la tienda. Este flujo de trabajo es distinto al de la migración de código back-end, y lo suelen abordar los desarrolladores de front-end, que suelen requerir conversaciones de planificación independientes.

>[!NOTE]
>
>Una tienda puede tener una complejidad de back-end baja y una complejidad de tienda alta. Revise siempre ambas secciones antes de enfocar el esfuerzo de migración.

- Temática personalizada: el área de nombres de la temática personalizada de la tienda (por ejemplo, BrandName_Theme). La presencia de una temática personalizada significa que se requiere una reconstrucción completa de la temática para [!DNL Adobe Commerce as a Cloud Service]. Cada tienda evaluada con un área de nombres de tema personalizada debe planificar un flujo de trabajo de migración front-end dedicado.

- Bloques totales: el número de archivos de bloque y plantilla (.phtml) del almacén. Los bloques son los artefactos de procesamiento principales del lado del servidor, cada uno de los cuales representa una tarea de migración discreta.

| Recuento de bloqueados | Esforzar |
| --- | --- |
| Menos de 100 | Línea de base: esfuerzo estándar |
| 100-300 | Medium: planificar una ola de front-end estructurada |
| Más de 300 | Alto: dé prioridad como flujo de trabajo dedicado |

### Controladores de migración

![Sección de controladores de migración que muestra la huella de personalización, los complementos y observadores y las tarjetas de preferencias de clase con clasificaciones de esfuerzo](../assets/assessment-migration-drivers.png){width="600" zoomable="yes"}

La sección Controladores de migración muestra los principales factores que determinan la clasificación de complejidad.

| Controlador | Definición |
| --- | --- |
| Huella de personalización | El volumen total de código personalizado en relación con la implementación total. |
| Complementos y observadores | Código que intercepta el comportamiento de la plataforma principal durante la ejecución |
| Preferencias de clase | Un frágil patrón de personalización, que reemplaza las clases principales por completo y se interrumpe silenciosamente al actualizar |
| Modelo de datos | Estructuras de base de datos personalizadas y modificadas |
| Integraciones | Sistemas externos conectados a su tienda |

Cada controlador aparece con un esfuerzo Alto, Medium o Bajo. Aborde primero los controladores de mayor clasificación al definir ámbitos y planear.

### Modelo de datos

![Sección del modelo de datos que muestra recuentos de tablas personalizadas, modificaciones de tablas principales y atributos EAV críticos](../assets/assessment-data-model.png){width="600" zoomable="yes"}

La sección Modelo de datos muestra un recuento de tablas personalizadas, modificaciones en las tablas de la base de datos principal [!DNL Adobe Commerce] y atributos críticos Entity-Attribute-Value (EAV).

Las modificaciones de la tabla principal son la categoría más difícil de migrar, ya que crean dependencias en una versión de esquema de plataforma específica y tienen un alto impacto en la fórmula de puntuación de complejidad.

>[!TIP]
>
>Si el informe enumera más de 15 modificaciones de tablas principales, planifique un flujo de trabajo de migración de datos dedicado antes de abordar la migración de módulos back-end.

## Desglose por personalización

![Desglose de personalización que enumera todas las categorías de personalización con recuentos e indicadores de impacto](../assets/assessment-customization-breakdown.png){width="600" zoomable="yes"}

La sección Desglose de personalización proporciona métricas detalladas en todas las categorías de personalización de la tienda.

>[!NOTE]
>
>No todas las subsecciones aparecen en todos los informes, solo se muestran las categorías detectadas en la base de código.
>
>Las subsecciones que afectan a la capa de presentación del front-end son un flujo de trabajo distinto de la migración de código back-end y normalmente requieren conversaciones de planificación independientes.
>
>Una tienda puede tener una complejidad back-end baja y una complejidad front-end alta. Revise siempre las subsecciones relacionadas con el servidor y la tienda antes de enfocar el esfuerzo de migración.

### XML de diseño

Número de archivos XML de diseño y recuento total de operaciones. Diseño XML define la estructura de cada página, incluidos los bloques que aparecen, los contenedores en los que aparecen y los tipos de página en los que se encuentran.

Un recuento alto de archivos con muchas operaciones indica una personalización significativa de la estructura de la página que debe rediseñarse.

### Invalidaciones del identificador principal

Número de lugares en los que el XML de diseño anula un identificador de página principal [!DNL Adobe Commerce] (por ejemplo, `checkout_cart_index` o `catalog_product_view`). Las invalidaciones de controladores principales son la señal de diseño de mayor riesgo porque modifican la estructura de la página en el nivel de plataforma y requieren una reconstrucción explícita.

| Anular recuento | Esforzar |
| --- | --- |
| 0 | Sin invalidaciones de diseño principal |
| 1-3 | Riesgo de tiempo de ejecución: cada anulación necesita una reconstrucción explícita del diseño |
| 4 o más | Esencial: plan para un ciclo de migración de diseño dedicado |

### Bloques

Número de archivos de bloque y plantilla (`.phtml`) del almacén. Los bloques son los artefactos de procesamiento principales del lado del servidor. Cada bloque representa una tarea de migración discreta.

| Recuento de bloqueados | Esforzar |
| --- | --- |
| Menos de 100 | Línea de base: esfuerzo estándar |
| 100-300 | Medium: planificar una ola de front-end estructurada |
| Más de 300 | Alto: dé prioridad como flujo de trabajo dedicado |

### Bloques de alto riesgo

Bloques que tocan las rutas de procesamiento principales, como la representación de cierre de compra, la visualización del carro de compras y superficies front-end similares. Cualquier bloque de alto riesgo requiere una evaluación de la migración individual antes de programarlo.

### Temáticas y plantillas de correo electrónico

Área de nombres de la temática personalizada de la tienda (por ejemplo, `BrandName_Theme`). La presencia de una temática personalizada significa que se requiere una reconstrucción completa de la temática. Cada tienda evaluada con un área de nombres de tema personalizada debe planificar un flujo de trabajo de migración front-end dedicado.

### Anulaciones de plantilla (modificación del núcleo)

Número de plantillas principales [!DNL Adobe Commerce] `.phtml` que se han anulado. Cada anulación de la plantilla principal crea una dependencia en una versión específica de esa plantilla. Las actualizaciones de la plataforma que cambian la plantilla rompen la anulación de forma silenciosa.

### Migración de destino requerida

[!DNL Adobe Commerce as a Cloud Service] utiliza una arquitectura de componentes modular desplegable para superficies de tienda, incluidos detalles de cierre de compra, carro de compras y producto. Las personalizaciones de estas superficies deben reconstruirse como componentes desplegables. Estas personalizaciones pueden cubrir una amplia gama de funcionalidades, como agregar pasos de cierre de compra personalizados, modificar la lógica de visualización del carro de compras o ampliar la página de detalles del producto.

El campo [!UICONTROL Drop-in migration required] indica qué áreas de tienda requieren reconstrucciones desplegables.

>[!IMPORTANT]
>
>Si **Cierre de compra** aparece como un requisito de migración de elementos integrados, planifique un flujo de trabajo de elementos desplegables de cierre de compra dedicado. Esta tarea es la tarea de migración de tiendas más compleja y crítica para la empresa.

## Pestaña Informes del módulo

![Pestaña Informes de módulo que muestra una lista de módulos en los que se puede buscar con filtros de impacto y panel detallado de análisis de módulos](../assets/assessment-module-reports-tab.png){width="600" zoomable="yes"}

La ficha **[!UICONTROL Module Reports]** contiene una entrada dedicada para cada módulo personalizado de su tienda. Comparta esta información con su equipo técnico.

El informe muestra lo siguiente para cada módulo:

| Nombre de campo | Definición |
| --- | --- |
| Qué hace | Descripción del propósito y la función empresarial del módulo personalizado |
| Nivel de impacto | Impacto de **alto**, **Medium** o **bajo** basado en el comportamiento comercial que toca el módulo |
| Recuento de ganchos | El número de webhooks, que indica cuántos lugares intercepta este módulo el comportamiento de la plataforma principal |
| Recomendación de migración | **Reconstruir**, **Refactorizar**, **Reemplazar** con una característica nativa o **Quitar** |
| Dependencias | Con qué otros módulos interactúa este módulo, lo que puede informar la secuencia de migración |

**Flujo de trabajo**

1. Filtre primero a **módulos de alto impacto**. Estos son los factores que generan la mayor cantidad de esfuerzo y costes de migración.
1. Para cada módulo personalizado, determine las respuestas a las siguientes preguntas:
   - ¿Este módulo sigue utilizándose de forma activa?
   - ¿Podría reemplazarse el módulo por una característica [!DNL Adobe Commerce as a Cloud Service] nativa?
   - Si es necesario reconstruir el módulo, ¿qué funcionalidad debe proporcionar su reemplazo?
1. Identifique los módulos personalizados que se pueden retirar o reemplazar. Cada una reduce el ámbito de migración antes de que se escriba cualquier código.
1. Copie la descripción de cada módulo personalizado con la recomendación de migración **Reconstruir**. Estas descripciones se pueden proporcionar directamente a las herramientas para desarrolladores de IA de Adobe. Consulte [Herramientas para desarrolladores de IA para la extensibilidad de Commerce](#ai-developer-tools-for-commerce-extensibility) para obtener más información.

## Referencia: términos clave

| Término | Definición |
| --- | --- |
| **Módulo** | Un paquete de funciones personalizado e independiente. Su tienda podría tener entre veinte módulos y cientos de módulos. |
| **Complemento (interceptor)** | Código que intercepta una función de Commerce y cambia su comportamiento antes, durante o después de ejecutarse. |
| **Observador** | Código que escucha un evento de plataforma específico, como &quot;pedido realizado&quot;, y ejecuta lógica personalizada cuando se activa ese evento. |
| **Preferencia (anulación de clase)** | Un tipo de personalización frágil que reemplaza completamente a una clase Commerce principal, que se interrumpe silenciosamente cuando la plataforma actualiza esa clase. |
| **Conflicto de cadenas** | Cuando dos o más complementos interceptan la misma función y uno no pasa el control al siguiente. Esto puede hacer que las funciones dejen de funcionar de forma silenciosa y no aparezcan mensajes de error. |
| **Modificación de tabla principal** | Un cambio estructural en las tablas de base de datos integradas de Commerce, que crea una dependencia irreversible en una versión de esquema de plataforma específica. Estos llevan el peso más alto en la fórmula de Puntuación de complejidad. |
| **Valor de atributo de entidad (EAV)** | Campo personalizado flexible añadido a productos o clientes como, por ejemplo, un campo personalizado de &quot;periodo de garantía&quot;. Los altos recuentos de EAV aumentan la complejidad de la migración de datos. |
| **Densidad del gancho** | Número promedio de complementos y observadores por módulo. Una mayor densidad significa que la personalización está más estrechamente vinculada a la plataforma principal. |
| **Inclusión** | [!DNL Adobe Commerce's] enfoque modular para los componentes de la tienda (incluidas las páginas de cierre de compra, el carro de compras y los detalles del producto). El comportamiento de cierre de compra personalizado en [!DNL Adobe Commerce on Cloud Infrastructure] o [!DNL Adobe Commerce on Premises] suele requerir una reconstrucción de inclusión en [!DNL Adobe Commerce as a Cloud Service]. |
| **App Builder** | La plataforma de extensibilidad fuera de proceso de Adobe y la forma recomendada de crear funcionalidades personalizadas, reemplazando las extensiones PHP en proceso. |
| **XML de diseño** | Archivos de configuración que definen qué bloques aparecen en qué páginas. El XML de diseño personalizado debe rediseñarse para la estructura de página [!DNL Adobe Commerce as a Cloud Service's]. |
| **Anulación de identificador principal** | Una personalización XML de diseño que modifica globalmente una estructura de páginas principal de Commerce. Tienen el patrón de diseño de mayor riesgo para la migración. |

## Herramientas para desarrolladores de IA para la extensibilidad de Commerce

Puede utilizar las descripciones de los módulos de la ficha **[!UICONTROL Module Reports]** como mensajes para las herramientas para desarrolladores de IA de Adobe. La herramienta le ayudará a generar e implementar una extensión de reemplazo compatible con [!DNL Adobe Commerce as a Cloud Service].

### Qué proporcionan las herramientas

Las [herramientas para desarrolladores de IA de Adobe para la extensibilidad de Commerce](https://developer.adobe.com/commerce/extensibility/developer-agent/) incluyen dos funcionalidades principales.

- Servidor MCP [!DNL Adobe Commerce] [!DNL App Builder]: una integración de protocolo de contexto de modelo (MCP) que conecta asistentes de codificación de IA directamente a [!DNL Adobe Commerce] documentación, API y patrones de desarrollo de App Builder. Los desarrolladores pueden describir lo que desean generar y el servidor MCP proporciona generación de código compatible con Commerce, orientación de arquitectura y automatización de la implementación dentro del IDE.
- Aptitudes del agente: habilidades de IA creadas previamente que abarcan patrones de extensibilidad comunes de Commerce, como API de REST, extensiones de cierre de compra, componentes de tienda e integraciones impulsadas por eventos. Las habilidades guían la IA a través de los pasos de arquitectura, implementación, pruebas e implementación específicos de [!DNL Adobe Commerce as a Cloud Service] y [!DNL App Builder].

#### Instalación de herramientas de IA

Consulte [instalar las herramientas para desarrolladores de IA](https://developer.adobe.com/commerce/extensibility/developer-agent/coding-tools) para obtener instrucciones completas y configuraciones específicas del IDE.

**Requisitos previos:** Node.js 22.x, npm 9.0.0 o superior, CLI de Adobe I/O.

Instalar, comando:

```bash
aio commerce extensibility tools-setup
```

### Crear indicadores a partir del informe de evaluación

Aunque la evaluación le ofrece un modelo para el desarrollo, las herramientas de IA permiten a su equipo empezar a crear de inmediato, antes de que se finalice un plan de migración completo.

1. Abra la ficha **[!UICONTROL Module Reports]** y busque un módulo de alto impacto con una recomendación **Reconstruir**.
1. Lea la descripción del módulo, por ejemplo:

```shell-session
Manages custom shipping rate calculations based on customer account tier and order    weight thresholds.
```

1. Abra el IDE, por ejemplo, Copiloto, Cursor o Claude de GitHub, con el servidor MCP de extensibilidad de Commerce habilitado.
1. Utilice la descripción del módulo para preguntar al agente de IA.
1. Revise la aplicación [!DNL App Builder] con andamiaje e itere con el agente para restringir la implementación.

## Pasos siguientes

1. Abra la ficha **[!UICONTROL Summary]**. Revise los módulos Complejidad de la migración y Mayor impacto y, a continuación, consulte las subsecciones Desglose de personalización. Si su tienda tiene una temática personalizada, bloques de alto riesgo o una lista de abandonos de cierre de compra, planifique un flujo de trabajo front-end paralelo junto con la migración back-end.
1. Comparta la ficha **[!UICONTROL Module Reports]** con su equipo técnico o socio de desarrollo. Pídale que marque los módulos personalizados que ya no se usan de forma activa o que podrían reemplazarse con la característica [!DNL Adobe Commerce as a Cloud Service].
1. Comience a crear sus personalizaciones. Utilice las descripciones de los módulos como entrada de la herramienta de IA para comenzar a andamiar extensiones compatibles.
1. Programe una llamada de tutorial con el equipo de la cuenta de Adobe. Adobe puede revisar los resultados con usted, responder a cualquier pregunta sobre módulos específicos y señales de tienda, y ayudarle a asignar el enfoque de migración a su perfil de complejidad.

## Recursos

- [!DNL Adobe Commerce as a Cloud Service]
   - [Información general](../overview.md)
   - [Resumen de migración](./overview.md)
   - [Tutorial de extensión de clasificaciones](../tutorials/ratings-extension.md)
   - [Tutorial del método de envío](../tutorials/shipping-method-extension.md)
- Extensibilidad
   - [Información general](https://developer.adobe.com/commerce/extensibility/)
   - [Herramientas para desarrolladores de IA](https://developer.adobe.com/commerce/extensibility/developer-agent/)
      - [Prácticas recomendadas](https://developer.adobe.com/commerce/extensibility/developer-agent/best-practices)
      - [Configurar](https://developer.adobe.com/commerce/extensibility/developer-agent/coding-tools)
      - [Aptitudes e indicaciones](https://developer.adobe.com/commerce/extensibility/developer-agent/skills-and-prompts)
      - [Casos de uso](https://developer.adobe.com/commerce/extensibility/developer-agent/use-cases)
   - [Información general de App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/)
   - [App Builder para Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/introduction-to-app-builder)
   - Starter kits
      - [Kit de inicio de integración back-end](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/)
      - [Kit de inicio de compra](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/)
- Desarrollo de tiendas
   - [Información general](https://experienceleague.adobe.com/developer/commerce/storefront/)
   - [Aptitudes de Storefront AI](https://experienceleague.adobe.com/developer/commerce/storefront/boilerplate/ai-agent-skills/)
