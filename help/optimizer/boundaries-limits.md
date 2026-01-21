---
title: Límites y límites
description: Comprenda [!DNL Adobe Commerce Optimizer] los límites y limitaciones para planificar la capacidad y evitar problemas de rendimiento.
role: Admin, Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
source-git-commit: 4f238b002d1481126d4fec0a249b7f9ff437248e
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# Límites y límites

[!DNL Adobe Commerce Optimizer] tiene dos tipos de límites:

- **Límites de licencias**: según la capacidad que haya adquirido; se puede ampliar comprando paquetes adicionales.
- **Límites del sistema**: límites fijos que protegen los recursos del sistema y garantizan un rendimiento confiable para todos los usuarios.

Su uso debe permanecer dentro de estos límites. Excederlos puede causar un aumento de la latencia y la limitación de solicitudes.

## Solicitar capacidad adicional

Los límites de licencia se pueden aumentar comprando los paquetes de licencia descritos en la sección [Límites de licencia y límites del sistema](#license-limits-and-system-boundaries), o negociando licencias personalizadas para casos de uso únicos. Póngase en contacto con su representante de cuentas de Adobe para hablar sobre sus necesidades.

Si tiene alguna pregunta sobre los límites del sistema, comuníquese con la [atención al cliente de Adobe](https://experienceleague.adobe.com/home?lang=es#support).

## Evitar problemas de rendimiento

Siga estas prácticas recomendadas para mantenerse dentro de los límites y evitar problemas operativos:

- **Revisa tus límites**: comprende tus [límites de capacidad](#license-limits-and-system-boundaries) antes de lanzar nuevas tiendas o campañas.
- **Rastree su uso**: use paneles de métricas integrados o registros de CDN.

## Límites de licencias y límites del sistema

En las tablas siguientes se resumen los límites de licencia y de sistema por área de capacidad e incluyen información sobre cómo agregar licencias adicionales para ampliar la capacidad cuando corresponda.

### Límites del entorno

| **Entorno** | **Descripción** | **Asignación base** | **Ampliable?** |
| --- | --- | --- | --- |
| **Entorno de espacio aislado** | El número de entornos de zona protegida incluidos | 2 por instancia | Sí<p>Añadir una licencia de entorno adicional por instancia</p> |
| **Entorno de producción** | El número de entornos de producción incluidos | 1 por instancia | Licencia<p>Añadir una licencia de entorno adicional por instancia</p> |

{style="table-layout:auto"}

### Catálogo

| **Capacidad** | **Descripción** | **Asignación base** | **Ampliable?** |
| --- | --- | --- | --- |
| Tasa de ingesta de productos | El número de productos creados o actualizados | 1K actualizaciones por minuto<p>Un máximo de 100 000 actualizaciones al día</p> | Sí<p>Agregar un paquete de licencias:</p><ul><li>Actualizaciones de 5K por minuto<br>Un máximo de 500K actualizaciones por día</li> <li>10 000 actualizaciones por minuto<br>Un máximo de 1 millón de actualizaciones por día</li></ul><p>La capacidad máxima de ingesta de datos es de 1 millón de actualizaciones al día.</p> |
| Tamaño de carga útil del producto | Cantidad máxima de datos permitida al crear, actualizar o ingerir información de producto mediante la API | 200 KB | No |
| Variaciones de catálogo | El número de vistas de un catálogo disponibles para los usuarios de tienda,<p>que se cuentan como (*Número de vistas del catálogo × Número de libros de precios*)</p> | 100 variaciones | Sí<p>Agregar paquete de licencias de 100 variaciones de catálogo</p> |
| Productos en un único origen de catálogo | SKU admitidas en el catálogo | SKU de 250.000 | Sí<p>Añadir paquete de licencias de SKU a 100.000</p> |
| Variantes por producto | Número de variantes de producto (tamaño, combinaciones de colores) permitidas por producto | 10K | No |
| Fuentes de catálogo | El número de contextos de datos de catálogo (por ejemplo, configuraciones regionales o fuentes de datos como PIM y ERP) | 50 | No |

{style="table-layout:auto"}

### Libros de precios

| **Capacidad** | **Descripción** | **Asignación base** | **Ampliable?** |
| --- | --- | --- | --- |
| Libros de precios | Número de libros de precios permitidos por instancia | Según la cantidad de [variaciones de catálogo](#catalog) | Sí<br>Aumentar las variaciones del catálogo |
| Descuentos por registro de precios | El número de descuentos que se pueden aplicar a un precio de producto dentro de un único libro de precios | 10 | No |

{style="table-layout:auto"}

### Imágenes de productos con tecnología de AEM Assets

| **Capacidad** | **Descripción** | **Asignación base** | **Ampliable?** |
| --- | --- | --- | --- |
| Imágenes del producto Usuarios avanzados | Usuario con licencia con funciones completas de administración de recursos digitales, incluidas herramientas de IA, integraciones de Adobe Express/Firefly y uso compartido de Content Hub, que gestiona tareas principales de DAM y funciones avanzadas nativas de la nube para una eficacia óptima. | 2 | Sí<p>Actualizar a licencia de AEM Assets</p> |
| Visuales del producto Usuarios de Collaborator | Acceda a los recursos y trabaje con ellos a través de la integración de Commerce de AEM, cree y edite contenido mediante Adobe Express y Firefly y, si está activada, aproveche los recursos aprobados a través del portal de Content Hub. | 2 | Sí<p>Actualizar a licencia de AEM Assets</p> |
| Almacenamiento de imágenes del producto | Espacio de almacenamiento asignado para recursos | Almacenamiento de 1 TB | No |
| Uso de Dynamic Media | Asignación para operaciones de procesamiento de medios dinámicos, que incluye:<ul><li>Entrega de imágenes</li><li>Imágenes inteligentes</li><li>Entrega de vídeo</li></ul><p>Para obtener más información, consulte *Calcular el uso de Dynamic Media* a continuación. | Basado en GMV<p>Asignación mínima: 5M operaciones/mes</p> | Sí<ul><li>Licencia de compra para operaciones adicionales</li><li>Actualizar a licencia de AEM Assets</li></ul> |
| Entrega de vídeo | Asignación para descargas o envíos de vídeo | 300 vídeos, 1 minuto por vídeo | Sí<p>Actualizar a licencia de AEM Assets</p> |
| Generación de recursos | Acceso a la IA generativa de Adobe Express y Adobe Firefly para crear imágenes | Ninguno | Compre créditos de IA generativos por separado |

{style="table-layout:auto"}


>[!NOTE]
>
>**Usuarios avanzados** pueden acceder a Adobe Express directamente o desde Adobe Commerce Optimizer. **Los usuarios de Collaborator** pueden acceder directamente a la aplicación de Adobe Express. El uso está regido por [Adobe Express con términos de licencia específicos de productos Firefly](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf).


>[!BEGINSHADEBOX &quot;Calcular uso de Dynamic Media&quot;]

El uso de Dynamic Media realiza un seguimiento de las solicitudes de API que llegan a los componentes Visuales del producto en Adobe Commerce Optimizer para facilitar una de las siguientes acciones:

- **La entrega de imágenes consume una operación de medios dinámicos** por cada ocurrencia de lo siguiente:
   - **transformación básica de la imagen** de un recurso digital; por ejemplo, operaciones de cambio de tamaño, escala, conversión de formato, compresión o recorte.
   - **entrega o descarga de imagen estática** de dichos recursos digitales o representación de recursos digitales (que no sean vídeos)
- **La entrega de imágenes inteligentes consume 20 operaciones de Dynamic Media** para cada entrega optimizada de un único recurso digital al generar automáticamente la representación de imágenes más adecuada para el dispositivo y el explorador del usuario final.
- **La entrega de vídeo consume 20 operaciones de Dynamic Media** para una sola entrega o descarga de un vídeo o una variante transformada de un vídeo.

>[!ENDSHADEBOX]


### Vistas de catálogo y políticas

| **Capacidad** | **Descripción** | **Asignación base** | **Ampliable?** |
| --- | --- | --- | --- |
| Vistas de catálogo | Número de subconjuntos configurables del catálogo maestro | Según la cantidad de [variaciones de catálogo](#catalog) | Sí<br>Aumentar las variaciones del catálogo |
| Políticas por vista de catálogo | Número de filtros de datos permitidos | 10 | No |
| Valores de atributo en una directiva | Número de características del producto que se pueden configurar para el filtrado | 100 | No |

{style="table-layout:auto"}

### Tienda de catálogo

La asignación base para las capacidades de la tienda del catálogo se determina en función del nivel de GMV. La tabla indica la asignación mínima para cada capacidad.

| **Capacidad** | **Descripción** | **Asignación base** | **Ampliable?** |
| --- | --- | --- | --- |
| Tasa de recuperación del catálogo | Número de veces que un sistema (tienda, sistema de transacciones, ERP u otro) llama mensualmente a una API de catálogo para recuperar datos del catálogo | Basado en el nivel de GMV<p>Asignación mínima: 10M/mes</p> | Sí<p>Agregar un millón de solicitudes al mes en paquetes de licencias</p> |
| Solicitudes de contenido | Solicitudes a Commerce Storefront para vistas de página de HTML o llamadas a la API JSON. Se cuenta como 1 vista de página o 5 llamadas a la API. | Basado en el nivel de GMV<p>Asignación mínima: 2M/mes</p> | Sí<p>Añadir un paquete de licencias de 1 millón al mes</p> |
| Variaciones GenAI de Storefront | Asignación para la generación de contenido basado en texto | Basado en el nivel de GMV<p>Asignación mínima: 1K variaciones/mes</p> | Sí<p>Compre créditos de IA generativos por separado</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>La generación de imágenes requiere una licencia de Adobe Firefly aprovisionada para la misma organización de IMS que Adobe Commerce Optimizer.


### Descubrimiento de productos

| **Capacidad** | **Descripción** | **Asignación base** | **Ampliable?** |
| --- | --- | --- | --- |
| Productos por solicitud de búsqueda | Número máximo de productos devueltos por página en los resultados de búsqueda | 100 | No |
| Atributos filtrables | El número de características del producto (como color, tamaño, marca o material) que se pueden habilitar para la navegación por capas y las facetas | 200 | No |
| Atributos de búsqueda | El número de características de producto que se pueden configurar para usarlas con el servicio de búsqueda del catálogo de productos | 200 | No |
| Atributos ordenables | El número de características del producto que se pueden configurar para determinar el orden de los valores de resultados de búsqueda | 50 | No |
| Profundidad de paginación de búsqueda | Número máximo de productos accesibles a través de la paginación (por ejemplo, página 100 × 100 productos/página) | 10K | No |
| Facetas | El número de atributos de producto filtrables (como marca, color, tamaño y precio) que se pueden configurar para ayudar a los compradores a refinar los resultados de búsqueda y examinar las categorías | 100<p>Deben ser atributos filtrables</p> | No |
| Opciones por faceta | El número de valores de atributos de producto filtrables (como &quot;Rojo&quot;, &quot;Azul&quot; para Color; &quot;Pequeño&quot; o &quot;Medium&quot; para Tamaño) que los compradores pueden seleccionar de una lista | 100 | Sí<p>Puede aumentar mediante una solicitud de asistencia</p> |

{style="table-layout:auto"}

### Recommendations

Las siguientes funciones están disponibles para recomendaciones de productos. Algunas características disponibles en otros productos de Adobe Commerce no son compatibles con [!DNL Adobe Commerce Optimizer].

| **Capacidad** | **Descripción** | **Asignación base** | **Ampliable?** |
| --- | --- | --- | --- |
| Unidades de recomendación activas | Número de componentes de recomendaciones activas en la tienda (como &quot;Los clientes también vieron&quot; o &quot;Es posible que también te guste&quot;) | 50 | No |
| Inclusiones/exclusiones de categorías o atributos | Filtre los productos a un conjunto específico que cumpla los requisitos para las recomendaciones | No compatible | |

{style="table-layout:auto"}

### Extensibilidad

| **Capacidad** | **Descripción** | **Asignación base** | **Ampliable?** | **Notas** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | Capacidad para crear integraciones y extensiones nativas de la nube | Basado en el nivel de GMV<p>Asignación mínima: 1 paquete/año</p> | Sí<p>Adición de paquetes adicionales</p> | Para los límites definidos por envase, ver:<ul><li>[Descripción del producto App Builder](https://helpx.adobe.com/es/legal/product-descriptions/adobe-developer-app-builder.html) para los límites definidos por paquete.</li><li>[Limitaciones y configuración del sistema](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings) en las *Guías de tiempo de ejecución de App Builder*.</li><li>[Requisitos de almacenamiento de App Builder](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)</li></ul> |

{style="table-layout:auto"}

<!--## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your Adobe Commerce Optimizer solution, follow these steps:

1. Review the available packages, and start with a package that most closely matches your requirements.
1. Review the capabilities and metrics to ensure they align with your business requirements.
1. Purchase add-on packages for any metrics where you require additional capacity.

This approach ensures your solution is accurately sized for your business needs.

### Example use cases

1. **Seasonal Catalog Expansion**

   * Need: +20K SKUs
   * Add-On: 2 × SKU Packs (10K each)

1. **High Traffic Surge**

   * Need: +3M content requests/month
   * Add-On: 3 × content request packs (1M each)

1. **Global Presence**

   * Need: Additional environments for testing
   * Add-On: +1 Production, +2 Sandbox instances

1. **GenAI or Media Needs**

   * Need: +10M dynamic media ops/month
   * Add-On: 10 × dynamic media packs (1M each) -->
