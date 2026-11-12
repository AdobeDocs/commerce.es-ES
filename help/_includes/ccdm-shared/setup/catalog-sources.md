---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%
---
Los orígenes de catálogo representan ámbitos autorizados de productos, atributos y categorías. Suelen asignarse a los límites del idioma, la audiencia o el sistema de origen y determinan el comportamiento de búsqueda, filtrado y ordenación.

## Fuentes de catálogo frente a conceptos relacionados

Comprender cómo se relacionan las fuentes de catálogo con otros conceptos de servicios de comercialización le ayuda a modelar los datos correctamente:

* **Origen del catálogo**: el contexto de datos subyacente que proporciona información del producto. Un origen de catálogo suele representar una configuración regional (por ejemplo, `en-US`, `fr-CA`) o un contexto de datos proporcionado por un sistema externo como un PIM o ERP. Los productos, los metadatos de atributos y las categorías se clasifican por origen de catálogo. Un origen de catálogo define el origen de los datos del catálogo sin procesar y su efecto en la detección de productos (resultados de búsqueda, filtrado y comportamiento de ordenación).

* **[Vista de catálogo](/help/optimizer/setup/catalog-view.md)**: una vista configurada del catálogo para una necesidad comercial específica. Una vista de catálogo selecciona orígenes de catálogo (o configuración regional), aplica [directivas](/help/optimizer/setup/policies.md) para filtrar la visibilidad de los productos y asocia [libros de precios](/help/optimizer/setup/pricebooks.md) a la vista. Un solo origen de catálogo puede activar muchas vistas de catálogo (por ejemplo, un origen de `en-US` con vistas de catálogo independientes para diferentes marcas o regiones). Considere una vista de catálogo como *cómo* expone esos datos a una tienda, canal o audiencia.

* **[Capa de catálogo](catalog-layer.md)**: una capa aplicada sobre los datos del catálogo base para modificar los atributos del producto (nombre, descripción, imágenes, metadatos) sin cambiar los datos de origen. Utilice capas de catálogo cuando las diferencias deban afectar solo a la visualización de tiendas, no al descubrimiento de productos.

## Cómo se rellenan los orígenes de catálogo

Las fuentes de catálogo se rellenan mediante la ingesta de datos de catálogo. La forma de proporcionar esos datos depende de la implementación:

- **Adobe Commerce as a Cloud Service con CCDM**: la sincronización nativa proporciona datos de catálogo de Commerce Foundation. Administre los productos subyacentes y la configuración de vista de tienda en Commerce Foundation y supervise la sincronización en el espacio de trabajo [Sincronización de datos](data-sync.md). No se requiere una integración de API de ingesta de datos independiente.
- **Adobe Commerce Optimizer con un servidor de terceros**: su integración proporciona productos e información de la fuente del catálogo a través de la [API de ingesta de datos](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/).


## Reglas y limitaciones

* Se crea un origen de catálogo cuando la capa de datos de Servicios de comercialización recibe por primera vez los datos de catálogo de una nueva configuración regional o sistema de origen.
* La exclusividad del producto viene determinada por el SKU + el origen del catálogo.
* Los compradores no acceden directamente a las fuentes del catálogo. Los datos del catálogo se exponen a la tienda a través de [vistas de catálogo](catalog-view.md).

## Guía de modelado

Siga estas directrices a la hora de planificar la estructura del catálogo. Para Adobe Commerce as a Cloud Service con CCDM, administre la configuración subyacente en Commerce Foundation en lugar de crear fuentes de catálogo a través de una integración de ingesta independiente.

* Utilice un origen de catálogo independiente para cada idioma de catálogo.
* Utilice orígenes de catálogo independientes cuando las diferencias de productos y atributos deban afectar al comportamiento de búsqueda, filtrado u ordenación, como diferentes configuraciones de búsqueda o filtrado.
* Use [capas de catálogo](catalog-layer.md) cuando las diferencias de producto y atributo deban afectar a la presentación del producto sin cambiar el comportamiento de búsqueda, filtrado u ordenación.

>[!MORELIKETHIS]
>
> * [Vistas de catálogo](catalog-view.md): configure vistas filtradas con precios sobre un origen de catálogo
> * [Capas de catálogo](catalog-layer.md): modifique la presentación del producto sin cambiar los datos de origen
> * [Directivas](policies.md) - Crear filtros basados en atributos para vistas de catálogo
> * [Libros de precios](/help/optimizer/setup/pricebooks.md): administre estructuras de precios para diferentes segmentos de clientes
> * [Claves de acceso restringido](restricted-access-keys.md): proteja una vista de catálogo con autenticación de token firmado
