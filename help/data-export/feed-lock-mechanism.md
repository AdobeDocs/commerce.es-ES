---
title: Mecanismo de bloqueo de fuente para la exportación de datos SaaS
description: Aprenda cómo [!DNL SaaS Data Export] usa bloqueos de fuentes para evitar conflictos en las operaciones de sincronización y proteger la integridad de los datos durante las actualizaciones simultáneas de fuentes.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Services
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 355
ht-degree: 0%

---


# Mecanismo de bloqueo de fuente para la exportación de datos SaaS

La extensión [!DNL SaaS Data Export] utiliza un mecanismo de bloqueo de fuentes para evitar condiciones de carrera cuando varios procesos intentan sincronizar la misma fuente simultáneamente. Esto puede ocurrir, por ejemplo, cuando una resincronización activada por cron se superpone con una llamada manual de CLI `saas:resync`.

## Funcionamiento del bloqueo de alimentación

Cada operación de sincronización de fuentes (desencadenada por un trabajo cron o una llamada manual a CLI de `saas:resync`) sigue la misma secuencia:

1. El proceso intenta adquirir el bloqueo de fuente. El intento de bloqueo es sin bloqueo y devuelve inmediatamente si el bloqueo ya está retenido por otro proceso.
1. Si el bloqueo está **no disponible**, la operación se omitirá y se registrará.

   No se pierden datos. La siguiente ejecución de cron recoge los cambios pendientes una vez finalizado el proceso actual.
1. Si el bloqueo es **adquirido**, el proceso registra su nombre y PID con fines diagnósticos y luego ejecuta la sincronización.
1. Cuando la sincronización se completa o falla, el bloqueo se libera incondicionalmente para que el siguiente trabajo cron programado pueda continuar normalmente.

Solo una operación de sincronización puede mantener el bloqueo de fuente a la vez, independientemente de si lo inició cron o la CLI. El bloqueo de fuente se implementó mediante `LockManagerInterface` de [!DNL Adobe Commerce]. El servidor predeterminado es MySQL, que usa las funciones `GET_LOCK` y `RELEASE_LOCK`. Para configurar un proveedor de bloqueo diferente, consulte [Configurar el proveedor de bloqueo](https://experienceleague.adobe.com/es/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}.

## Mensajes de registro esperados

El siguiente mensaje de `commerce-data-export.log` es normal y no indica ningún problema:

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

Este mensaje aparece cuando una sincronización parcial desencadenada por cron intenta ejecutarse mientras ya se está realizando una reindexación completa de `saas:resync`. No se pierde la operación omitida. Una vez que el proceso en ejecución termina y libera el bloqueo, la siguiente ejecución de cron recoge y sincroniza cualquier cambio pendiente.

>[!NOTE]
>
>Para obtener información general acerca del formato de registro y los tipos de operaciones registrados en `commerce-data-export.log`, vea [Revisar registros y solucionar problemas](troubleshooting/logging.md).

>[!MORELIKETHIS]
>
> - [Sincronizar datos con la exportación de datos SaaS](sync-overview.md)
> - [Sincronizar fuentes usando la CLI de Commerce](data-export-cli-commands.md)
> - [Canalización de sincronización de conectores](../aco-connector/connector-sync-pipeline.md)
> - [Configurar el proveedor de bloqueo](https://experienceleague.adobe.com/es/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}
