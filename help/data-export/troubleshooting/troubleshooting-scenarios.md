---
title: Solucionando problemas de escenarios para  [!DNL SaaS Data Export]
description: Aprenda a diagnosticar y resolver el comportamiento de sincronización  [!DNL SaaS Data Export] inesperado debido a una configuración incorrecta, a una configuración del indizador o a una interpretación errónea de los resultados de sincronización.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: c32adafa-ed01-4b31-997e-2413013911b0id: e7dae43f-215c-4cdf-90d3-c5a461a6e669id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2: id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 991
ht-degree: 0%

---


# Situaciones de solución de problemas para [!DNL SaaS Data Export]

Esta página describe los comportamientos que puede observar al trabajar con [!DNL SaaS Data Export] que normalmente se deben a una configuración incorrecta o a una interpretación incorrecta de los resultados de sincronización. Utilice las descripciones siguientes para identificar la causa raíz y aplicar la resolución adecuada.

## Falta un producto configurable o agrupado en los servicios de Commerce {#configurable-bundle-missing}

**Problema:** Un producto configurable o agrupado tiene el estado *Habilitado* en [!DNL Adobe Commerce], pero no se devuelve en la tienda o se muestra con el estado *Deshabilitado* en los servicios SaaS de Commerce.

**Causa:** El estado efectivo de los productos compuestos depende del estado de sus productos secundarios, no solo del estado del producto principal. Los servicios SaaS de Commerce reflejan este estado calculado:

- **Productos configurables**: debe habilitarse al menos una variante de producto.
- **Productos agrupados**: debe habilitarse al menos un producto para cada opción de paquete requerida.

Si no se cumplen estas condiciones, el producto principal se trata como deshabilitado aunque su propio estado esté establecido en *Enabled*.

**Solución:**

- Para los productos configurables, compruebe que hay al menos una variante de producto simple asociada habilitada y asignada al sitio web y a la vista de tienda correctos.
- Para los productos agrupados, compruebe que cada opción de paquete requerida tenga al menos un producto secundario habilitado. Una opción necesaria con todos los elementos secundarios deshabilitados hace que todo el paquete se trate como deshabilitado.
- Después de habilitar los productos secundarios adecuados, vuelva a sincronizar el déclencheur o espere a la siguiente sincronización programada y, a continuación, confirme el estado actualizado en los servicios SaaS de Commerce.

## Precios no actualizados tras la activación de la regla de precios del catálogo {#prices-not-updated}

**Problema:** Después de activar una regla de precios de catálogo usando la característica Actualización programada, los precios no se actualizan. `commerce-data-export.log` muestra `synced: 0` para la fuente `prices` después de aplicar las actualizaciones programadas.

**Causa:** Puede producirse una condición de carrera entre grupos cron cuando se utilizan actualizaciones programadas para reglas de precios de catálogo. Es posible que el indizador `catalog_data_exporter_product_prices` se ejecute antes de que su dependencia, el índice `catalogrule_product`, haya terminado de reconstruirse. Como resultado, el exportador de precios lee datos obsoletos y no exporta cambios.

**Solución:**

La solución inmediata para este problema es una solución alternativa: Configure ambos grupos de cron para que se ejecuten secuencialmente y eliminen la condición de carrera:

1. Vaya a **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL System]** > **[!UICONTROL Cron (Scheduled Tasks)]**.
1. Establezca **[!UICONTROL Use Separate Process]** en **[!UICONTROL No]** para ambos:
   - Opciones de configuración de Cron para el grupo: **[!UICONTROL index]**
   - Opciones de configuración de Cron para el grupo: **[!UICONTROL staging]**
1. Vacíe la caché de configuración después de guardar.

>[!NOTE]
>
>Con ambos grupos ejecutándose en proceso y de forma secuencial, un reíndice completo lento impide que se ejecute el ensayo hasta que termine. En catálogos grandes, esto puede retrasar las actualizaciones de ensayo.

## Discrepancia de datos de catálogo entre [!DNL Adobe Commerce] y los servicios conectados {#catalog-data-discrepancy}

**Problema:** Los datos del producto que se muestran en los servicios conectados de Commerce (como [!DNL Live Search] o [!DNL Product Recommendations]) no coinciden con los datos del catálogo en [!DNL Adobe Commerce]. Por ejemplo, el nombre, el precio o la descripción de un producto aparecen obsoletos o son incorrectos en la tienda.

