---
title: Fuentes de catálogo
description: Descubra cuáles son las fuentes de catálogo y cómo definen el ámbito autorizado de los productos, atributos y categorías para el comportamiento de búsqueda, filtro y ordenación.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
autotag-review: '2026-06-09T19:36:23.516Z'
TQID: 'https://experienceleague.adobe.com/MiLbuYx6Pf95n3jvrgvou05Ery9XHXskx8p6KrN6CYg'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 94ba07437d532d0d101c166f58114c2aa0bd4be4
workflow-type: tm+mt
source-wordcount: 446
ht-degree: 0%

---

# Fuentes de catálogo

Los orígenes de catálogo representan ámbitos autorizados de productos, atributos y categorías. Suelen asignarse a los límites del idioma, la audiencia o el sistema de origen y determinan el comportamiento de búsqueda, filtrado y ordenación.

## Fuentes de catálogo frente a conceptos relacionados

Comprender cómo se relacionan las fuentes de catálogo con otros [!DNL Adobe Commerce Optimizer] conceptos le ayuda a modelar los datos correctamente:

* **Origen del catálogo**: el contexto de datos subyacente que proporciona información del producto. Un origen de catálogo suele ser una configuración regional (por ejemplo, `en-US`, `fr-CA`) o un sistema externo como PIM o ERP. Los productos, los atributos, los metadatos y las categorías se clasifican por origen de catálogo. Piense en un origen de catálogo como *de dónde* provienen los datos del catálogo sin procesar y *cómo* afectan al descubrimiento de productos (resultados de búsqueda, filtrado y ordenación).

* **[Vista de catálogo](catalog-view.md)**: una vista configurada del catálogo para una necesidad comercial específica. Cuando crea una vista de catálogo, selecciona qué origen de catálogo (o configuración regional) usar y luego agrega [directivas](policies.md) para filtrar qué productos son visibles y vincula [libros de precios](pricebooks.md) para controlar los precios. Un solo origen de catálogo puede activar muchas vistas de catálogo (por ejemplo, un origen de `en-US` con vistas de catálogo independientes para diferentes marcas o regiones). Considere una vista de catálogo como *cómo* expone esos datos a una tienda, canal o audiencia.

* **[Capa de catálogo](catalog-layer.md)**: una capa aplicada sobre los datos del catálogo base para modificar los atributos del producto (nombre, descripción, imágenes, metadatos) sin cambiar los datos de origen. Utilice capas de catálogo cuando las diferencias deban afectar solo a la visualización de tiendas, no al descubrimiento de productos.

## Reglas y limitaciones

* Cada fuente de catálogo se crea mediante la ingesta de un producto a través de la API de ingesta de datos. Consulte [Documentos de desarrolladores - Ingesta de datos](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/) para obtener más información.
* La exclusividad del producto viene determinada por el SKU + el origen del catálogo.
* Los compradores no acceden directamente a las fuentes del catálogo. Los datos del catálogo se exponen a la tienda a través de [vistas de catálogo](catalog-view.md).

## Guía de modelado

Siga estas directrices a la hora de decidir cómo estructurar los orígenes de catálogo:

* Cree un origen de catálogo independiente para cada idioma de catálogo.
* Utilice orígenes de catálogo independientes cuando las diferencias de producto y atributo deban afectar al comportamiento de búsqueda, filtrado u ordenación (por ejemplo, una capacidad de búsqueda, filtrado o configuración de faceta diferentes para el mismo atributo).
* Use [capas de catálogo](catalog-layer.md) cuando las diferencias de producto y atributo deban afectar solamente la visualización de la tienda, no la detección de productos.

>[!MORELIKETHIS]
>
> * [Vistas de catálogo](catalog-view.md): configure vistas filtradas con precios sobre un origen de catálogo
> * [Capas de catálogo](catalog-layer.md): modifique la presentación del producto sin cambiar los datos de origen
> * [Directivas](policies.md) - Crear filtros basados en atributos para vistas de catálogo
> * [Libros de precios](pricebooks.md): administre estructuras de precios para diferentes segmentos de clientes

