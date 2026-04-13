---
title: Notas de la versión [!DNL SaaS Data Export Extension]
description: La información de la versión más reciente de  [!DNL Data Export Extension]  para Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
exl-id: 8ae51d3d-8c12-4607-b7e5-985033143a84
source-git-commit: 396ed02596d451f41cfb81e0da226d299f1f2bb7
workflow-type: tm+mt
source-wordcount: '2375'
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

## Versiones de 2026

### Versión 103.4.22

_10 de abril de 2026_

![Corrección](../assets/fix.svg) **Sincronización de datos mejorada**

- Se ha corregido un problema en el cual los productos eliminados no se eliminaban correctamente de los servicios de Commerce conectados si el servicio de exportación no estaba disponible durante la eliminación. Las operaciones de reintento y resincronización ahora garantizan que los productos eliminados se reflejen correctamente en el SaaS. <!--MDEE-1319-->
- Ahora, las entidades de catálogo (productos y categorías) se pueden exportar a los servicios conectados de Commerce aunque falten valores de atributo en la vista del almacén de administración. Esto mejora la compatibilidad con las extensiones de terceros y reduce los errores de exportación debido a la falta de valores predeterminados. <!--MDEE-1333-->

![Corrección](../assets/fix.svg) Se ha resuelto un error en la página Estado de sincronización de fuentes de datos que se podía producir cuando los registros de fuentes contenían datos inesperados o faltaban. El sistema ahora gestiona correctamente estos casos, mejorando la estabilidad y evitando bloqueos. Si está usando el conector de Adobe Commerce Optimizer para sincronizar datos de Adobe Commerce a Adobe Commerce Optimizer, actualice a [versión 1.0.11](https://experienceleague.adobe.com/en/docs/commerce/aco-optimizer-connector/release-notes) o posterior del conector de ACO para obtener la corrección.<!--MDEE-1327-->

### Versión 103.4.21

_2 de abril de 2026_

![Corrección](../assets/fix.svg) **Se ha mejorado la confiabilidad de la resincronización manual del indizador de permisos de categoría**-Se ha corregido un problema en el cual la ejecución de indizadores en un orden determinado podía hacer que algunos productos se volvieran invisibles temporalmente. El sistema ahora aplica el orden correcto y déclencheur automáticamente una resincronización completa cuando es necesario, lo que garantiza que todos los productos permanezcan visibles después de las operaciones manuales de reindexación. <!--MDEE-1332-->

### Versión 103.4.20

_5 de marzo de 2026_

![Corregir](../assets/fix.svg) Se aseguró la compatibilidad con futuras versiones de PHP al actualizar el proceso de índice de Fuente de productos para evitar el uso obsoleto de null como compensación de matriz. Esto mejora la estabilidad durante la indexación.<!--MDEE-1306-->

![Corrección](../assets/fix.svg) Se ha mejorado la sincronización de fuentes de productos para los datos de categoría. Ahora, al actualizar una dirección URL de categoría en la interfaz de usuario de administración de Commerce, la fuente de productos se actualiza automáticamente para reflejar la nueva ruta de categoría. No se requieren acciones manuales y los resultados de la búsqueda de productos siempre están actualizados después de un cambio de dirección URL de categoría.<!--MDEE-1294-->

### Versión 103.4.19

_6 de febrero de 2026_

![Corrección](../assets/fix.svg) ha resuelto un problema en el que el comando `di:compile` fallaba en PHP 8.5. El proceso de compilación ahora se completa correctamente, asegurando la compatibilidad con la última versión de PHP.<!--MDEE-1299-->

### Versión 103.4.18

_2 de febrero de 2026_

![Corrección](../assets/fix.svg) Se ha corregido un problema por el que los lotes de elementos podían superar el límite permitido durante las actualizaciones, lo que provocaba `items_limit_exceeded` errores al sincronizar datos con [servicios de Commerce](https://experienceleague.adobe.com/en/docs/commerce/user-guides/home) o [Adobe Commerce Optimizer](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync). <!--MDEE-1264-->

![Corrección](../assets/fix.svg): se ha mejorado la confiabilidad de las exportaciones de datos de productos al agregar lógica para registrar los elementos con errores durante la recopilación de opciones de productos del paquete. <!--CCSAAS-4458-->

### Versión 103.4.17

_5 de enero de 2026_

![Corrección](../assets/fix.svg) Se ha actualizado la extensión de exportación de datos (`magento/module-data-exporter`) para quitar la dependencia `magento/module-analytics`, que ya no es necesaria.<!--MDEE-1260-->

![Corregir](../assets/fix.svg) Se corrigió un problema en el cual al actualizar los precios de nivel de un producto no se eliminaban los valores antiguos, lo que daba como resultado entradas de precios de nivel duplicadas u obsoletas. Ahora, solo se muestran los precios de nivel actuales después de las actualizaciones. <!--MDEE-1157-->

![Corregir](../assets/fix.svg) Se corrigió un problema en el cual los productos con un precio de $0 o un descuento del 100% no se mostraban como gratuitos en la tienda. Los precios de las tiendas y del carro de compras ahora son coherentes. <!--MDEE-1159-->

![Se ha corregido](../assets/fix.svg) la compatibilidad con Symfony 7.4 LTS en las extensiones de exportación de datos para admitir futuras actualizaciones e integraciones. <!--MDEE-1272-->

## Versiones anteriores

### Versión 103.4.16

_24 de noviembre de 2025_

![Corrección](../assets/fix.svg) ha resuelto un problema en el que algunos indizadores no podían cambiar al modo `Update On Schedule` durante la instalación o actualización debido a la falta de implementaciones de ActionInterface en varios indizadores. Esta corrección garantiza una instalación y actualización correcta de la extensión sin encontrar errores relacionados con el indexador. <!--MDEE-1235-->

### Versión 103.4.15

_22 de octubre de 2025_

![Nuevo](../assets/new.svg) Se agregó compatibilidad con la extensión de estado de sincronización de fuentes de datos para supervisar y solucionar problemas de transferencias de datos de Adobe Commerce a servicios conectados (Servicio de catálogo, Live Search y Recomendaciones de productos). Para obtener más información sobre cómo instalar y usar esta extensión, consulte [Supervisión del estado de sincronización de fuentes de datos](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status.html) en la *Guía de administración de Commerce*. <!--MDEE-954-->

### Versión 103.4.14

_10 de octubre de 2025_

![Corrección](../assets/fix.svg) ha resuelto un problema en el que el trabajo de [indizador mview](https://developer.adobe.com/commerce/php/development/components/indexing/#mview) podría fallar si falta la tabla `cde_product_overrides_feed_cl`. La corrección garantiza una reindexación estable y evita errores de trabajos relacionados con esta tabla en entornos de varios inquilinos. <!--MDEE-1175-->

### Versión 103.4.13

_24 de septiembre de 2025_

![Corrección](../assets/fix.svg) Se ha corregido un problema por el cual al editar las opciones de configuración web se restablecía el índice de fuentes de productos. <!--MDEE-1154-->

![Corrección](../assets/fix.svg) Se ha resuelto un problema en el que las variantes y las opciones de productos agrupados podían aparecer varias veces en la respuesta del servicio de catálogo, especialmente en el caso de los productos asignados a varias tiendas o sitios web. Con esta corrección, cada opción/variante del paquete ahora se devuelve solo una vez por producto, lo que garantiza pantallas de tienda precisas y coherentes tanto para los comerciantes como para los clientes. <!--MDEE-1167-->

### Versión 103.4.12

_18 de septiembre de 2025_

![Corrección](../assets/fix.svg) Se ha corregido un problema por el que la página de detalles del producto (PDP) no mostraba descuentos en las reglas de precios de catálogo cuando había precios de grupos de clientes. El PDP ahora muestra correctamente el precio más bajo.<!--MDEE-1158-->

### Versión 103.4.11

_29 de agosto de 2025_

![Nuevo](../assets/new.svg) [!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."}
Se ha agregado compatibilidad con atributos de producto adicionales para incluir datos de clase de impuestos, juego de atributos e inventario de configuraciones de producto de Commerce en la fuente de productos. Los clientes que deseen incluir estos atributos en las fuentes de exportación de productos deben agregar el módulo Atributos de producto adicionales a su proyecto de Adobe Commerce. Ver [Agregar clase de impuestos, conjunto de atributos y atributos de inventario](add-tax-attribute-set-inventory-attributes.md).<!--MDEE-1135-->

![Corrección](../assets/fix.svg) ha resuelto un problema que provocaba una sincronización incorrecta de las actualizaciones de productos eliminadas si se producía un error durante un índice de productos completo. Ahora, todas las eliminaciones de productos se sincronizan correctamente incluso si se produce un error durante el proceso de indexación. <!--MDEE-1144-->

### Versión 103.4.10

_18 de agosto de 2025_

![Corrección](../assets/fix.svg) Se ha corregido un problema por el que se devolvía un tipo incorrecto (`text` en lugar de `OBJECT`) para algunos atributos creados dinámicamente Ahora, la información de tipo correcta se devuelve de forma coherente, lo que elimina la necesidad de realizar resincronizaciones manuales o soluciones alternativas.<!--MDEE-1131-->

![Corrección](../assets/fix.svg) Se ha corregido un problema por el que la recopilación de datos de productos durante las sincronizaciones parciales podía fallar debido a errores en el proveedor de inventario LowStock. Esta corrección garantiza que los datos del producto se exporten de forma fiable y que no se omitan los ID de producto debido a errores relacionados con LowStock.<!--MDEE-1132-->

### Versión 103.4.9

_13 de agosto de 2025_

![Corrección](../assets/fix.svg) Se ha corregido un problema por el que las fuentes de precios de productos no se regeneraban cuando se eliminaba un producto o cuando se cambiaba el SKU del producto.<!--MDEE-1125-->

![Corrección](../assets/fix.svg) Se mejoró el procesamiento de la actualización de productos para garantizar que los cambios se reflejen con precisión al actualizar un producto recién creado con el mismo SKU que un producto eliminado anteriormente. La sincronización de productos ahora utiliza correctamente los identificadores de producto actualizados, lo que garantiza una exportación de datos precisa y confiable.<!--MDEE-1126-->

![Corrección](../assets/fix.svg) Se ha corregido un problema en el que el servicio de catálogo podía devolver datos de variante obsoletos para productos configurables al garantizar que los eventos de actualización de productos se publiquen después de eliminaciones de atributos.<!--MDEE-1127-->

### Versión 103.4.8

_6 de agosto de 2025_

![Nuevo](../assets/new.svg) agregó información de precio de nivel a la fuente de precios. <!--MDEE-1070-->

![Corrección](../assets/fix.svg): La extensión del exportador de datos ahora exporta correctamente los precios de selección de paquetes con ámbito de sitio web, lo que garantiza que los precios de tienda reflejen valores precisos basados en la configuración &quot;Ámbito de precio de catálogo&quot;.<!--MDEE-1115-->

![Corrección](../assets/fix.svg) Anteriormente, los productos se sincronizaban con un estado `lowStock=true` incorrecto al usar Inventory management (Multi-source Inventory management) con la configuración de umbral. Este problema se ha corregido para garantizar la precisión en la creación de informes de existencias bajas.<!--MDEE-1113-->

### Versión 103.4.7

_22 de julio de 2025_

![Corrección](../assets/fix.svg) Se eliminaron tablas obsoletas que almacenaban permisos de categoría para productos. <!--MDEE-1065-->

### Versión 103.4.6

_20 de junio de 2025_

![Corrección](../assets/fix.svg): Exportar datos de productos descargables de Adobe Commerce con el atributo `ac_downloadable` para usarlos con Adobe Commerce Optimizer. <!--MDEE-1043-->

![Corrección](../assets/fix.svg) Corrección de errores de instalación críticos para Adobe Commerce versión 2.4.4. <!--MDEE-1074-->

### Versión 103.4.5

_27 de mayo de 2025_

![La nueva exportación de datos SaaS de ](../assets/new.svg) ahora es compatible con el tipo de producto Adobe Commerce `giftcard`. En la fuente de datos, los productos de tarjeta de regalo se exportan como productos simples con el tipo de atributo de producto `ac_giftcard`. <!--MDEE-1042-->

![Corrección](../assets/fix.svg): se mejoró el informe de errores de exportación de datos. Los registros ahora incluyen mensajes de error más detallados, incluidos detalles técnicos originales para facilitar la depuración y el seguimiento de errores. <!--MDEE-1064-->

### Versión 103.4.4

_15 de mayo de 2025_

![Nuevo](../assets/new.svg) Se ha agregado un mensaje de advertencia que aparece cuando se agrega el argumento `cleanup-feed` al comando CLI `saas:resync`. La opción `--cleanup-feed` debe usarse con precaución y solo en escenarios específicos como después de la limpieza del entorno o con la opción `--dry-run`. Su uso en otros casos puede provocar la pérdida de datos y problemas de sincronización. <!--MDEE-1047-->

![Corrección](../assets/fix.svg) agregó `x-request-id` desde la respuesta del servidor para mejorar la trazabilidad. <!--MDEE-1041-->

![Corrección](../assets/fix.svg) Se ha corregido un problema que impedía guardar el estado de sincronización para todo el lote de fuentes y que provocaba una resincronización innecesaria. <!--MDEE-1049-->

![Corrección](../assets/fix.svg) Se ha corregido un problema por el que todas las fuentes del lote de fuentes se omitían durante la sincronización si una fuente contenía un error. <!--MDEE-976-->

![Corrección](../assets/fix.svg) Se agregó compatibilidad con dimensiones en el indizador de permisos de categoría. <!--MDEE-654-->

### Versión 103.4.3

_22 de abril de 2025_

![Corrección](../assets/fix.svg) ha resuelto un problema por el que los productos se omitían durante el proceso de exportación de datos debido a la falta de atributos EAV. <!--MDEE-970-->

### Versión 103.4.2

_16 de abril de 2025_

![Corrección](../assets/fix.svg) agregó la capacidad de recopilar cargas útiles de entidad en `saas-export.log` al ejecutar la resincronización de prueba mediante el comando `saas:resync --dry-run` con la variable de entorno `EXPORTER_EXTENDED_LOG=1`. <!--MDEE-1023-->

### Versión 103.4.1

_10 de abril de 2025_

![Corrección](../assets/fix.svg) Se agregó un prefijo a las claves de caché de QueryXml para evitar conflictos de nomenclatura con otros módulos. <!--MDEE-1019-->

### Versión 103.4.0

_31 de marzo de 2025_

![Corrección](../assets/fix.svg): La fuente de invalidaciones del producto ya no envía permisos si el producto no está asignado a una categoría.<!--MDEE-449-->

### Versión 103.3.21

_11 de marzo de 2025_

![Se ha agregado la funcionalidad ](../assets/new.svg) para sincronizar parcialmente las fuentes de `products`, `productOverrides` y `productAttributes` en función de una lista especificada de SKU de productos. Use la nueva funcionalidad agregando la opción `--by-ids` al comando resincronizar CLI: <!--MDEE-606-->

```shell
bin/magento saas:resync --feed=<FEED_NAME> --by-ids='<SKU1>,<SKU2>,<SKU3>
```

![Corrección](../assets/fix.svg) Se han reducido los posibles problemas de compatibilidad con PHP 8.4 al abordar la funcionalidad obsoleta. <!--MDEE-1002-->

### Versión 103.3.20

_28 de febrero de 2025_

![Corregir](../assets/fix.svg) Se corrigieron `BulkException` errores no rastreables en `cron.log` al mejorar la mensajería para errores relacionados con errores de trabajos cron de exportación de datos de catálogo.<!--MDEE-966-->

![Corrección](../assets/fix.svg) Se mejoró el rendimiento del proceso de resincronización del producto en instancias con un número elevado de vistas de tienda. <!--MDEE-974-->

### Versión 103.3.19

_13 de febrero de 2025_

![Corrección](../assets/fix.svg) Se ha actualizado la extensión de exportación de datos para mejorar la extensibilidad de las fuentes. <!--MDEE-936-->

![Corrección](../assets/fix.svg) El procesador de exportación de datos ahora comprueba el estado del indizador antes de una resincronización completa para evitar la pérdida accidental de datos en la tabla de fuentes.

### Versión 103.3.18

_28 de enero de 2025_

![Corrección](../assets/fix.svg) Las actualizaciones de ensayo para entidades de producto y categoría ahora se activan correctamente en las actualizaciones de datos de exportación de datos.<!--MDEE-963-->

### Versión 103.3.17

_20 de enero de 2025_

![Corrección](../assets/fix.svg) Se agregó compatibilidad con PHP 8.4. <!--MDEE-941-->

### Versión 103.3.16

_6 de enero de 2025_

![Corrección](../assets/fix.svg): los valores de opción pueden estar vacíos para los productos configurables en varias vistas de tienda. <!--MDEE-926-->

### Versión 103.3.15

_12 de diciembre de 2024_

![Corregir](../assets/fix.svg) Se garantizó el funcionamiento estable de las pruebas de integración en configuraciones anteriores. <!--MDEE-869-->

![Corregir](../assets/fix.svg) Dejar de propagar opciones de atributos innecesarias. <!--MDEE-882-->

![Corrección](../assets/fix.svg) Se corrigió el mensaje de error enviado al registro de exportación de datos cuando falla la serialización de datos. <!--MDEE-913-->

![Corrección](../assets/fix.svg) mejoró la confiabilidad de las actualizaciones de productos simples con cobertura de prueba adicional. <!--MDEE-886-->

### Versión 103.3.14

_8 de octubre de 2024_

![Corrección](../assets/fix.svg) El indizador de exportador ahora mantiene el estado correcto para indizadores dependientes. Anteriormente, estos índices se invalidaban incorrectamente y requerían comprobaciones y validaciones adicionales que ralentizaban el rendimiento de la indexación. <!--MDEE-866-->

### Versión 103.3.13

_1 de octubre de 2024_

![Corrección](../assets/fix.svg) Se mejoró el rendimiento del proceso de sincronización de datos al agregar una caché local para los datos de opciones de atributos.<!--MDEE-864-->

### Versión 103.3.12

_25 de septiembre de 2024_

![Corregir](../assets/fix.svg) se ha resuelto un problema que incrementaba el tiempo de sincronización de productos simples y virtuales. <!--MDEE-861-->

### Versión 103.3.11

_9 de septiembre de 2024_

![Corrección](../assets/fix.svg): El servicio de exportación de datos ahora envía datos de precios especiales para productos agrupados como porcentaje, corrigiendo un problema anterior en el que se enviaba como precio final. <!--MDEE-854-->

![Corrección](../assets/fix.svg) Se ha actualizado la implementación del monólogo por compatibilidad con Monolog 3. <!--MDEE-858-->

### Versión 103.3.10

_26 de agosto de 2024_

![Corregir](../assets/fix.svg) Se ha corregido el filtrado de vista de tienda múltiple para la fuente de opciones personalizadas del producto. <!--MDEE-842-->

![Corregir](../assets/fix.svg) Las fuentes no válidas no se vuelven a enviar hasta que cambie el valor hash de la fuente.<!--MDEE-848-->

### Versión 103.3.9

_22 de julio de 2024_

![Corrección](../assets/fix.svg) Cuando se elimina una entidad, el indicador `deleted` ahora se propaga para las fuentes de servicios de ámbito del sitio web (`scopesWebsite`) y el grupo de clientes (`scopesCustomerGroup`).<!--MDEE-839-->

### Versión 103.3.8

_17 de julio de 2024_

![Corregir](../assets/fix.svg) Las opciones de configuración deshabilitadas ya no se exportan como opciones activas.<!--MDEE-812-->

![Corregir](../assets/fix.svg) Las opciones y los valores ahora se actualizan en un producto configurable cuando se realizan cambios en un producto secundario. <!--MDEE-835-->

![Nuevo](../assets/new.svg) agregó la capacidad de incluir datos de atributos del sistema adicionales en la fuente de atributos del producto.

### Versión 103.3.7

_25 de junio de 2024_

![Corrección](../assets/fix.svg) eliminó dependencias innecesarias del módulo InventoryDataExporter.

![Corrección](../assets/fix.svg) Se han cambiado las versiones necesarias para los módulos de inventario incluidos en el módulo CatalogInventoryDataExporter para que sean compatibles con la versión 2.4.4 de Adobe Commerce.

### Versión 103.3.6

_20 de junio de 2024_

![Corregir](../assets/fix.svg) Se corrigieron interbloqueos que se producían durante la reindexación de fuentes en modo multiproceso. Las consultas ahora se separan en operaciones Insert y Update.

![Corrección](../assets/fix.svg) optimizó la consulta de precios para catálogos grandes con muchos sitios web.

![Nuevo](../assets/new.svg) agregó lógica de reintento para volver a ejecutar las transacciones fallidas cuando se producen interbloqueos.

### Versión 103.3.5

_5 de junio de 2024_

![Corregir](../assets/fix.svg) Establecer dependencia para la última versión de exportación de datos compatible para el módulo común SaaS.

![Corrección](../assets/fix.svg) reemplazó la instancia `ScopeConfig` con `ServiceConfigInterface` para admitir configuraciones de servicio diferentes.

### Versión 103.3.4

_31 de mayo de 2024_

![Se ha agregado compatibilidad con el registro de auditoría de transferencia de datos al agregar un mecanismo para enviar un evento ](../assets/fix.svg) cada vez que se transmiten datos de la instancia de Commerce a un servicio de Commerce. `data_sent_outside`<!--MDEE-785-->

### Versión 103.3.3

_21 de mayo de 2024_

La exportación de datos de ![New](../assets/new.svg) SaaS ahora almacena en caché los atributos Entity-Attribute-Value (EAV) para la consulta de metadatos de atributos.

![Corrección](../assets/fix.svg) Se ha corregido un problema por el que la fuente `InventoryStockStatus` no se guardaba durante el reintento si se eliminaba el producto.

### Versión 103.3.2

_14 de mayo de 2024_

![Corrección](../assets/fix.svg) Se ha corregido un problema por el que faltaba el campo `modifiedAt` en las fuentes de entidades eliminadas.

### Versión 103.3.1

_8 de mayo de 2024_

![Corrección](../assets/fix.svg) Se ha corregido un problema que hacía que apareciera un mensaje de `Invalid Template File` durante la reindexación de fuentes de productos cuando se instalaba Page Builder.

### Versión 103.3.0

_30 de abril de 2024_

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

- nombres de tabla de registro de cambios: sigue el mismo patrón de nomenclatura que las tablas de fuentes, pero los nombres de tabla de registro de cambios agregan un sufijo `_cl`. Por ejemplo `catalog_data_exporter_products_cl`-> `cde-products_feed_cl`

Si tiene código personalizado que hace referencia a cualquiera de estas entidades, actualice las referencias con los nuevos nombres para asegurarse de que el código sigue funcionando correctamente.

![Corrección](../assets/fix.svg) Establezca el campo `modified_at` en los datos de fuente solo para las fuentes que lo requieran.

![Corrección](../assets/fix.svg) Modifique la consulta `productAttributes` para recuperar únicamente atributos de producto.

### Versión 103.2.6

_23 de abril de 2024_

![Corrección](../assets/fix.svg) Se ha corregido un problema que impedía que las fuentes se reindexaran cuando las tablas tienen un prefijo.

### Versión 103.2.5

_19 de abril de 2024_

![Corrección](../assets/fix.svg) optimizó la consulta Precio.

### Versión 103.2.4

_12 de abril de 2024_

![Corrección](../assets/fix.svg) Se ha corregido un estado de Stock incorrecto que se mostraba para un producto cuando Commerce Inventory management está habilitado.

### Versión 103.2.3

_3 de abril de 2024_

![Corregir](../assets/fix.svg) precio especial fijo a nivel de sitio web.

![Corregir](../assets/fix.svg) exclusión mutua agregada para todas las fuentes que se procesan.

### Versión 103.2.2

_14 de marzo de 2024_

![Corrección](../assets/fix.svg): se ha mejorado la estrategia de agrupamiento de fuentes para catálogos grandes. La tabla de lotes ahora se rellena con un número limitado de ID para reducir el uso de memoria.

![Corrección](../assets/fix.svg): se ha eliminado la dependencia de hardware de CommerceInventoryDataExporter a los módulos MSI.

![Corrección](../assets/fix.svg) mejoró `commerce-data-exporter` registros para recopilar más información y organizar por diferentes fases de exportación.

### Versión 103.2.1

_5 de marzo de 2024_

- Versión actualizada publicada.

### Versión 103.2.0

_21 de febrero de 2024_

- Se ha agregado la sincronización de datos multiproceso para productos y precios.


