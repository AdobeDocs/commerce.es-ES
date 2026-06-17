---
title: Sincronizar fuentes mediante la CLI de Commerce
description: Aprenda a utilizar comandos CLI de Commerce para administrar fuentes y procesos de sincronización para  [!DNL data export extension] en los servicios SaaS de Adobe Commerce.
autotag-review: '2026-06-17T15:08:59.000Z'
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
TQID: 'https://experienceleague.adobe.com/Vi8hMKOBjTPkSQp0t8DCkjZsJ8s3Q5GSbSXyX2gmWRo'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 670
ht-degree: 0%

---

# Sincronizar fuentes mediante la CLI de Commerce

El comando `saas:resync` del paquete `magento/saas-export` le permite administrar la sincronización de datos para los servicios SaaS de [!DNL Adobe Commerce].

>[!NOTE]
>
>El comando `saas:resync` también se aplica a [!DNL Adobe Commerce Optimizer Connector] fuentes como `products`, `categories` y `priceBooks`. Consulte [Fuentes compatibles](../aco-connector/reference/connector-reference.md#supported-feeds) para obtener la lista completa de fuentes de conector y nombres de indizador.

Adobe no recomienda usar el comando `saas:resync` con regularidad. Los escenarios habituales para utilizar el comando son:

- Sincronización inicial
- Sincronizar datos a un nuevo espacio de datos después de cambiar el [ID de espacio de datos SaaS](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)
- Resolución de problemas

Supervisar operaciones de sincronización en el archivo `var/log/saas-export.log`.

## Sincronización inicial

>[!NOTE]
>
>La sincronización inicial se ejecuta automáticamente cuando Live Search o Product Recommendations están habilitados. No se necesitan comandos manuales.
>
>Para implementaciones de [!DNL Adobe Commerce Optimizer Connector], el comando `aco:config:init` programa la sincronización completa inicial invalidando todos los indexadores de fuentes de conector. Ver [Habilitar la  [!DNL Commerce Optimizer] integración](../aco-connector/get-started.md#enable-the-adobe-commerce-optimizer-integration) y [Administrar sincronización con [!DNL Commerce Optimizer]](../aco-connector/data-sync-manage.md).

Al almacenar en déclencheur un(a) `saas:resync` desde la línea de comandos, según el tamaño del catálogo, los datos pueden tardar entre unos minutos y unas pocas horas en actualizarse.

Las sincronizaciones de fuentes se pueden ejecutar en cualquier orden; no hay dependencias fijas entre ellas. La siguiente secuencia comienza primero con los datos de ámbito, lo que es un punto de partida lógico, ya que los ámbitos definen las vistas de almacén a las que hacen referencia otras fuentes.

```shell
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed productAttributes
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed products
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed productoverrides
```

>[!NOTE]
>
>Es posible que su entorno no incluya todas las fuentes en esta secuencia. Consulte [Fuentes compatibles](reference/feed-table-reference.md#supported-feeds) para obtener la lista de fuentes completa, los nombres de fuentes CLI y los requisitos de módulo.

## Opciones de comando

El comando `saas:resync` admite varias operaciones de sincronización:

- Sincronización parcial por SKU
- Reanudar sincronizaciones interrumpidas
- Validar datos sin sincronizar

Ver todas las opciones y marcas de comando:

```shell
bin/magento saas:resync --help
```

Consulte las secciones siguientes para ver descripciones de opciones con ejemplos.

>[!NOTE]
>
>Para obtener opciones avanzadas para administrar el procesamiento de exportación, consulte [Personalizar el procesamiento de exportación](customize-export-processing.md).

## `--feed`

Requerido. Especifica la entidad de fuente que se va a resincronizar.

`bin/magento saas:resync --help` documentos opciones de comando y marcas. No enumera todas las fuentes disponibles en su entorno. Para obtener la lista completa de fuentes con nombres de fuentes CLI, ID de indizador y tablas de fuentes, consulte [Fuentes compatibles](reference/feed-table-reference.md#supported-feeds).

>[!NOTE]
>
>Los módulos instalados determinan qué fuentes se pueden volver a sincronizar. Por ejemplo, `productOverrides` requiere [!DNL Adobe Commerce] en la nube, de forma local o Commerce as a Cloud Service, y `orders` requiere el módulo Pedidos de venta.

**Ejemplo:**

```shell
bin/magento saas:resync --feed products
```

## `--by-ids`

Resincronizar parcialmente entidades específicas mediante sus ID. Admite fuentes de `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` y `categoryPermissions`.

De manera predeterminada, al usar la opción `--by-ids`, se especifican valores mediante los valores de SKU del producto. Para usar identificadores de producto, agregue la opción `--id-type=productId`.

**Ejemplos:**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed products --by-ids='1,2,3' --id-type='productId'
```

## `--cleanup-feed`

Limpie la tabla del indexador de fuentes antes de reindexar y enviar datos a SaaS. Solo se admite para `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` y `categoryPermissions`.

Si se utiliza con la opción `--dry-run`, la operación realiza una operación de resincronización de ejecución en seco para todos los elementos.

>[!WARNING]
>
>El uso del comando resync con la opción `cleanup-feed` borra el estado de exportación de la fuente local y puede provocar una sincronización incompleta. Por ejemplo, es posible que las eliminaciones de entidades en [!DNL Adobe Commerce] no se reflejen en los servicios de Commerce conectados, o que las entidades antiguas permanezcan en los índices remotos de los servicios de Commerce aunque se eliminaron o actualizaron en [!DNL Adobe Commerce]. Utilice esta opción solo para reconstrucciones de entorno completas, como después de una limpieza del espacio de datos SaaS.

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

**Ejemplo:**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
```

## `--no-reindex`

Vuelve a enviar los datos del catálogo existente a [!DNL Commerce Services] sin volver a indexar. No compatible con fuentes relacionadas con productos.

El comportamiento varía según el [modo de exportación](sync-overview.md#synchronization-modes):

- Modo heredado: vuelve a enviar todos los datos sin truncarlos.
- Modo inmediato: la opción se ignora, solo sincroniza actualizaciones/errores.

**Ejemplo:**

```shell
bin/magento saas:resync --feed productAttributes --no-reindex
```

>[!MORELIKETHIS]
>
> - [Revisar registros y solucionar problemas](troubleshooting/logging.md): Diagnostique errores de exportación de datos y SaaS.
> - [Situaciones de solución de problemas](troubleshooting/troubleshooting-scenarios.md): resuelva la configuración incorrecta y los resultados de sincronización inesperados.
> - [Funcionamiento de la sincronización](sync-overview.md): obtenga información sobre los modos de sincronización y el comportamiento de reintentos.
