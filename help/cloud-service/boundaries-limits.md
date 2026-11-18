---
title: Límites y límites de Adobe Commerce as a Cloud Service
description: Obtenga información acerca de los límites de licencias y del sistema de Adobe Commerce as a Cloud Service. Planifique la capacidad, realice un seguimiento del uso y evite la latencia y la limitación cuando se superen los límites.
role: Admin, Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y a [!DNL Adobe Commerce as a Cloud Service] proyectos (infraestructura SaaS administrada por Adobe)."
nudge: true
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: a13aaee57732f27b51a2d2acdd0ca3de364ee6ab
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 1%
---
# Límites y límites

[!DNL Adobe Commerce as a Cloud Service] aplica **límites de licencia** y **límites del sistema** que definen cuánta capacidad puede utilizar su proyecto:

- **Los límites de licencia** dependen de la capacidad que haya adquirido y se pueden ampliar comprando paquetes adicionales.
- **Los límites del sistema** son límites fijos que protegen los recursos del sistema y garantizan un rendimiento confiable para todos los usuarios.

>[!IMPORTANT]
>
> Su uso debe permanecer dentro de estos límites. Excederlos puede causar un aumento de la latencia y la limitación de solicitudes.

## Solicitar capacidad adicional

Puede aumentar sus límites de licencia comprando los paquetes de licencia descritos en [Límites de licencia y límites del sistema](#license-limits-and-system-boundaries), o negociando licencias personalizadas para casos de uso únicos. Póngase en contacto con su representante de cuentas de Adobe para hablar sobre sus necesidades.

Si tiene alguna pregunta sobre los límites del sistema, comuníquese con la [atención al cliente de Adobe](https://experienceleague.adobe.com/home?lang=es#support).

## Evitar problemas de rendimiento

Siga estas prácticas recomendadas para mantenerse dentro de los límites y evitar problemas operativos:

- **Revisa tus límites** - Comprende tus [límites de capacidad](#license-limits-and-system-boundaries) antes de lanzar nuevas tiendas o campañas.
- **Realizar un seguimiento de su uso** - Usar paneles de métricas integrados o registros de CDN.

## Límites de licencias y límites del sistema

En las tablas siguientes se resumen los límites de licencia y los límites del sistema por área de capacidad e incluyen información sobre el uso de licencias adicionales para ampliar la capacidad, según corresponda.

### Límites del entorno

| **Entorno** | **Descripción** | **Asignación base** | **Ampliable?** |
| --- | --- | --- | --- |
| **Entorno de espacio aislado** | El número de entornos de zona protegida incluidos | 2 por instancia | Sí<p>Añadir una licencia de entorno adicional por instancia</p> |
| **Entorno de producción** | El número de entornos de producción incluidos | 1 por instancia | Sí<p>Añadir una licencia de entorno adicional por instancia</p> |

{style="table-layout:auto"}

### Catálogo

| **Capacidad** | **Descripción** | **Asignación base** | **Ampliable?** |
| --- | --- | --- | --- |
| Tasa de ingesta de productos | El número de productos creados o actualizados | 1K actualizaciones por minuto<p>Un máximo de 100 000 actualizaciones al día</p> | Sí<p>Agregar un paquete de licencias:</p><ul><li>Actualizaciones de 5K por minuto<br>Un máximo de 500K actualizaciones por día</li><li>10 000 actualizaciones por minuto<br>Un máximo de 1 millón de actualizaciones por día</li></ul><p>La capacidad máxima de ingesta de datos es de 1 millón de actualizaciones al día.</p> |
| Tamaño de carga útil del producto | Cantidad máxima de datos permitida al crear, actualizar o ingerir información de producto mediante la API | 200 KB | No |
| Categorías | El número de categorías en las que se pueden agrupar los productos | 6,000 | No |
| Número de productos | Número de SKU admitidas en el catálogo | SKU de 250.000 | Sí<p>Añadir paquete de licencias de SKU a 100.000</p> |
| Variantes por producto | Número de variantes de producto (tamaño, combinaciones de colores) permitidas por producto | 10K | No |
| Vistas de tienda | El número de contextos de vista de tienda (por ejemplo, configuraciones regionales) | 50 | No |
| SLA para que una actualización de producto aparezca en la búsqueda | Hora a la que debe aparecer una creación o actualización de producto en la búsqueda de tiendas | 10 a 15 minutos | No |

{style="table-layout:auto"}

### Finalizar compra

| **Capacidad** | **Descripción** | **Asignación base** | **Ampliable?** |
| --- | --- | --- | --- |
| Productos en el carro | Número de productos permitidos por carro de compras | 650 | No |
| Direcciones de clientes por cuenta | Número de direcciones de clientes permitidas por cuenta | 2,000 | No |
| Reglas de precios del carrito | El número de reglas de precios del carro de compras que aplican descuentos a los artículos del carro de compras, según un conjunto de condiciones | 100,000 | No |
| Cupones | El número de códigos de cupón utilizados con las reglas de precios del carro de compras | 1,000,000 | No |

{style="table-layout:auto"}

<!--
# Price books

# | **Capability** | **Description** | **Base allocation** | **Expandable?** |
# | --- | --- | --- | --- |
# | Price books | The number of price books allowed per instance | Based on the number of [Catalog variations](#catalog) | Yes<br>Increase catalog variations |
# | Discounts per price record | The number of discounts that can be applied to a product price within a single price book | 10 | No |

{style="table-layout:auto"}
-->

### [!DNL Product Visuals] límites

| **Capacidad** | **Descripción** | **Asignación base** | **Ampliable?** |
| --- | --- | --- | --- |
| Imágenes del producto Usuarios avanzados | Usuario con licencia con capacidades completas de administración de recursos digitales, incluidas herramientas de IA, integraciones de [!DNL Adobe Express]/[!DNL Firefly] y uso compartido de Content Hub, que gestiona tareas principales de DAM y funciones avanzadas nativas de la nube para lograr una eficacia óptima. | 2 | Sí<p>Actualizar a la licencia [!DNL AEM Assets]</p> |
| Visuales del producto Usuarios de Collaborator | Acceda a los recursos y trabaje con ellos a través de la integración de AEM Commerce, cree y edite contenido con [!DNL Adobe Express] y [!DNL Firefly] y, si está habilitado, aproveche los recursos aprobados a través del portal de Content Hub. | 2 | Sí<p>Actualizar a la licencia [!DNL AEM Assets]</p> |
| Almacenamiento de imágenes del producto | Espacio de almacenamiento asignado para recursos | Almacenamiento de 1 TB | No |
| Uso de Dynamic Media | Asignación para operaciones de procesamiento de medios dinámicos, que incluye:<ul><li>Entrega de imágenes</li><li>Imágenes inteligentes</li><li>Entrega de vídeo</li></ul><p>Para obtener más información, consulte *Calcular el uso de Dynamic Media* a continuación. | Basado en GMV (valor bruto de mercancía)<p>Asignación mínima: 5M operaciones/mes</p> | Sí<ul><li>Licencia de compra para operaciones adicionales</li><li>Actualizar a la licencia [!DNL AEM Assets]</li></ul> |
| Entrega de vídeo | Asignación para descargas o envíos de vídeo | 300 vídeos, 1 minuto por vídeo | Sí<p>Actualizar a la licencia [!DNL AEM Assets]</p> |
| Generación de recursos | Acceso a [!DNL Adobe Express] y a [!DNL Adobe Firefly] IA generativa para crear imágenes | Ninguno | Compre créditos de IA generativos por separado |

{style="table-layout:auto"}

>[!NOTE]
>
>**Usuarios avanzados** pueden acceder a [!DNL Adobe Express] directamente o en un plazo de [!DNL Adobe Commerce as a Cloud Service].
>
>**Los usuarios de Collaborator** pueden tener acceso directo a la aplicación [!DNL Adobe Express]. El uso está regido por [Adobe Express con términos de licencia específicos de productos Firefly](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf).

>[!BEGINSHADEBOX &quot;Calcular uso de Dynamic Media&quot;]

El uso de Dynamic Media hace un seguimiento de las solicitudes de API que llegan a los componentes de elementos visuales del producto en [!DNL Adobe Commerce as a Cloud Service] para facilitar una de las siguientes acciones:

- **La entrega de imágenes consume una operación de medios dinámicos** por cada ocurrencia de lo siguiente:
  - **transformación básica de la imagen** de un recurso digital; por ejemplo, operaciones de cambio de tamaño, escala, conversión de formato, compresión o recorte.
  - **entrega o descarga de imagen estática** de dichos recursos digitales o representación de recursos digitales (que no sean vídeos).
- **La entrega de imágenes inteligentes consume 20 operaciones de Dynamic Media** para cada entrega optimizada de un único recurso digital al generar automáticamente la representación de imágenes más adecuada para el dispositivo y el explorador del usuario final.
- **La entrega de vídeo consume 20 operaciones de Dynamic Media** para una sola entrega o descarga de un vídeo o una variante transformada de un vídeo.

>[!ENDSHADEBOX]

>[!NOTE]
>
>Los límites anteriores cubren las asignaciones de capacidad y uso. Para obtener información general sobre las características visuales de productos y las restricciones funcionales, vea [Imágenes de productos con AEM Assets](../optimizer/setup/product-visuals.md).

<!--
### Catalog views and policies

| **Capability** | **Description** | **Base allocation** | **Expandable?** |
| --- | --- | --- | --- |
| Catalog views | Number of configurable subsets of your master catalog | Based on the number of [Catalog variations](#catalog) | Yes<br>Increase catalog variations |
| Policies per catalog view | Number of data filters allowed | 10 | No |
| Attribute values in a policy | Number of product characteristics that can be configured for filtering | 100 | No |
| [Restricted access key assignment](setup/private-catalog-view.md) | Number of restricted access keys that can be assigned to a single catalog view | 3 | No |
| RSA key size (restricted access keys) | Minimum and maximum key strength accepted for a restricted access key | 2048-bit minimum, 8192-bit maximum | No |
| Restricted access keys | Key revocation propagation delay | Up to 5 minutes, due to caching. Tokens signed by a removed key are denied once the delay elapses. | Not applicable |

{style="table-layout:auto"}
-->

### Tienda de catálogo

La asignación base para las capacidades de tienda de catálogo se determina en función del nivel GMV (valor bruto de mercancía). La tabla indica la asignación mínima para cada capacidad.

| **Capacidad** | **Descripción** | **Asignación base** | **Ampliable?** |
| --- | --- | --- | --- |
| Tasa de recuperación del catálogo | Número de veces que un sistema (tienda, sistema de transacciones, ERP u otro) llama mensualmente a una API de catálogo para recuperar datos del catálogo | Basado en el nivel de GMV<p>Asignación mínima: 10M/mes</p> | Sí<p>Agregar un millón de solicitudes al mes en paquetes de licencias</p> |
| Solicitudes de contenido | Solicitudes a la tienda para vistas de página de HTML o llamadas a la API JSON. Se cuenta como 1 vista de página o 5 llamadas a la API. | Basado en el nivel de GMV<p>Asignación mínima: 2 millones por mes</p> | Sí<p>Añadir un paquete de licencias de 1 millón al mes</p> |
| Variaciones GenAI de Storefront | Asignación para la generación de contenido basado en texto | Basado en el nivel de GMV<p>Asignación mínima: 1K variaciones/mes</p> | Sí<p>Compre créditos de IA generativos por separado</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>La generación de imágenes requiere una licencia de [!DNL Adobe Firefly] aprovisionada para la misma organización de IMS que [!DNL Adobe Commerce as a Cloud Service].

### Descubrimiento de productos

Los límites siguientes se aplican a la configuración de búsqueda de productos, listados y comercialización de tiendas.

| **Capacidad** | **Descripción** | **Asignación base** | **Ampliable?** |
| --- | --- | --- |---------------------------------------------------|
| Recuperación de productos | Número máximo de SKU por solicitud de GraphQL de [!DNL Catalog Service] al recuperar datos de productos con `products`, `productSearch`, `refineProduct` y `variants`. Dividir solicitudes más grandes en varias llamadas. | 100 | No |
| Atributos filtrables | El número de características del producto (como color, tamaño, marca o material) que se pueden habilitar para la navegación por capas y las facetas | 200 | No |
| Atributos de búsqueda | El número de características del producto que se pueden indexar para la búsqueda en el catálogo | 200 | No |
| Atributos ordenables | El número de características del producto disponibles como opciones de ordenación en las páginas de búsqueda y categoría. | 50 | No |
| Profundidad de paginación de búsqueda | Máximo de productos accesibles a través de la paginación de búsqueda (por ejemplo, página 100 × 100 productos/página) | 10K | No |
| Facetas | El número de atributos de producto filtrables (como marca, color, tamaño y precio) que se pueden configurar para ayudar a los compradores a refinar los resultados de búsqueda y examinar las categorías | 100<p>Deben ser atributos filtrables</p> | Sí<p>Puede aumentar a 500 mediante una solicitud de asistencia</p> |
| Opciones por faceta | El número de valores de atributos de producto filtrables que los compradores pueden seleccionar dentro de una faceta (por ejemplo, &quot;Rojo&quot;, &quot;Azul&quot; para Color; &quot;Pequeño&quot;, &quot;Medium&quot; para Tamaño) | 100 | Sí<p>Puede aumentar mediante una solicitud de asistencia</p> |

{style="table-layout:auto"}

### Recommendations

Las siguientes funciones están disponibles para recomendaciones de productos. Algunas características disponibles en otros productos de Adobe Commerce no son compatibles con [!DNL Adobe Commerce as a Cloud Service].

| **Capacidad** | **Descripción** | **Asignación base** | **Ampliable?** |
| --- | --- | --- | --- |
| Unidades de recomendación activas | Número de componentes de recomendaciones activas en la tienda (como &quot;Los clientes también vieron&quot; o &quot;Es posible que también te guste&quot;) | 50 unidades activas por tipo de página para recomendaciones de productos, con ámbito explícito del modelo de catálogo si es necesario | No |

{style="table-layout:auto"}
<!-- Talos complained about this even thought it was copied directly from the ACO version of this page. Commenting out for now, | Category or attribute inclusions/exclusions | Filter products to a specific set that qualifies for recommendations | Not supported | — | -->

### Extensibilidad

| **Capacidad** | **Descripción** | **Asignación base** | **Ampliable?** | **Notas** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | Capacidad para crear integraciones y extensiones nativas de la nube | Basado en el nivel de GMV<p>Asignación mínima: 1 paquete/año</p> | Sí<p>Adición de paquetes adicionales</p> | Para los límites definidos por envase, ver:<ul><li>[Descripción del producto de App Builder](https://helpx.adobe.com/es/legal/product-descriptions/adobe-developer-app-builder.html).</li><li>[Limitaciones y configuración del sistema](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings) en las *Guías de tiempo de ejecución de App Builder*.</li><li>[Requisitos de almacenamiento de App Builder](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)</li></ul> |

{style="table-layout:auto"}

<!--
## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your [!DNL Adobe Commerce as a Cloud Service] solution, follow these steps:

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
   * Add-On: 10 × dynamic media packs (1M each)
-->