**Causa:** Después de activar una resincronización, los datos pueden tardar hasta una hora en actualizarse y reflejarse en los componentes de la interfaz de usuario. Si la discrepancia persiste más allá de esa ventana, es posible que la última sincronización no haya seleccionado el elemento o que la sincronización no haya detectado un cambio porque los datos de la fuente ya se hayan marcado como actualizados.

**Solución:**

1. En la tienda Commerce, abra los resultados de búsqueda. A continuación, seleccione el producto en cuestión para abrir su vista detallada.
1. Copie la salida JSON y compruebe que coincide con lo que tiene en el catálogo [!DNL Commerce].
1. Si el contenido no coincide, realice una edición menor del producto en el catálogo, como añadir un espacio o un punto, para forzar la detección del cambio.
1. Espere a que se realice una resincronización o ponga en déclencheur una resincronización manual desde la CLI o la página [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) en el administrador.

Para obtener información adicional sobre la solución de problemas de los datos del catálogo en [!DNL Product Recommendations], consulte [Solución de problemas del módulo de recomendaciones de productos](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce) en la Base de conocimiento de Commerce.

## La sincronización de datos no se está ejecutando según lo programado {#sync-not-on-schedule}

**Problema:** La sincronización de datos no se ejecuta según lo programado o no se están sincronizando elementos a pesar de los cambios de producto en [!DNL Adobe Commerce].

**Causa:** Las causas más comunes son trabajos cron que no se ejecutan o indizadores no configurados en el modo **[!UICONTROL Update by Schedule]**.

**Solución:**

- [Confirme que los trabajos cron se están ejecutando](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).
- Compruebe que los indizadores de las siguientes fuentes estén establecidos en **[!UICONTROL Update by Schedule]**: Atributos de catálogo, Producto, Anulaciones de producto y Variante de producto. Compruebe [[!UICONTROL Index Management]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) en el administrador de Commerce o use la CLI: `bin/magento indexer:show-mode | grep -i feed`.

## La sincronización del catálogo tiene el estado Error {#catalog-sync-failed}

**Problema:** La sincronización del catálogo muestra el estado **Error** en la página **[!UICONTROL Data Feed Sync Status]**.

**Causa:** Se produjo un error irrecuperable durante la fase de recopilación o envío de datos. Las causas comunes incluyen problemas de autenticación de API, errores de red o errores de validación de datos.

**Solución:**

1. Revise los registros de errores de exportación de datos para obtener más información sobre el error. Consulte [Revisar registros y solucionar problemas](logging.md) para ver las opciones de formato de registro y registro extendido:
   - `var/log/commerce-data-export-errors.log` para detectar errores durante la recopilación de datos.
   - `var/log/saas-export-errors.log` para errores durante el envío de datos.
1. Si el error no está relacionado con la configuración o una extensión de terceros, [envíe un vale de soporte técnico](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) con las entradas de registro relevantes.

## El registro muestra mensajes &quot;operación omitida: proceso bloqueado&quot; {#process-locked}

**Problema:** El archivo `commerce-data-export.log` contiene entradas similares a las siguientes:

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

**Causa:** Este es un comportamiento esperado, no un error. El mensaje aparece cuando una sincronización parcial activada por cron intenta ejecutarse mientras ya se está realizando una reindexación completa de `saas:resync`. La extensión [!DNL SaaS Data Export] utiliza un mecanismo de bloqueo de fuentes para evitar que se produzcan conflictos en las operaciones de sincronización simultánea.

**Solución:**

No se requiere ninguna acción. Una vez que el proceso en ejecución termina y libera el bloqueo, la siguiente ejecución de cron recoge y sincroniza cualquier cambio pendiente. Para obtener más información sobre cómo funciona el mecanismo de bloqueo, consulte [Mecanismo de bloqueo de fuente para la exportación de datos SaaS](../feed-lock-mechanism.md).

>[!MORELIKETHIS]
>
> - [Revisar registros y solucionar problemas](logging.md)
> - [Referencia de códigos de registro](log-codes-reference.md)
> - [Mecanismo de bloqueo de fuente para la exportación de datos SaaS](../feed-lock-mechanism.md)
