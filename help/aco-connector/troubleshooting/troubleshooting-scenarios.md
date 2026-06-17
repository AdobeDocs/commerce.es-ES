---
title: Situaciones de solución de problemas para  [!DNL Adobe Commerce Optimizer Connector]
description: Diagnosticar y resolver el comportamiento inesperado en  [!DNL Adobe Commerce Optimizer Connector] causado por una configuración incorrecta o una interpretación incorrecta de los resultados de sincronización.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: c32adafa-ed01-4b31-997e-2413013911b0id: e7dae43f-215c-4cdf-90d3-c5a461a6e669id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2: id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 516
ht-degree: 0%

---


# Situaciones de solución de problemas para [!DNL Adobe Commerce Optimizer Connector]

Esta página describe los comportamientos que puede observar al trabajar con [!DNL Adobe Commerce Optimizer Connector] que normalmente se deben a una configuración incorrecta o a una interpretación incorrecta de los resultados de sincronización. Utilice las descripciones siguientes para identificar la causa raíz y aplicar la resolución adecuada.

## El estado de la fuente muestra &quot;Correcto&quot; pero los datos no son visibles en [!DNL Adobe Commerce Optimizer]

**Problema:** La página **[!UICONTROL Data Feed Sync Status]** informa de una sincronización correcta, pero los productos, precios, etc. no aparecen como se esperaba en [!DNL Adobe Commerce Optimizer].

**Causa:** Un estado de fuente correcto significa que el extremo de ingesta aceptó los datos, pero no que se haya terminado de propagar a través de [!DNL Adobe Commerce Optimizer]. La propagación puede tardar varios minutos después de la ingestión.

**Solución:**

- Espere unos minutos y actualice la vista [!DNL Adobe Commerce Optimizer].
- Confirme que el identificador de inquilino configurado en [!DNL Adobe Commerce] coincide con el entorno [!DNL Commerce Optimizer] que está comprobando.
- Compruebe que la [fuente del catálogo](../../optimizer/setup/catalog-sources.md) (código de vista de tienda) o el libro de precios correctos estén seleccionados en [!DNL Commerce Optimizer].

## Faltan productos en el catálogo exportado

**Problema:** Algunos productos no aparecen en [!DNL Adobe Commerce Optimizer] después de una sincronización de catálogo completa.

**Causa:** Si los productos no superan la validación durante la exportación, se omiten de la sincronización. La API de productos no devolverá los productos que estén desactivados o no sean visibles en el catálogo.

**Solución:**

- Confirme que los productos afectados están asignados al sitio web y a la vista de la tienda utilizada como origen del catálogo.
- Compruebe que los productos estén activados y configurados para una visibilidad que incluya listados de catálogo.
- Revise los detalles de error por elemento para la fuente de catálogo en **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

## Los precios son incorrectos o faltan en [!DNL Adobe Commerce Optimizer]

**Problema:** Los productos aparecen en [!DNL Adobe Commerce Optimizer] pero no muestran ningún precio devuelto con [productos GraphQL query](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"} o el precio no coincide con lo configurado en [!DNL Adobe Commerce].

**Causa:** la fuente de la libreta de precios usa un ámbito que se asigna a un sitio web y grupo de clientes específicos. Una configuración incorrecta de [vista de catálogo](../../optimizer/setup/catalog-view.md) puede provocar precios incorrectos o que falten.

**Solución:**

- Compruebe que el sitio web esté configurado para la sincronización en la configuración de exportación del conector. Ver [Personalizar la configuración de exportación de datos](../get-started.md#customize-the-commerce-scopes-export-configuration).
- Confirme que el Id. de libro de precios utilizado en [!DNL Commerce Optimizer] está presente en la configuración de [vista de catálogo](../../optimizer/setup/catalog-view.md){target="_blank"} utilizada para realizar la consulta de productos.

## Los datos de [!DNL Adobe Commerce Optimizer] se sobrescriben o se modifican inesperadamente después de la sincronización

**Problema:** Los cambios de datos aplicados directamente en [!DNL Adobe Commerce Optimizer] por un sistema externo (como un PIM o ERP) se pierden o revierten después de que el conector ejecute una sincronización.

**Causa:** Cuando otros sistemas distintos de [!DNL Adobe Commerce] escriben directamente en [!DNL Adobe Commerce Optimizer] (por ejemplo, un PIM u otro sistema externo), pueden producirse conflictos de datos. El conector sincroniza los datos *de una manera*, de [!DNL Adobe Commerce] a [!DNL Adobe Commerce Optimizer], y no vuelve a sincronizar los cambios con [!DNL Adobe Commerce]. Como resultado, los datos escritos directamente en [!DNL Adobe Commerce Optimizer] no se reflejan en [!DNL Adobe Commerce] y pueden sobrescribirse durante una sincronización posterior.


**Solución:**

En lugar de escribir modificaciones de catálogo directamente en [!DNL Adobe Commerce Optimizer], use [capas de catálogo](../../optimizer/setup/catalog-layer.md){target="_blank"} para aplicar cambios fuera de [!DNL Adobe Commerce]. Las capas de catálogo permiten que los sistemas externos enriquezcan o anulen los datos del catálogo en [!DNL Adobe Commerce Optimizer] sin entrar en conflicto con la sincronización del conector.

## Situaciones de solución de problemas para [!DNL SaaS Data Export] problemas comunes

Para ver los problemas relacionados con el(la) [!DNL SaaS Data Export] subyacente(s) que pueden afectar al conector, consulte [Escenarios de solución de problemas para [!DNL SaaS Data Export]](../../data-export/troubleshooting/troubleshooting-scenarios.md).
