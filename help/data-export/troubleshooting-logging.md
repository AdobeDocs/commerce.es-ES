---
title: Revisar registros y solucionar problemas
description: Obtenga información sobre cómo solucionar  [!DNL data export] errores mediante los registros de exportación de datos y exportación de saas.
feature: Services
exl-id: d022756f-6e75-4c2a-9601-31958698dc43
source-git-commit: a1afed7b635a2b05c5c0e0d1c9bf4a07fc5eef31
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 0%

---

# Revisar registros y solucionar problemas

La extensión [!DNL data export] proporciona registros para realizar un seguimiento de los procesos de sincronización y recopilación de datos.

## Registros

Los registros están disponibles en el directorio `var/log` del servidor de aplicaciones de Commerce.

| nombre del registro | filename | description |
|-----------------| ----------| -------------|
| Registro de exportación de datos SaaS | `commerce-data-export.log` | Proporciona información sobre las actividades de exportación de datos, como los eventos de entidad y los déclencheur de resincronización completa.  Cada registro tiene una estructura específica y proporciona información sobre la fuente, la operación, el estado, el tiempo transcurrido, el ID de proceso y el llamador. |
| Registro de errores de exportación de datos SaaS | `data-export-errors.log` | Proporciona mensajes de error y seguimientos de pila para los errores que se producen durante el proceso de sincronización de datos. |
| Registro de exportación de SaaS | `saas-export.log` | Proporciona información sobre los datos enviados a los servicios SaaS de Commerce. |
| Registro de errores de exportación de SaaS | `saas-export-errors.log` | Proporciona información sobre los errores que se producen al enviar datos a los servicios SaaS de Commerce. |

