---
title: Solucionar problemas de  [!DNL Adobe Commerce Optimizer Connector]
description: 'Obtenga información sobre cómo solucionar problemas de exportación de credenciales, catálogos y ámbitos para  [!DNL Adobe Commerce Optimizer Connector] integraciones de PaaS. [!DNL Adobe Commerce] '
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/ei86QuJ3nQ2d-6NRoAeJslgDxjGlZRejD-Nx-6SAVdc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 331
ht-degree: 0%

---

# Solucionar problemas de [!DNL Adobe Commerce Optimizer Connector]

Utilice esta guía para diagnosticar y resolver problemas comunes con [!DNL Adobe Commerce Optimizer Connector] durante la instalación inicial, la sincronización de fuentes de catálogo y la configuración de exportación de ámbito. Las secciones siguientes abarcan la validación de credenciales e inquilinos, errores de sincronización de datos y [!DNL SaaS Data Export] diagnósticos relacionados.

## Error de validación de credenciales o inquilino

Si `aco:config:init` falla durante la validación de credenciales:

- Ejecute el comando CLI `bin/magento aco:config:show` [!DNL Adobe Commerce] para comprobar los valores almacenados.
- Confirme que el ID de inquilino pertenece a la organización de IMS utilizada para obtener las credenciales.
- Confirme que el cliente de OAuth tiene los ámbitos necesarios para el servicio de ingesta [!DNL Adobe Commerce Optimizer] (consulte [Obtener credenciales de IMS](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials)).

## Los datos no se sincronizan

**Comprobar detalles del error en el nivel de elemento:**

Ver [Verificar que la sincronización de datos funcione](./data-sync-manage.md#verify-that-the-data-sync-is-working) para ver los pasos para abrir **[!UICONTROL Data Feed Sync Status]** en el administrador de Commerce. Seleccione la fuente que falla para ver los detalles de error por elemento.

Puntos clave sobre la administración de errores:

- No se vuelven a intentar **400 errores**. Inspeccione la carga útil en busca de campos obligatorios mal formados o que falten. Consulte [Asignación de campos para fuentes de conectores](reference/field-mapping.md) para ver el formato esperado.
- El trabajo cron de `*_resend_failed_items` vuelve a intentar automáticamente **5xx errores** (se ejecuta cada 5 minutos).

**Comprobar configuración de ámbito:**

Si el problema solo afecta a un origen de catálogo específico (código de vista de tienda) o a un libro de precios, compruebe si el sitio web o la vista de tienda correspondiente tienen la sincronización deshabilitada. Vea [Personalizar la configuración de exportación de los ámbitos de Commerce](./get-started.md#customize-the-commerce-scopes-export-configuration).

**Cuando se resolvió:**

Las fuentes del conector muestran un estado correcto en **[!UICONTROL Data Feed Sync Status]** y los productos, precios y atributos esperados aparecen en la página **[!UICONTROL Data Sync]** de [!DNL Commerce Optimizer].

## Configuración incorrecta e interpretación de resultados

Para ver un catálogo de comportamientos específicos causados por una configuración incorrecta o una interpretación errónea de los resultados de sincronización, como productos que faltan, precios incorrectos o lagunas de datos en el nivel de ámbito, consulte [Escenarios de solución de problemas](troubleshooting/troubleshooting-scenarios.md).

## [!DNL SaaS Data Export] diagnósticos

Para obtener diagnósticos de nivel inferior [!DNL SaaS Data Export], incluidas ubicaciones de registro y comandos de resincronización de fuentes, consulte la [[!DNL SaaS Data Export] guía de solución de problemas](https://experienceleague.adobe.com/es/docs/commerce/saas-data-export/troubleshooting/logging){target="_blank"}.
