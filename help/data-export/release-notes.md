---
title: Notas de la versión [!DNL SaaS Data Export Extension]
description: La información de la versión más reciente de  [!DNL Data Export Extension]  para Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
exl-id: 8ae51d3d-8c12-4607-b7e5-985033143a84
source-git-commit: bb9300c621ceac618c51e4dd787527ac1e960dd8
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 0%

---

# Notas de la versión de la extensión [!DNL SaaS Data Export]

Estas notas de la versión describen las versiones más recientes de la extensión [!DNL SaaS data export]. Se proporciona soporte para la versión publicada principal actual. Las notas de la versión de las versiones anteriores se proporcionan como referencia.

Las actualizaciones incluyen:

![Nuevas](../assets/new.svg) nuevas características
![Corrección](../assets/fix.svg) Correcciones y mejoras
![Error](../assets/bug.svg) Problemas conocidos


>[!NOTE]
>
>La extensión de exportación de datos SaaS es una colección de módulos que se instalan automáticamente con Live Search, Product Recommendations y el servicio de catálogo. Puede comprobar la versión instalada en su sistema con Composer. En algunos casos, es posible que desee actualizar la extensión de exportación de datos en el sistema para recoger correcciones o nuevas funciones sin actualizar la versión del servicio de Commerce.

## Versión principal actual

## Versión 103.4.2

![Corrección](../assets/fix.svg) agregó la capacidad de recopilar cargas útiles de entidad en `saas-export.log` al ejecutar la resincronización de prueba mediante el comando `saas:resync --dry-run` con la variable de entorno `EXPORTER_EXTENDED_LOG=1`. <!--MDEE-1023-->

## Versión 103.4.1

![Corrección](../assets/fix.svg) Se agregó un prefijo a las claves de caché de QueryXml para evitar conflictos de nomenclatura con otros módulos. <!--MDEE-1019-->

## Versión 103.4.0

![Corrección](../assets/fix.svg): La fuente de invalidaciones del producto ya no envía permisos si el producto no está asignado a una categoría.<!--MDEE-449-->

## Versión 103.3.21

![Corrección](../assets/new.svg) Se ha agregado funcionalidad para sincronizar parcialmente las fuentes `products`, `productOverrides` y `productAttributes` en función de una lista especificada de SKU de productos. Use la nueva funcionalidad agregando la opción `--by-ids` al comando resincronizar CLI: <!--MDEE-606-->

```shell
bin/magento saas:resync --feed=<FEED_NAME> --by-ids='<SKU1>,<SKU2>,<SKU3>
```

![Corrección](../assets/fix.svg) Se han reducido los posibles problemas de compatibilidad con PHP 8.4 al abordar la funcionalidad obsoleta. <!--MDEE-1002-->

## Versión 103.3.20

![Corregir](../assets/fix.svg) Se corrigieron `BulkException` errores no rastreables en `cron.log` al mejorar la mensajería para errores relacionados con errores de trabajos cron de exportación de datos de catálogo.<!--MDEE-966-->
![Corrección](../assets/fix.svg): se ha mejorado el rendimiento del proceso de resincronización del producto en instancias con un número elevado de vistas de tienda. <!--MDEE-974-->

## Versión 103.3.19

![Corrección](../assets/fix.svg) Se ha actualizado la extensión de exportación de datos para mejorar la extensibilidad de las fuentes. <!--MDEE-936-->
![Corrección](../assets/fix.svg): el procesador de exportación de datos ahora verifica el estado del indizador antes de una resincronización completa para evitar la pérdida accidental de datos en la tabla de fuentes.

## Versión 103.3.18

![Corrección](../assets/fix.svg) Las actualizaciones de ensayo para entidades de producto y categoría ahora se activan correctamente en las actualizaciones de datos de exportación de datos.<!--MDEE-963-->

## Versión 103.3.17

![Corrección](../assets/fix.svg) Se agregó compatibilidad con PHP 8.4. <!--MDEE-941-->

## Versión 103.3.16

![Corrección](../assets/fix.svg): los valores de opción pueden estar vacíos para los productos configurables en varias vistas de tienda. <!--MDEE-926-->

## Versión 103.3.15