Si no ve los datos esperados para un servicio de Adobe Commerce, utilice los registros de error de la extensión de exportación de datos para determinar dónde se produjo el problema. Además, puede ampliar los registros con datos adicionales para el seguimiento y la resolución de problemas. Consulte [Registro extendido](#extended-logging).

### Formato de registro

Cada registro tiene la siguiente estructura.

```
[<log record datetime>] report.<log level>:
{
   "feed": "<feed name>",
   "operation": "<executed operation>",
   "status": "<status of operation>",
   "elapsed": "<time elapsed from script run>",
   "pid": "<process id that executed `operation`>",
   "caller": "<who called this `operation`>"
} [] []
```

>[!NOTE]
>
>La cadena basada en JSON está embellecida para mejorar la legibilidad.

En la tabla siguiente se describen los tipos de operación que se pueden registrar en los registros.

| Operación | Descripción | Ejemplo de llamador |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| sincronización completa | Recopila y envía todos los datos al SaaS de una fuente determinada. | `bin/magento saas:resync --feed=products` |
| reindexación parcial | Recopila y envía datos a SaaS solo para las entidades actualizadas de una fuente determinada. Este registro solo está presente si existen entidades actualizadas. | `bin/magento cron:run --group=index` |
| reintentar elementos con errores | Reenviar elementos de una fuente determinada a SaaS si la operación de sincronización anterior ha fallado debido a un error de la aplicación o del servidor de Commerce. Este registro solo está presente si existen elementos con error. | `bin/magento cron:run --group=saas_data_exporter` (cualquier grupo cron &quot;*_data_exporter&quot;) |
| sincronización completa (heredada) | Recopila y envía todos los datos a SaaS para una fuente determinada en el modo de exportación heredado. | `bin/magento saas:resync --feed=categories` |
| reindexación parcial (heredada) | Envía entidades actualizadas a SaaS para una fuente determinada en el modo de exportación heredado. Este registro solo está presente si existen entidades actualizadas. | `bin/magento cron:run --group=index` |
| sincronización parcial (heredada) | Envía entidades actualizadas a SaaS para una fuente determinada en el modo de exportación heredado. Este registro solo está presente si existen entidades actualizadas. | `bin/magento cron:run --group=saas_data_exporter` (cualquier grupo cron &quot;*_data_exporter&quot;) |


### Ejemplos de registro

De forma predeterminada, durante una resincronización completa, el progreso se rastrea y registra cada 30 segundos. Este es un ejemplo de entrada de registro.

```json
{
   "feed": "prices",
   "operation": "full sync",
   "status": "Progress: 2/5, processed: 200, synced: 100",
   "elapsed": "00:00:00 190 ms",
   "pid": "12824",
   "caller": "bin/magento saas:resync --feed=products"
}
```

En este ejemplo, los valores `status` proporcionan información sobre la operación de sincronización:

- **`"Progress 2/5"`** indica que se han completado 2 de 5 iteraciones. El número de iteraciones depende del número de entidades exportadas.
- **`"processed: 200"`** indica que se han procesado 200 elementos.
- **`"synced: 100"`** indica que se enviaron 100 elementos a SaaS. Se espera que `"synced"` no sea igual a `"processed"`. A continuación se muestra un ejemplo:
   - **`"synced" < "processed"`** significa que la tabla de fuentes no detectó ningún cambio en el elemento, en comparación con la versión sincronizada anteriormente. Estos elementos se omiten durante la operación de sincronización.
   - **`"synced" > "processed"`** el mismo id. de entidad (por ejemplo, `Product ID`) puede tener varios valores en distintos ámbitos. Por ejemplo, se puede asignar un producto a cinco sitios web. En este caso, es posible que tenga &quot;1 elemento procesado&quot; y &quot;5 sincronizados&quot; elementos.

+++ **Ejemplo: registro de resincronización completo para la fuente de precios**

```
Price feed full resync:

[2024-03-05T21:00:51.754687+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Initialize","elapsed":"383 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.803178+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Creating batch table `catalog_data_exporter_product_prices_index_batches`. Start position: 30515","elapsed":"434 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.851878+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Batch table `catalog_data_exporter_product_prices_index_batches` created. Total Items: 500, batches: ~1","elapsed":"482 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.852548+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"start processing `500` items in `1` threads with `500` batch size","elapsed":"483 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:52.288369+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 0","elapsed":"919 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.994249+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 100","elapsed":"00:00:02 625 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.995168+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Complete","elapsed":"00:00:02 626 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
```

+++

## Visualización y solución de problemas de registros con New Relic

Si almacena los registros de Adobe Commerce en New Relic, puede agregar reglas de análisis para mejorar la legibilidad y la experiencia de consulta.

1. Inicie sesión en New Relic.

1. Ir a `Logs => Parsing`.

1. Haga clic en `Create parsing rule`.

1. Configure la regla de análisis añadiendo los siguientes valores.

   - **Filtrar registros basados en NRQL**

     `filePath LIKE '%commerce-data-export%.log'`

   - **Regla de análisis**

     `\[%{DATA:timestamp}\] report.%{DATA:logLevel}: %{GREEDYDATA:feed:json}`

En este ejemplo se agrega una regla que permite consultar los registros de New Relic por tipo de fuente específico, operación, etc.

**Ejemplo de cadena de consulta**—`feed.feed:"products" and feed.status:"Complete"`

## Resolución de problemas

Si faltan datos o estos son incorrectos en Commerce Services, compruebe en los registros si hay mensajes acerca de errores que se produjeron durante la sincronización de Adobe Commerce a la plataforma de Commerce Services. Si es necesario, utilice el registro ampliado para agregar información adicional a los registros para la resolución de problemas.

- El registro de errores de exportación de datos (`commerce-data-export-errors.log`) captura los errores que se producen durante la fase de recopilación.
- El registro de errores de exportación de SaaS (`saas-export-errors.log`) registra los errores que se producen durante la fase de transmisión.

Si observa errores no relacionados con la configuración o con extensiones de terceros, envíe un [ticket de asistencia](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) con la mayor información posible.

### Resolver problemas de sincronización del catálogo {#resolvesync}

Cuando se sincroniza en déclencheur una sincronización de datos, los datos pueden tardar hasta una hora en actualizarse y se reflejarán en componentes de la interfaz de usuario como la búsqueda en directo y las unidades de recomendación. Si sigue viendo discrepancias entre el catálogo y los datos de la tienda de Commerce o si la sincronización del catálogo falla, consulte lo siguiente:

#### Discrepancia de datos

1. Mostrar la vista detallada del producto en cuestión en los resultados de búsqueda.
1. Copie la salida JSON y verifique que el contenido coincida con lo que tiene en el catálogo [!DNL Commerce].
1. Si el contenido no coincide, realice un cambio menor en el producto del catálogo, como añadir un espacio o un punto.
1. Espere a que se realice una resincronización o [déclencheur una resincronización manual](#resync).

#### La sincronización no se está ejecutando

Si la sincronización no se está ejecutando según una programación o no hay nada sincronizado, consulte este artículo de [KnowledgeBase](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce).

#### Error de sincronización

Si la sincronización del catálogo tiene el estado **Error**, envíe un [ticket de asistencia](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket).

## Registro extendido

Utilice variables de entorno para ampliar los registros con datos adicionales para el seguimiento y la resolución de problemas. Agregue la variable de entorno a la línea de comandos cuando ejecute comandos CLI de exportación de datos, como se muestra en los ejemplos siguientes.

### Comprobación de la carga útil de fuente

Incluya la carga útil de la fuente en el registro de exportación de SaaS agregando la variable de entorno `EXPORTER_EXTENDED_LOG=1` al volver a sincronizar la fuente.

```shell script
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed=products
```

Una vez finalizada la operación, la carga útil de fuente está disponible para su revisión en el registro de exportación de SaaS (`var/.log/saas-export.log`).

### Conservar carga útil en tabla de índice de fuentes

Para la extensión de exportación de datos SaaS de Commerce (`magento/module-data-exporter`) 103.3.0 y posterior, las fuentes de exportación inmediatas mantienen solamente los datos mínimos requeridos en la tabla de índice. Las fuentes incluyen todas las fuentes de estado de stock de catálogo e inventario.

No se recomienda conservar los datos de carga útil en la tabla de índices en los entornos de producción, pero puede resultar útil en un entorno de desarrollo. Incluya la carga útil de la fuente en el índice agregando la variable de entorno `PERSIST_EXPORTED_FEED=1` al resincronizar la fuente.

```shell script
PERSIST_EXPORTED_FEED=1 bin/magento saas:resync --feed=products
```

### Ejecute el generador de perfiles para solucionar problemas de rendimiento lento

Si el proceso de reindexación de una fuente específica lleva una cantidad de tiempo no razonable, ejecute el generador de perfiles para recopilar datos adicionales que puedan ser útiles para el equipo de asistencia.

Ejecute el generador de perfiles agregando la variable de entorno `EXPORTER_PROFILER=1` al ejecutar el comando reindex.

```
EXPORTER_PROFILER=1 bin/magento indexer:reindex catalog_data_exporter_products
```

Los datos del analizador se almacenan en el registro de exportación de datos (`var/log/commerce-data-export.log`) con el siguiente formato:

```
<Provider class name>, <# of processed entities>, <execution time im ms>, <memory consumption in Mb>
```
