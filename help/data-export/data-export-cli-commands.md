---
title: Sincronizar fuentes mediante la CLI de Commerce
description: Aprenda a utilizar los comandos de la interfaz de la línea de comandos para administrar fuentes y procesos para los servicios SaaS de  [!DNL data export extension] for Adobe Commerce.
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
source-git-commit: 37d5699315e34f1504602090fae5201ee51cf470
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Sincronizar fuentes mediante la CLI de Commerce

El comando `saas:resync` del paquete `magento/saas-export` le permite administrar la sincronización de datos para los servicios SaaS de Adobe Commerce.

Adobe no recomienda usar el comando `saas:resync` con regularidad. Los escenarios habituales para utilizar el comando son:

- Sincronización inicial
- Sincronizar datos a un nuevo espacio de datos después de cambiar el [ID de espacio de datos SaaS](https://experienceleague.adobe.com/es/docs/commerce-admin/config/services/saas)
- Resolución de problemas

Supervisar operaciones de sincronización en el archivo `var/log/saas-export.log`.

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

Consulte las secciones siguientes para ver descripciones de opciones con ejemplos.


>[!NOTE]
>
>Para obtener opciones avanzadas para administrar el procesamiento de exportación, consulte [Personalizar el procesamiento de exportación](customize-export-processing.md).

## `--by-ids`

Resincronizar parcialmente entidades específicas mediante sus ID. Admite fuentes de `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` y `categoryPermissions`.

De manera predeterminada, al usar la opción `--by-ids`, se especifican valores mediante los valores de SKU del producto. Para usar identificadores de producto, agregue la opción `--id-type=ProductID`.

**Ejemplos:**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed= products --by-ids='1,2,3' --id-type='productId'
```


## `--cleanup-feed`

Limpie la tabla del indexador de fuentes antes de reindexar y enviar datos a SaaS. Solo se admite para `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` y `categoryPermissions`.

Si se utiliza con la opción `--dry-run`, la operación realiza una operación de resincronización de ejecución en seco para todos los elementos.

>[!IMPORTANT]
>
>Use solo después de limpiar el entorno o con la opción `--dry-run`. Si se utiliza en otros casos, la operación de limpieza puede causar pérdida de datos y problemas de sincronización de datos.

**Ejemplo:**

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

**Ejemplo**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
```

## `--feed`

Requerido. Especifica la entidad de fuente que se va a resincronizar.

Fuentes disponibles:

- `categories`
- `categoryPermissions`
- `orders`
- `prices`
- `products`
- `productAttributes`
- `productOverrides`
- `scopesWebsite`
- `scopesCustomerGroup`
- `variants`

>[!NOTE]
>
>Las fuentes disponibles en su entorno pueden variar según los módulos que se instalen en el entorno de Adobe Commerce.

**Ejemplo:**

```shell
bin/magento saas:resync --feed products
```

## `--no-reindex`

Vuelve a enviar los datos del catálogo existente a [!DNL Commerce Services] sin volver a indexar. No compatible con fuentes relacionadas con productos.

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