![Corregir](../assets/fix.svg) Se garantizó el funcionamiento estable de las pruebas de integración en configuraciones anteriores. <!--MDEE-869-->
![Corregir](../assets/fix.svg) Dejar de propagar opciones de atributos innecesarias. <!--MDEE-882-->
![Corregir](../assets/fix.svg) Se corrigió el mensaje de error enviado al registro de exportación de datos cuando falla la serialización de datos. <!--MDEE-913-->
![Corrección](../assets/fix.svg) mejoró la confiabilidad de simples actualizaciones de productos con cobertura de prueba adicional. <!--MDEE-886-->

## Versión 103.3.14

![Corrección](../assets/fix.svg) El indizador de exportador ahora mantiene el estado correcto para indizadores dependientes. Anteriormente, estos índices se invalidaban incorrectamente y requerían comprobaciones y validaciones adicionales que ralentizaban el rendimiento de la indexación. <!--MDEE-866-->

## Versión 103.3.13

![Corrección](../assets/fix.svg) Se mejoró el rendimiento del proceso de sincronización de datos al agregar una caché local para los datos de opciones de atributos.<!--MDEE-864-->

## Versión 103.3.12

![Corregir](../assets/fix.svg) se ha resuelto un problema que incrementaba el tiempo de sincronización de productos simples y virtuales. <!--MDEE-861-->

## Versión 103.3.11

![Corrección](../assets/fix.svg): El servicio de exportación de datos ahora envía datos de precios especiales para productos agrupados como porcentaje, corrigiendo un problema anterior en el que se enviaba como precio final. <!--MDEE-854-->
![Corrección](../assets/fix.svg) Se ha actualizado la implementación del monólogo por compatibilidad con Monolog 3. <!--MDEE-858-->

## Versión 103.3.10

![Corregir](../assets/fix.svg) Se ha corregido el filtrado de vista de tienda múltiple para la fuente de opciones personalizadas del producto. <!--MDEE-842-->
![Corregir](../assets/fix.svg) las fuentes no válidas no se vuelven a enviar hasta que cambie el valor hash de la fuente.<!--MDEE-848-->

## Versión 103.3.9

![Corrección](../assets/fix.svg) Cuando se elimina una entidad, el indicador `deleted` ahora se propaga para las fuentes de servicios de ámbito del sitio web (`scopesWebsite`) y el grupo de clientes (`scopesCustomerGroup`).<!--MDEE-839-->

## Versión 103.3.8

![Corregir](../assets/fix.svg) Las opciones de configuración deshabilitadas ya no se exportan como opciones activas.<!--MDEE-812-->
![Corregir](../assets/fix.svg) Las opciones y los valores ahora se actualizan en un producto configurable cuando se realizan cambios en un producto secundario. <!--MDEE-835-->
![Nuevo](../assets/new.svg) agregó la capacidad de incluir datos de atributos del sistema adicionales en la fuente de atributos del producto.

## Versión 103.3.7

![Corrección](../assets/fix.svg) eliminó dependencias innecesarias del módulo InventoryDataExporter.
![Corrección](../assets/fix.svg) Se han cambiado las versiones necesarias para los módulos de inventario incluidos en el módulo CatalogInventoryDataExporter para que sean compatibles con la versión 2.4.4 de Adobe Commerce.

## Versión 103.3.6

![Corregir](../assets/fix.svg) Se corrigieron interbloqueos que se producían durante la reindexación de fuentes en modo multiproceso. Las consultas ahora se separan en operaciones Insert y Update.
![Corrección](../assets/fix.svg) optimizó la consulta de precios para catálogos grandes con muchos sitios web.
![Nuevo](../assets/new.svg) agregó lógica de reintento para volver a ejecutar las transacciones fallidas cuando se producen interbloqueos.

## Versión 103.3.5

![Corregir](../assets/fix.svg) Establecer dependencia para la última versión de exportación de datos compatible para el módulo común SaaS.

![Corrección](../assets/fix.svg) reemplazó la instancia `ScopeConfig` con `ServiceConfigInterface` para admitir configuraciones de servicio diferentes.

## Versión 103.3.4

![Se ha agregado compatibilidad con el registro de auditoría de transferencia de datos al agregar un mecanismo para enviar un evento `data_sent_outside` cada vez que se transmiten datos de la instancia de Commerce a un servicio de Commerce <!--MDEE-785-->](../assets/fix.svg)

