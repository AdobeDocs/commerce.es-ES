---
title: Notas de la versión
description: La información de la versión más reciente de  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
source-git-commit: a42f6b3348eed476095c6d9777ac9486579fe6ea
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 1%

---

# Notas de la versión

Las siguientes notas de la versión contienen actualizaciones de [!DNL Adobe Commerce Optimizer].

## Abril de 2026

**Fecha de publicación**: 7 de abril de 2026

>[!BEGINSHADEBOX]

### Reglas de catálogo (beta)

Las reglas de comercialización ahora incluyen [reglas de categoría](./merchandising/rules/add.md), por lo que puede segmentar una o más categorías y controlar el orden del producto en las páginas de categoría utilizando la misma clasificación inteligente y las mismas acciones manuales (fijar, aumentar, enterrar) que para la búsqueda.

### Filtro de precios (beta)

Los filtros de recomendación ahora admiten un [filtro de precio](./merchandising/recommendations/filters.md#price) que puede usar para establecer un rango de precios mínimo y máximo para los productos.

{{aco-release}}

>[!ENDSHADEBOX]

## Febrero de 2026

**Fecha de publicación**: 19 de febrero de 2026

>[!BEGINSHADEBOX]

### Vista de catálogo de reglas y recomendaciones de comercialización (beta)

Se ha agregado la capacidad de especificar una vista de catálogo al [crear unidades de recomendación](./merchandising/recommendations/create.md) o [reglas de comercialización](./merchandising/rules/add.md).

{{aco-release}}

>[!ENDSHADEBOX]

## Diciembre de 2025

**Fecha de la versión**: 10 de diciembre de 2025

>[!BEGINSHADEBOX]

### Oportunidades

Las recomendaciones de optimización de sitios con tecnología de IA ya están disponibles a través de la [integración de Adobe Sites Optimizer](./manage-results/opportunities.md). Esta función ayuda a los comerciantes a identificar y abordar los problemas que afectan al rendimiento del sitio de comercio mediante la detección automatizada y las recomendaciones inteligentes.

### Capas de catálogo

Se agregaron [capas de catálogo](./setup/catalog-layer.md) para que pueda modificar los datos de producto sin cambiar los datos de origen, incluida la administración de prioridades de capa y la integración con las funciones de corrección automática de Adobe Sites Optimizer.

{{aco-release}}

>[!ENDSHADEBOX]

## Octubre de 2025

**Fecha de la versión**: 14 de octubre de 2025

>[!BEGINSHADEBOX]

### Conector de Commerce de Commerce Optimizer Salesforce

[!DNL Commerce Optimizer Salesforce Commerce Connector] es un nuevo Starter Kit de integración de App Builder que permite a los administradores y desarrolladores de Commerce conectar sin problemas los datos del catálogo de Commerce B2C de Salesforce con [!DNL Commerce Optimizer].<!--COMOPT-536-->

**Para administradores:**

* Las actualizaciones de catálogo de Salesforce (productos, precios, metadatos, libros de precios) se sincronizan automáticamente con Commerce Optimizer, sin necesidad de intervención manual.
* La integración funciona de forma independiente del Adobe Commerce, lo que reduce la complejidad y los posibles puntos de error.
* Los administradores pueden confiar en la programación regular de actualizaciones programadas para garantizar datos de catálogo precisos dentro de Commerce Optimizer, lo que mejora la comercialización y las recomendaciones de productos.

**Para desarrolladores:**

* El Starter Kit ofrece un marco de trabajo optimizado y ampliable para la ingesta de datos del catálogo de Salesforce en los servicios de comercialización de SaaS.
* Hay implementaciones de referencia, documentación de diseño y ejemplos de código disponibles para acelerar las integraciones personalizadas o la solución de problemas.<!--COMOPT-536-->

### Búsqueda por capas

* Versión de GA para las siguientes funciones de búsqueda avanzada: búsqueda por niveles con `startsWith` y `contains`. [Más información](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types).

### API de categorías

Ya está disponible una nueva API de REST de categorías, que permite a los administradores y desarrolladores crear, actualizar y administrar mediante programación varios árboles de categorías para la navegación y la agrupación de productos. La API admite configuraciones globales y específicas del canal, y está diseñada para proporcionar una alta escalabilidad, admitiendo hasta 10 000 árboles de categorías y 500 categorías por árbol. Para obtener más información, consulte [Categorías](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#categories) en la _Guía para desarrolladores de servicios de comercialización_.<!--DCAT-2649-->

{{aco-release}}

>[!ENDSHADEBOX]

## Agosto de 2025

**Fecha de lanzamiento**: 28 de agosto de 2025

>[!BEGINSHADEBOX]

### Región de la UE ya disponible

Ya está disponible la compatibilidad con la región de la Unión Europea (eu1) para las organizaciones de IMS de clientes. Ahora puede seleccionar **European Union** como **región** al [agregar una instancia de Commerce Optimizer](./get-started.md#step-1-create-an-instance) en Cloud Manager. La región de la Unión Europea solo está disponible para entornos de producción.

Las URL de producción de base para la región de la Unión Europea son:

* Administrador: `https://eu1.admin.commerce.adobe.com`
* REST y GraphQL: `https://eu1.api.commerce.adobe.com`

![crear instancia](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

{{aco-release}}

>[!ENDSHADEBOX]
