---
title: Notas de la versión de Adobe Commerce Optimizer
description: Información de versión mensual de  [!DNL Adobe Commerce Optimizer], incluidas las actualizaciones de la API de REST de ingesta de datos y de la API de GraphQL para la recuperación de datos del catálogo de tiendas.
feature: Release Notes
role: Admin, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
TQID: https://experienceleague.adobe.com/apcpxN0AOniRcHDCa5MMAVWysxRO5mTcudXXXjET-Lo
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 27cbf66e4851f0d21ecc039fd53aa838b4c211ba
workflow-type: tm+mt
source-wordcount: 1365
ht-degree: 0%

---

# Notas de la versión

Las siguientes notas de la versión contienen actualizaciones de [!DNL Adobe Commerce Optimizer], entre ellas:

* Nuevas características y mejoras en [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour).
* Actualizaciones a la [API de REST de ingesta de datos](https://developer.adobe.com/commerce/services/reference/rest/) y a la [API de GraphQL para la recuperación de datos del catálogo de tiendas](https://developer.adobe.com/commerce/services/reference/graphql/).

  {{aco-api-updates-and-dropins}}

## Julio de 2026

>[!BEGINSHADEBOX]

_20 de julio de 2026_

![Corregir](../assets/fix.svg) **Rendimiento de navegación de categoría**: se aplicaron optimizaciones de rendimiento al servicio de categoría, lo que dio como resultado un mayor rendimiento y una menor latencia P99 para la consulta `CategoryNavigation`, lo que mejoró la capacidad de respuesta del servicio y la experiencia general del usuario con una carga alta.
<!--DATA-7131 DATA-7250-->

{{aco-release}}

>[!ENDSHADEBOX]

## Junio de 2026

>[!BEGINSHADEBOX]

_24 de junio de 2026_

<!-- v1.3 -->

![Nuevo](../assets/new.svg) **Nuevo campo `canEditQuantity`**—Se agregó `canEditQuantity` a `ProductViewOptionValueProduct` en el GraphQL del servicio de catálogo. Expone la configuración de cantidad **definida por el usuario** opcional para las selecciones de paquetes del administrador de Commerce, de modo que los consumidores de tienda puedan determinar si la cantidad de una selección de paquetes es editable.
<!--COMOPT-2050-->

### Búsqueda semántica

[!DNL Adobe Commerce Optimizer] ahora admite **[búsqueda semántica]** en la ficha [**Búsqueda avanzada**](./settings.md#advanced-search) de **[!UICONTROL Settings]**. La búsqueda semántica utiliza IA para hacer coincidir productos por significado y contexto junto con la búsqueda de palabras clave, lo que reduce las páginas de búsqueda vacías para consultas en lenguaje natural. Está activada de forma predeterminada para los catálogos en inglés aptos. Opcionalmente, puede ajustar **[!UICONTROL Semantic boost]**, **[!UICONTROL Similarity threshold]** y **[!UICONTROL Fuzzy search]** en la misma ficha. No es necesario configurar atributos ni realizar cambios en la tienda. [Más información](./setup/semantic-search.md).

### Filtros de precios de recomendación (beta)

Las unidades de recomendación de productos ahora admiten [**filtros de precio**](./merchandising/recommendations/filters.md#price) en el paso **[!UICONTROL Filter products]**. Incluya o excluya candidatos que usen los rangos mínimo y máximo de **static** o las reglas de **dynamic** en la página de detalles del producto que comparen productos recomendados con el **precio calculado final** del producto que se está viendo actualmente en el libro de precios activo de la tienda. Las reglas de precios filtran el conjunto de candidatos. No vuelven a clasificar los productos. [Más información](./merchandising/recommendations/filters.md#price).

{{aco-release}}

>[!ENDSHADEBOX]

## Mayo de 2026

>[!BEGINSHADEBOX]

### Aumento inteligente de clasificación

[Las reglas de comercialización](./merchandising/rules/add.md#intelligent-ranking-boost) para búsquedas, listados de productos predeterminados y [páginas de categoría](./merchandising/rules/add.md#rule-types) ahora incluyen **[!UICONTROL Intelligent Ranking Boost]**. Puede ajustar la fuerza con la que estrategias como **Más visitados** o **Tendencias** influyen en el orden del producto en relación con la relevancia textual en las señales de búsqueda y comportamiento en los listados de categorías. La vista previa de la regla refleja su configuración. El aumento se aplica en el momento de la consulta, por lo que no necesita una resincronización del catálogo al cambiarlo.

### Actualizaciones de API

_28 de mayo de 2026_

<!-- v1.2 -->

![Corrección](../assets/fix.svg) **Árboles de navegación completos**: Las categorías descendientes etiquetadas ahora se incluyen correctamente en los árboles `navigation` filtrados por la familia cuando existe un nodo intermedio sin etiquetar en la ruta de acceso. Esta corrección garantiza que los compradores vean todas las categorías relevantes en la navegación, lo que facilita la exploración y la detección de artículos.
<!--DATA-7183-->

![Corrección](../assets/fix.svg) **Administración de slug vacía en `categoryTree` solicitudes**—Se ha corregido un problema en el cual la consulta [`categoryTree`](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) devolvía un error interno del servidor cuando el argumento `slugs` incluía una cadena vacía. Ahora se omiten los valores de slug vacíos, por lo que las tiendas y las integraciones siguen resolviendo los datos de categoría sin solicitudes fallidas.
<!--DATA-7184-->

![Corregir](../assets/fix.svg) **`searchCategory`solicitudes devuelve resultados alfabetizados que no distinguen entre mayúsculas y minúsculas**—La consulta `searchCategory` ahora ordena los resultados de búsqueda alfabéticamente sin distinción entre mayúsculas y minúsculas, lo que garantiza un orden coherente y predecible. Las categorías con prefijos más cortos aparecen primero cuando los nombres son idénticos.
<!--COMOPT-2142-->

_4 de mayo de 2026_

<!--v1.53-->

**Visualización correcta de la moneda**: los precios de los productos de tienda ahora muestran el código de moneda correcto (por ejemplo, USD) para todos los tipos de productos. Anteriormente, algunos productos mostraban `NONE` en lugar de la moneda esperada, lo que resultaba en la falta de precios.

<!--DATA-7115-->

{{aco-release}}

>[!ENDSHADEBOX]

## Abril de 2026

**Fecha de publicación**: 7 de abril de 2026

>[!BEGINSHADEBOX]

### Reglas de catálogo

[Las reglas de categoría](./merchandising/rules/add.md) amplían las reglas de comercialización para que pueda segmentar categorías y controlar el pedido de productos en páginas de categoría con la misma clasificación y acciones (fijar, aumentar, enterrar) que la búsqueda.

### Filtro de precios (beta)

Los filtros de recomendación ahora incluyen un [filtro de rango de precios](./merchandising/recommendations/filters.md#price) (mínimo y máximo).

### Actualizaciones de API

_29 de abril de 2026_

<!--v1.52 release-->

**Se requiere el agrupamiento de solicitudes** — La API de GraphQL ahora aplica un máximo de 100 SKU por solicitud al recuperar los datos del catálogo. Ver [límites y límites documentados](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits#product-discovery).

<!--DATA-7156-->

_17 de abril de 2026_

<!--v1.51 release-->

**Buscar categorías por nombre con GraphQL** — La nueva consulta [`searchCategory`](https://developer.adobe.com/commerce/services/reference/graphql/) devuelve categorías coincidentes con paginación para tiendas e integraciones. Consulte la referencia de la API para ver los parámetros y los campos de respuesta. <!--COMOPT-1819-->

_7 de abril de 2026_

<!--v1.50 release-->

**Búsquedas de categoría más sencillas**: la consulta [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) trata a `family` como opcional, de modo que puede resolver categorías mediante slug sin proporcionar una familia.

{{aco-release}}

>[!ENDSHADEBOX]

## Marzo de 2026

No hubo [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) versiones este mes. Consulte Actualizaciones de API a continuación.

>[!BEGINSHADEBOX]

### Actualizaciones de API

_24 de marzo de 2026_

Los paquetes dinámicos ahora devuelven un intervalo de precios calculado. <!--DATA-7014-->

{{aco-release}}

>[!ENDSHADEBOX]

## Febrero de 2026

**Fecha de publicación**: 19 de febrero de 2026

>[!BEGINSHADEBOX]

### Vista de catálogo de reglas y recomendaciones de comercialización

Ahora puede especificar una vista de catálogo al [crear unidades de recomendación](./merchandising/recommendations/create.md) o [reglas de comercialización](./merchandising/rules/add.md).

### Actualizaciones de API

_19 de febrero de 2026_

<!--v1.48-->

**Contenido de categoría más rico para escaparates** — La consulta [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) ahora devuelve descripciones, imágenes y metaetiquetas SEO para que los escaparates puedan mostrar páginas de categoría más ricas.<!--DATA-6933-->

_12 de febrero de 2026_

<!--v1.49-->

**Datos de productos mejorados por categoría**: la API de GraphQL agrega el tipo [`CategoryProductView`](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#definition-CategoryProductView){target="blank"} para que pueda consultar y filtrar productos por categoría con menos viajes de ida y vuelta.

{{aco-release}}

>[!ENDSHADEBOX]

## Enero de 2026

No hubo [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) versiones este mes. Consulte Actualizaciones de API a continuación.

>[!BEGINSHADEBOX]

### Actualizaciones de API

_19 de enero de 2026_

* **Compatibilidad con categorías más ricas con la API de REST** — Las operaciones de la API [Categorías](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories) ahora aceptan valores `metaTags`, `images` y `description` opcionales además de `families`, para que pueda proporcionar detalles de comercialización y SEO más completos para las categorías.

{{aco-release}}

>[!ENDSHADEBOX]

## Diciembre de 2025

**Fecha de la versión**: 10 de diciembre de 2025

>[!BEGINSHADEBOX]

### Oportunidades

Los comerciantes ahora pueden obtener recomendaciones con tecnología de IA a través de [Adobe Sites Optimizer](./manage-results/opportunities.md) para detectar problemas en el sitio y sugerir correcciones de rendimiento.

### Capas de catálogo

Los comerciantes ahora pueden usar [Capas de catálogo](./setup/catalog-layer.md) para superponer datos de productos sin editar el catálogo de origen, administrar la prioridad de las capas y usar la corrección automática de Adobe Sites Optimizer.

{{aco-release}}

>[!ENDSHADEBOX]

## Noviembre de 2025

No hubo [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) versiones este mes. Consulte Actualizaciones de API a continuación.

>[!BEGINSHADEBOX]

### Actualizaciones de API

_21 de noviembre de 2025_

**Se han actualizado las instrucciones de autenticación para la API de REST de ingesta de datos**. Las instrucciones ahora hacen referencia a los tokens de acceso de OAuth y a los ámbitos de credenciales de Developer Console correctos para el servicio de ingesta de datos. Si los ámbitos de las credenciales están obsoletos, vuelva a crearlos para mantener el acceso.

_3 de noviembre de 2025_

<!-- v1.43 -->

**Contenido de producto localizado y con capas en GraphQL**: ahora puede entregar contenido de producto específico del canal y según la configuración regional desde [!DNL Adobe Commerce Optimizer].

* Adaptar el contenido del producto por segmento de cliente
* Aplicar invalidaciones específicas de la configuración regional sin duplicar los datos del catálogo base
* Controlar las anulaciones de nivel de campo con máscaras de capa
* Utilice capas de contenido premium, estacionales y optimizadas para dispositivos móviles

Sin cambio de esquema de la API de GraphQL: las capas se aplican a través de los encabezados de solicitud y consulta de `products` existentes. Ver [capa de catálogo](./setup/catalog-layer.md).

{{aco-release}}

>[!ENDSHADEBOX]

## Octubre de 2025

**Fecha de la versión**: 14 de octubre de 2025

>[!BEGINSHADEBOX]

### Conector de Commerce de Commerce Optimizer Salesforce

[!DNL Commerce Optimizer Salesforce Commerce Connector] es un nuevo Starter Kit de App Builder que sincroniza los datos del catálogo de Salesforce B2C Commerce en [!DNL Commerce Optimizer].<!--COMOPT-536-->

**Para administradores:**

* Los cambios de catálogo de Salesforce (productos, precios, metadatos, libros de precios) se sincronizan automáticamente con [!DNL Commerce Optimizer].
* Se ejecuta fuera de [!DNL Adobe Commerce] para obtener menos puntos de contacto de integración.
* Las actualizaciones programadas mantienen actualizados los datos de [!DNL Commerce Optimizer] para la comercialización y las recomendaciones.

**Para desarrolladores:**

* Marco extensible para la ingesta del catálogo de Salesforce en servicios de comercialización de SaaS.
* Implementaciones de referencia, documentos de diseño y ejemplos de código para generaciones y resolución de problemas más rápidos.

### Búsqueda por capas

* **Búsqueda por niveles (GA)**: la búsqueda de productos ahora admite la coincidencia de `startsWith` y `contains`. Consulte [Búsqueda por niveles y tipos de búsqueda expandida](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types).

### Actualizaciones de API

* _17 de octubre de 2025_

  **Agregar compatibilidad con la API de REST para ingerir capas de producto** — Use la [API de capas de catálogo](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers) para personalizar y anular los datos de productos base para contextos, configuraciones regionales o requisitos empresariales específicos. Después de crear las capas, puede aplicarlas y administrarlas desde [Adobe Commerce Optimizer Studio](./setup/catalog-layer.md).<!--DATA-6632-->

* _14 de octubre de 2025_

  **Árboles de categoría programática**: Cree, actualice y administre árboles de categoría para la navegación y la agrupación mediante REST (global o específico del canal), a escala: hasta 10 000 árboles y 500 categorías por árbol. Consulte [Categorías](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="blank"} en la _Referencia de API de REST de ingesta de datos de catálogo_.<!--DCAT-2649-->

* _8 de octubre de 2025_

  **Asignación de categorías más clara para la ingesta de datos**: las nuevas directrices explican el formato de slug de categoría y las reglas de jerarquía, y aclaran que los valores del producto `routes.path` deben coincidir con un slug de categoría existente (por ejemplo, `men/clothing`).

{{aco-release}}

>[!ENDSHADEBOX]

## Septiembre de 2025

No hubo [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) versiones este mes. Consulte Actualizaciones de API a continuación.

>[!BEGINSHADEBOX]

### Actualizaciones de API

_23 de septiembre de 2025_

* **Administrar categorías mediante la API de REST**: usa la [API de categorías](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories) para crear y administrar categorías. Las categorías organizan los productos en grupos lógicos y admiten jerarquías anidadas a través de rutas basadas en slug. Después de asignar categorías a los productos, recupérelas con las consultas de GraphQL `[navigation](https://developer.adobe.com/commerce/services/reference/graphql/#navigation)` y `[categoryTree](https://developer.adobe.com/commerce/services/reference/graphql/#categorytree)` para representar los menús de tienda y los árboles de categorías.<!--DCAT-2626-->

{{aco-release}}

>[!ENDSHADEBOX]

## Agosto de 2025

**Fecha de lanzamiento**: 28 de agosto de 2025

>[!BEGINSHADEBOX]

### Región de la UE ya disponible

La región de producción de la UE (**eu1**) está disponible para las organizaciones IMS. Cuando [agregue una [!DNL Commerce Optimizer] instancia](./get-started.md#step-1-create-an-instance) en Cloud Manager, elija **[!UICONTROL European Union]** como **[!UICONTROL Region]** (solo producción).

Las URL de producción de base para la región de la Unión Europea son:

* Administrador: `https://eu1.admin.commerce.adobe.com`
* REST y GraphQL: `https://eu1.api.commerce.adobe.com`

![Cuadro de diálogo Crear instancia de Cloud Manager con el campo Región](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

{{aco-release}}

>[!ENDSHADEBOX]

