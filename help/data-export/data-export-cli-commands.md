---
title: Interfaz de línea de comandos de exportación de datos SaaS
description: Aprenda a utilizar los comandos de la interfaz de la línea de comandos para administrar fuentes y procesos para los servicios SaaS de  [!DNL data export extension] for Adobe Commerce.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# Referencia de la interfaz de la línea de comandos para la exportación de datos SaaS

Los desarrolladores y administradores de sistemas pueden administrar las operaciones de sincronización para la exportación de datos SaaS mediante la [herramienta de línea de comandos de Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI). El comando `saas:resync` está incluido en el paquete `magento/saas-export`.

Adobe no recomienda usar el comando `saas:resync` con regularidad. Los escenarios habituales para utilizar el comando son:

- La sincronización inicial
- Se cambió el [Id. de espacio de datos SaaS](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) y necesita sincronizar los datos con el nuevo espacio de datos.
- Resolución de problemas

## Sincronización inicial

>[!NOTE]
>Si utiliza Live Search o Product Recommendations, no necesita ejecutar la sincronización inicial. El proceso se inicia automáticamente después de conectar el servicio a la instancia de Commerce.

Al almacenar en déclencheur un(a) `saas:resync` desde la línea de comandos, según el tamaño del catálogo, los datos pueden tardar entre unos minutos y unas pocas horas en actualizarse.

Para la sincronización inicial, Adobe recomienda ejecutar los comandos en el siguiente orden:

```bash
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

## Ejemplos de comandos

Antes de usar `saas:resync` comandos, revise las [descripciones de opciones](#command-options).

- Realice una resincronización completa de una fuente de entidades.

  ```
  bin/magento saas:resync --feed='<FEED_NAME>' 1
  ```

  Las fuentes que ya se han exportado correctamente no se vuelven a sincronizar.

- Sincronizar completamente los datos de fuente y limpieza especificados

  ```
  bin/magento saas:resync --feed='FEED_NAME' --cleanup-feed
  ```

  Usar solo después de realizar una operación [!DNL Data Space ID Cleanup].

- Para las fuentes de exportación inmediatas, reenvíe todos los datos a servicios de Commerce conectados sin truncar los datos de índice de la tabla de fuentes

  ```
   bin/magento saas:resync --feed='FEED_NAME' --no-reindex
  ```

- Enumerar comandos y opciones disponibles con descripciones.

  ```
  bin/magento saas:resync --help
  ```

## Opciones de comando

Las siguientes opciones están disponibles para administrar `saas:resync` operaciones.

>[!NOTE]
>
>El comando `saas:resync` también admite opciones avanzadas para mejorar los comandos de exportación de datos al aumentar el tamaño del lote y agregar el procesamiento de varios subprocesos. Ver [Personalizar procesamiento de exportación](customize-export-processing.md).

### `feed`

Esta opción requerida especifica qué entidad de fuente se debe resincronizar, como `products`.

El valor de la opción `feed` puede incluir cualquiera de las fuentes de entidades disponibles:

- `products`: fuente de datos del producto
- `productAttributes`: fuente de datos de atributos del producto
- `categories`: fuente de datos de categorías
- `variants`: fuente de datos configurable de variaciones de productos
- `prices`: fuente de datos de precios del producto
- `categoryPermissions`: fuente de datos de permisos de categoría
- `productOverrides`: fuente de datos de permisos del producto
- `inventoryStockStatus`: fuente de datos de estado de existencias de inventario
- `scopesWebsite`: sitios web con tiendas y fuentes de datos de vistas de tiendas
- `scopesCustomerGroup`: fuente de datos de grupos de clientes
- `orders`: fuente de datos de pedidos de ventas

Según los [servicios de Commerce](../landing/saas.md) que estén instalados, es posible que tenga un conjunto diferente de fuentes disponibles para el comando `saas:resync`.

### `no-reindex`

Esta opción vuelve a enviar los datos del catálogo existentes a [!DNL Commerce Services] sin volver a indexar. Si no se especifica esta opción, el comando ejecuta una reindexación completa antes de sincronizar los datos.

El comportamiento de esta opción depende de si la fuente se exporta en [modo de exportación heredado o inmediato](data-synchronization.md#synchronization-modes)

- Para fuentes de exportación heredadas, el proceso de sincronización no trunca los datos indexados en la tabla de fuentes. En su lugar, vuelve a enviar todos los datos al servicio de Adobe Commerce.
- En el caso de las fuentes de exportación inmediatas, esta opción se ignora si se especifica. Para estas fuentes, el proceso de resincronización no trunca el índice y solo vuelve a sincronizar las actualizaciones o los elementos con errores anteriores.

### `cleanup`

Esta opción limpia la tabla del indizador de fuentes antes de una sincronización. Cuando se especifica, la exportación de datos de SaaS ejecuta una resincronización completa para la fuente especificada y limpia todos los datos existentes en la tabla de fuentes.

Adobe recomienda usar este comando solamente después de realizar la operación [!DNL Data Space ID Cleanup].

>[!WARNING]
>
>**No use esta opción con regularidad**. Puede provocar problemas de sincronización de datos en los servicios de Adobe Commerce. Por ejemplo, es posible que `delete product event` no se propague al servicio Adobe Commerce si se utiliza la opción `cleanup`.

## Resolución de problemas

Si no ve los datos esperados en los servicios de Commerce conectados, solucione los problemas comprobando los registros de errores de exportación de datos y utilizando el comando `saas:resync` con variables de entorno para revisar las cargas útiles y los datos del generador de perfiles. Ver [Revisar registros y solucionar problemas](troubleshooting-logging.md).
