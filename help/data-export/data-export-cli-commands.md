---
title: Sincronizar fuentes mediante la CLI de Commerce
description: Aprenda a utilizar los comandos de la interfaz de la línea de comandos para administrar fuentes y procesos para los servicios SaaS de  [!DNL data export extension] for Adobe Commerce.
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
source-git-commit: 086a571b69e8ad76a912c339895409b0037642b9
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# Sincronizar fuentes mediante la CLI de Commerce

El comando `saas:resync` del paquete `magento/saas-export` le permite administrar la sincronización de datos para los servicios SaaS de Adobe Commerce.

Adobe no recomienda usar el comando `saas:resync` con regularidad. Los escenarios habituales para utilizar el comando son:

- Sincronización inicial
- Sincronizar datos a nuevo espacio de datos después de cambiar el [ID de espacio de datos SaaS](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)
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

Resincronizar parcialmente entidades específicas mediante sus ID. Admite fuentes `products`, `productAttributes` y `productOverrides`.

De forma predeterminada, las entidades se especifican por SKU del producto. Use `--id-type=ProductID` para usar identificadores de producto en su lugar.

**Ejemplos:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<SKU-1>,<SKU-2>,<SKU-3>'

bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<ID-1>,<ID-2>,<ID-3>' --id-type='productId'
```

## `--cleanup-feed`

Limpia la tabla del indexador de fuentes antes de reindexar y enviar datos a SaaS. Solo se admite para las fuentes `products`, `productOverrides` y `prices`.

>[!IMPORTANT]
>
>Utilícelo solo después de limpiar el entorno. Puede causar problemas de sincronización de datos en los servicios de Commerce.

**Ejemplo:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --cleanup-feed
```

## `--continue-resync`

Reanuda una operación de resincronización interrumpida. Solo se admite para las fuentes `products`, `productAttributes` y `productOverrides`.

**Ejemplo:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --continue-resync
```

## `--dry-run`

Ejecuta el proceso de reindexación de fuentes sin enviar a SaaS ni guardar en la tabla de fuentes. Se utiliza para validar datos.

Agregue la variable de entorno `EXPORTER_EXTENDED_LOG=1` para guardar la carga útil en `var/log/saas-export.log`.

**Ejemplo:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed='<FEED_NAME>' --dry-run
```

## `--feed`

Requerido. Especifica la entidad de fuente que se va a resincronizar.

Fuentes disponibles:

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

**Ejemplo:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>'
```

## `--no-reindex`

Vuelve a enviar los datos del catálogo existente a [!DNL Commerce Services] sin volver a indexar. No compatible con fuentes relacionadas con productos.

El comportamiento varía según el [modo de exportación](data-synchronization.md#synchronization-modes):

- Modo heredado: vuelve a enviar todos los datos sin truncarlos.
- Modo inmediato: la opción se ignora, solo sincroniza actualizaciones/errores.

**Ejemplo:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --no-reindex
```

## Resolución de problemas

Si no ve los datos esperados en los servicios de Commerce conectados, solucione los problemas comprobando los registros de errores de exportación de datos y utilizando el comando `saas:resync` con variables de entorno para revisar las cargas útiles y los datos del generador de perfiles. Ver [Revisar registros y solucionar problemas](troubleshooting-logging.md).
