---
title: Mejora del rendimiento de exportación de datos SaaS
description: Obtenga información sobre cómo mejorar el rendimiento de exportación de datos SaaS para Commerce Services mediante el modo de exportación de datos de varios subprocesos.
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# Mejora del rendimiento de exportación de datos SaaS

**El modo de exportación de datos multiproceso** acelera el proceso de exportación al dividir los datos de las fuentes en lotes y procesarlos en paralelo.

Los desarrolladores o integradores de sistemas pueden mejorar el rendimiento utilizando el modo de exportación de datos de varios subprocesos en lugar del modo predeterminado de un solo subproceso. En el modo de un solo hilo, no hay paralelización del proceso de envío de fuentes. Además, debido a los límites predeterminados establecidos, todos los clientes están restringidos a utilizar un solo subproceso. En la mayoría de los casos, no es necesario personalizar la configuración.

## Consideraciones para utilizar el modo multiproceso

Al trabajar con los servicios de exportación de datos, desea optimizar el rendimiento a la vez que garantiza una sincronización precisa.
Adobe recomienda utilizar la configuración predeterminada para la ingesta de datos, que generalmente cumple los requisitos de sincronización para los comerciantes de Commerce. Sin embargo, hay situaciones en las que la personalización puede acelerar el tiempo de procesamiento.

Tenga en cuenta los siguientes factores clave al decidir si desea personalizar la configuración de exportación de datos:

- **Sincronización inicial**: evalúe el número de productos y [estime el volumen de datos y el tiempo de transmisión](estimate-data-volume-sync-time.md) en función de la configuración predeterminada. Pregúntese lo siguiente: ¿puede esperar esta sincronización de datos inicial después de incorporar un servicio de Commerce?

- **Agregar nuevas vistas de la tienda o sitios web**: si planea agregar vistas de la tienda o sitios web con el mismo recuento de productos después de su lanzamiento, calcule el volumen de datos y el tiempo de transmisión. Determine si la hora de sincronización es aceptable con la configuración predeterminada o si es necesario el procesamiento de subprocesos múltiples.

- **Importaciones regulares**: prevea importaciones regulares, como actualizaciones de precios o cambios de estado de las existencias. Evalúe si estas actualizaciones se pueden aplicar en un lapso de tiempo aceptable o si se necesita un procesamiento más rápido.

- **Peso del producto**: considere si sus productos son ligeros o pesados. Ajuste el tamaño del lote en consecuencia si las descripciones o atributos del producto inflan el tamaño del producto.

Recuerde que una planificación cuidadosa, que incluya la estimación del volumen de datos y el tiempo de sincronización, a menudo puede eliminar la necesidad de personalización. Programe operaciones de ingesta de fuentes en función de estas estimaciones para lograr resultados óptimos.

>[!NOTE]
>
>Adobe recomienda tener cuidado al utilizar el procesamiento de subprocesos múltiples. Esta capacidad es una función de acceso anticipado que aún se está mejorando. Si configura el subprocesamiento múltiple para obtener un rendimiento más rápido, puede almacenar en déclencheur las protecciones de los servicios de Adobe Commerce incluidas para evitar el uso indebido del sistema durante la ingesta de datos. Estas protecciones también restringen a los usuarios de activar cambios de sincronización que pueden sobrecargar el sistema. Cuando se activan las protecciones, las solicitudes se bloquean y el sistema devuelve errores 429. Si se producen estos errores, ajuste la configuración y envíe un ticket de asistencia para obtener ayuda.

## Configurar subprocesamiento múltiple

Se admite el modo multiproceso para todos los [métodos de sincronización](data-synchronization.md#synchronization-process): sincronización completa, sincronización parcial y sincronización de elementos con errores. Para configurar subprocesos múltiples, especifique el número de subprocesos y el tamaño del lote que se utilizarán durante la sincronización.

- `thread-count` es el número de subprocesos activados para procesar entidades. El valor predeterminado `thread-count` es `1`.
- `batch-size` es el número de entidades procesadas en una iteración. El valor predeterminado `batch-size` es `100` registros para todas las fuentes, excepto la fuente de precios. Para la fuente de precios, el valor predeterminado es `500` registros.

Puede configurar el subprocesamiento múltiple como una opción temporal al ejecutar un comando de resincronización o agregando la configuración de subprocesamiento múltiple a la configuración de la aplicación de Adobe Commerce.

>[!NOTE]
>
>Asegúrese de alinear el rendimiento de la exportación de datos de SaaS con el límite de velocidad definido para un cliente en el lado del consumidor.

### Configurar subprocesamiento múltiple durante la ejecución

Cuando ejecute un comando de sincronización completa desde la línea de comandos, especifique el procesamiento de subprocesos múltiples agregando las opciones `thread-count` y `batch-size` al comando CLI.

```
bin/magento saas:resync --feed=products --thread-count=2 --batch-size=200
```

Las opciones especificadas en la línea de comandos anulan la configuración de exportación de datos especificada en el archivo de la aplicación Adobe Commerce `config.php`.

### Agregar subprocesos múltiples a la configuración de Commerce

Para procesar todas las operaciones de exportación de datos mediante subprocesamiento múltiple, los integradores de sistemas o los desarrolladores pueden modificar el número de subprocesos y el tamaño del lote para cada fuente en la configuración de la aplicación de Commerce.

Estos cambios se pueden aplicar agregando valores personalizados a la [sección del sistema](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/files/config-reference-configphp#system) del archivo de configuración, `app/etc/config.php`.

**Ejemplo: Configurar subprocesamiento múltiple para productos y precios**

```php
<?php
return [
    'system' => [
        'default' => [
            'commerce_data_export' => [
                'feeds' => [
                    'products' => [
                        'batch_size' => 100,
                        'thread_count' => 2,
                    ],
                    'prices' => [
                        'batch_size' => 400,
                        'thread_count' => 4,
                    ]
                ]
            ],
//   ...
```
