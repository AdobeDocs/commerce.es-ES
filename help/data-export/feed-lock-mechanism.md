---
title: Mecanismo de bloqueo de fuente para la exportación de datos SaaS
description: Aprenda cómo [!DNL SaaS Data Export] usa bloqueos de fuentes para evitar conflictos en las operaciones de sincronización y proteger la integridad de los datos durante las actualizaciones simultáneas de fuentes.
role: Admin, Developer
feature: Services
source-git-commit: cfa1002653bf66afd3f6b8484b33076adcd1b7d4
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# Mecanismo de bloqueo de fuente para la exportación de datos SaaS

La extensión [!DNL SaaS Data Export] utiliza un mecanismo de bloqueo de fuentes para evitar condiciones de carrera cuando varios procesos intentan sincronizar la misma fuente simultáneamente. Esto puede ocurrir, por ejemplo, cuando una resincronización activada por cron se superpone con una llamada manual de CLI `saas:resync`.

## Funcionamiento del bloqueo de alimentación

Cada operación de sincronización de fuentes (desencadenada por un trabajo cron o una llamada manual a CLI de `saas:resync`) sigue la misma secuencia:

1. El proceso intenta adquirir el bloqueo de fuente. El intento de bloqueo es sin bloqueo y devuelve inmediatamente si el bloqueo ya está retenido por otro proceso.
1. Si el bloqueo es **no disponible**, la operación [se omitirá y se registrará].

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
>Para obtener información general acerca del formato de registro y los tipos de operaciones registrados en `commerce-data-export.log`, vea [Revisar registros y solucionar problemas](troubleshooting-logging.md).

## Más ayuda sobre este tema

- [Sincronización de datos con exportación de datos SaaS](data-synchronization.md)
- [Sincronizar fuentes mediante la CLI de Commerce](data-export-cli-commands.md)
- [Configuración del proveedor de bloqueos](https://experienceleague.adobe.com/es/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}
