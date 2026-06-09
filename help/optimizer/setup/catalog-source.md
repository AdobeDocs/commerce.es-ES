---
title: Origen del catálogo
description: Descubra cuáles son las fuentes de catálogo y cómo definen el ámbito autorizado de los productos, atributos y categorías para el comportamiento de búsqueda, filtro y ordenación.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
source-git-commit: dc50e4d7bcd118b2b9a800779c600ade5560e0bf
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# Origen del catálogo

Un origen de catálogo representa un ámbito autorizado de productos, atributos y categorías. Las fuentes de catálogo suelen asignarse a los límites del idioma, la audiencia o el sistema de origen, y determinan el comportamiento de búsqueda, filtrado y ordenación.

## Conceptos relacionados con el origen del catálogo

Comprender cómo se relaciona un origen de catálogo con otros [!DNL Adobe Commerce Optimizer] conceptos le ayuda a modelar los datos correctamente:

* **Origen del catálogo**: el contexto de datos subyacente que proporciona información del producto. Un origen de catálogo suele ser una configuración regional (por ejemplo, `en-US`, `fr-CA`) o un sistema externo como PIM o ERP. Los productos, los atributos, los metadatos y las categorías se clasifican por origen de catálogo. Piense en un origen de catálogo como *de dónde* provienen los datos del catálogo sin procesar y *cómo* afectan al descubrimiento de productos (resultados de búsqueda, filtrado y ordenación).

* **[Vista de catálogo](catalog-view.md)**: una vista configurada del catálogo para una necesidad comercial específica. Cuando crea una vista de catálogo, selecciona qué origen de catálogo (o configuración regional) usar y luego agrega [directivas](policies.md) para filtrar qué productos son visibles y vincula [libros de precios](pricebooks.md) para controlar los precios. Un solo origen de catálogo puede activar muchas vistas de catálogo (por ejemplo, un origen de `en-US` con vistas de catálogo independientes para diferentes marcas o regiones). Considere una vista de catálogo como *cómo* expone esos datos a una tienda, canal o audiencia.

* **[Capa de catálogo](catalog-layer.md)**: una capa aplicada sobre los datos del catálogo base para modificar los atributos del producto (nombre, descripción, imágenes, metadatos) sin cambiar los datos de origen. Utilice capas de catálogo cuando las diferencias deban afectar solo a la visualización de tiendas, no al descubrimiento de productos.

## Reglas y limitaciones

* Se crea una fuente de catálogo mediante la ingesta de un producto a través de la API de ingesta de datos. Consulte [Documentos de desarrolladores - Ingesta de datos](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/) para obtener más información.
* La exclusividad del producto viene determinada por el SKU + el origen del catálogo.
* Los compradores no acceden directamente a las fuentes del catálogo. Los datos del catálogo se exponen a la tienda a través de [vistas de catálogo](catalog-view.md).

## Guía de modelado

Siga estas directrices a la hora de decidir cómo estructurar los orígenes de catálogo:

* Cree un origen de catálogo independiente por cada idioma de catálogo diferente.
* Utilice orígenes de catálogo independientes cuando las diferencias de producto y atributo deban afectar al comportamiento de búsqueda, filtrado u ordenación (por ejemplo, una capacidad de búsqueda, filtrado o configuración de faceta diferentes para el mismo atributo).
* Use [capas de catálogo](catalog-layer.md) cuando las diferencias de producto y atributo deban afectar solamente la visualización de la tienda, no la detección de productos.

>[!MORELIKETHIS]
>
> * [Vistas de catálogo](catalog-view.md): configure vistas filtradas con precios sobre un origen de catálogo
> * [Capas de catálogo](catalog-layer.md): modifique la presentación del producto sin cambiar los datos de origen
> * [Directivas](policies.md) - Crear filtros basados en atributos para vistas de catálogo
> * [Libros de precios](pricebooks.md): administre estructuras de precios para diferentes segmentos de clientes