## Versión 103.3.3

La exportación de datos de ![New](../assets/new.svg) SaaS ahora almacena en caché los atributos Entity-Attribute-Value (EAV) para la consulta de metadatos de atributos.

![Corrección](../assets/fix.svg) Se ha corregido un problema por el que la fuente `InventoryStockStatus` no se guardaba durante el reintento si se eliminaba el producto.

## Versión 103.3.2

![Corrección](../assets/fix.svg) Se ha corregido un problema por el que faltaba el campo `modifiedAt` en las fuentes de entidades eliminadas.

## Versión 103.3.1

![Corrección](../assets/fix.svg) Se ha corregido un problema que hacía que apareciera un mensaje de `Invalid Template File` durante la reindexación de fuentes de productos cuando se instalaba Page Builder.

## Versión 103.3.0

![Nuevo](../assets/new.svg) migró tablas de fuentes de exportación inmediatas a la estructura unificada:
`id`, `source_entity_id`, `feed_id`, `modified_at`, `is_deleted`, `status`, `feed_data`, `feed_hash`, `errors`

![Nuevo](../assets/new.svg) ha migrado fuentes de inventario y catálogo a la solución de exportación inmediata.

![Nuevo](../assets/new.svg) Se cambió el nombre de los trabajos cron de la fuente de exportación inmediata a `*_feed_resend_failed_items`.

![Nuevo](../assets/new.svg): se ha cambiado el nombre de las fuentes de exportación inmediatas, los identificadores de vista de indizador y las tablas de registro de cambios.
- tablas de fuentes (e ID de vistas de indizador):
   - `catalog_data_exporter_products` -> `cde_products_feed`
   - `catalog_data_exporter_product_attributes` -> `cde_product_attributes_feed`
   - `catalog_data_exporter_categories` -> `cde_categories_feed`
   - `catalog_data_exporter_product_prices` -> `cde_product_prices_feed`
   - `catalog_data_exporter_product_variants` -> `cde_product_variants_feed`
   - `inventory_data_exporter_stock_status` -> `inventory_data_exporter_stock_status_feed`
- nombres de tabla de registro de cambios: sigue el mismo patrón de nomenclatura que las tablas de fuentes, pero los nombres de tabla de registro de cambios agregan un sufijo `_cl`.  Por ejemplo `catalog_data_exporter_products_cl`-> `cde-products_feed_cl`
Si tiene código personalizado que hace referencia a cualquiera de estas entidades, actualice las referencias con los nuevos nombres para asegurarse de que el código sigue funcionando correctamente.

![Corrección](../assets/fix.svg) Establezca el campo `modified_at` en los datos de fuente solo para las fuentes que lo requieran.

![Corrección](../assets/fix.svg) Modifique la consulta `productAttributes` para recuperar únicamente atributos de producto.

## Versión 103.2.6

![Corrección](../assets/fix.svg) Se ha corregido un problema que impedía que las fuentes se reindexaran cuando las tablas tienen un prefijo.

## Versión 103.2.5

![Corrección](../assets/fix.svg) optimizó la consulta Precio.

## Versión 103.2.4

![Corrección](../assets/fix.svg) Se ha corregido un estado de Stock incorrecto que se mostraba para un producto cuando Commerce Inventory management está habilitado.

## Versión 103.2.3

![Corregir](../assets/fix.svg) precio especial fijo a nivel de sitio web.
![Corregir](../assets/fix.svg) exclusión mutua agregada para todas las fuentes que se procesan.


## Versión 103.2.2

![Corrección](../assets/fix.svg): se ha mejorado la estrategia de agrupamiento de fuentes para catálogos grandes. La tabla de lotes ahora se rellena con un número limitado de ID para reducir el uso de memoria.

![Corrección](../assets/fix.svg): se ha eliminado la dependencia de hardware de CommerceInventoryDataExporter a los módulos MSI.

![Corrección](../assets/fix.svg) mejoró `commerce-data-exporter` registros para recopilar más información y organizar por diferentes fases de exportación.

## Versión 103.2.1

- Versión actualizada publicada.

## Versión 103.2.0

- Se ha agregado la sincronización de datos multiproceso para productos y precios.
