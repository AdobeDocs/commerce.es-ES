---
title: Sync feeds using the Commerce CLI
description: Learn how to use the command-line interface commands to manage feeds and processes for the [!DNL data export extension] for Adobe Commerce SaaS services.
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
source-git-commit: 8233b2e184c8af293ffc41cb22e085388cf18049
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Sync feeds using the Commerce CLI

El comando `saas:resync` del paquete `magento/saas-export` le permite administrar la sincronización de datos para los servicios SaaS de Adobe Commerce.

Adobe does not recommend using the `saas:resync` command regularly. Typical scenarios for using the command are:

- Initial sync
- Sync data to a new data space after changing the [SaaS Data Space ID](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)
- Resolución de problemas

Monitor sync operations in the `var/log/saas-export.log` file.

## Sincronización inicial

>[!NOTE]
>
>La sincronización inicial se ejecuta automáticamente cuando Live Search o Product Recommendations están habilitados. No se necesitan comandos manuales.

Al almacenar en déclencheur un(a) `saas:resync` desde la línea de comandos, según el tamaño del catálogo, los datos pueden tardar entre unos minutos y unas pocas horas en actualizarse.

Para la sincronización inicial, Adobe recomienda ejecutar los comandos en el siguiente orden:

```shell
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

## Sincronizar mediante comandos CLI

El comando `saas:resync` admite varias operaciones de sincronización:

- Sincronización parcial por SKU
- Reanudar sincronizaciones interrumpidas
- Validar datos sin sincronizar

Ver todas las opciones disponibles:

```shell
bin/magento saas:resync --help
```

See the following sections for option descriptions with examples.


>[!NOTE]
>
>For advanced options to manage export processing, see [Customize export processing](customize-export-processing.md).

## `--by-ids`

Partially resync specific entities by their IDs. Supports `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants`, and `categoryPermissions` feeds.

De manera predeterminada, al usar la opción `--by-ids`, se especifican valores mediante los valores de SKU del producto. To use product IDs instead, add the `--id-type=ProductID` option.

**Ejemplos:**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed= products --by-ids='1,2,3' --id-type='productId'
```


## `--cleanup-feed`

Clean up the feed indexer table before reindexing and sending data to SaaS. Only supported for `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants`, and `categoryPermissions`.

If used with the `--dry-run` option, the operation performs a dry-run resync operation for all items.

>[!IMPORTANT]
>
>Use only after environment cleanup, or with the `--dry-run` option. If used in other cases, the cleanup operation can cause data loss and data sync issues.

**Example:**

```shell
bin/magento saas:resync --feed products --cleanup-feed
```

## `--continue-resync`

Reanuda una operación de resincronización interrumpida. Solo se admite para las fuentes `products`, `productAttributes` y `productOverrides`.

**Ejemplo:**

```shell
bin/magento saas:resync --feed productAttributes --continue-resync
```

## `--dry-run`

Ejecuta el proceso de reindexación de fuentes sin enviar la fuente a SaaS y sin guardar en la tabla de fuentes. Esta opción es útil para identificar cualquier problema con el conjunto de datos.

Agregue la variable de entorno `EXPORTER_EXTENDED_LOG=1` para guardar la carga útil en `var/log/saas-export.log`.

**Ejemplo:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run
```

### Probar elementos de fuente específicos

Pruebe elementos de fuentes específicos agregando la opción `--by-ids` con la colección de registros extendida para ver la carga útil generada en el archivo `var/log/saas-export.log`.

**Ejemplo:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run --by-ids='ADB102,ADB111,ADB112'
```

### Probar todos los elementos de fuente

De manera predeterminada, la fuente enviada durante una operación de `resync --dry-run` incluye solo elementos nuevos o elementos que no se pudieron exportar anteriormente. Para incluir todos los elementos en la fuente que se va a procesar, use la opción `--cleanup-feed`.

**Example**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
```

## `--feed`

Required. Specifies the feed entity to resync.

Available feeds:

- `categories`
- `categoryPermissions`
- `inventoryStockStatus`
- `orders`
- `prices`
- `products`
- `productAttributes`
- `productOverrides`
- `scopesWebsite`
- `scopesCustomerGroup`
- `variants`

**Example:**

```shell
bin/magento saas:resync --feed products
```

## `--no-reindex`

Vuelve a enviar los datos del catálogo existente a [!DNL Commerce Services] sin volver a indexar. Not supported for product-related feeds.

El comportamiento varía según el [modo de exportación](data-synchronization.md#synchronization-modes):

- Modo heredado: vuelve a enviar todos los datos sin truncarlos.
- Modo inmediato: la opción se ignora, solo sincroniza actualizaciones/errores.

**Ejemplo:**

```shell
bin/magento saas:resync --feed productAttributes --no-reindex
```

## `--id-type=ProductId`

De forma predeterminada, las entidades especificadas cuando utiliza el comando `saas:resync feed` con la opción `--by-ids` se especifican mediante el SKU del producto. Utilice la opción `--id-type=ProductId` para especificar entidades por ID de producto.

```shell
bin/magento saas:resync --feed products --by-ids='1,2,3' --id-type='productId'
```

**Ejemplo:**

## Resolución de problemas

Si no ve los datos esperados en los servicios de Commerce conectados, solucione los problemas comprobando los registros de errores de exportación de datos y utilizando el comando `saas:resync` con variables de entorno para revisar las cargas útiles y los datos del generador de perfiles. Ver [Revisar registros y solucionar problemas](troubleshooting-logging.md).
