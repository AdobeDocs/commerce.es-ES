---
title: Introducción a  [!DNL Catalog Service]
description: Obtenga información sobre cómo acceder a  [!DNL Catalog Service]  e integrarlo con aplicaciones de front-end y servicios de terceros.
role: Admin, Developer
exl-id: ee178e67-519d-4283-8de8-2634ae1f347a
TQID: https://experienceleague.adobe.com/KBdWesEoKJu-qWsY-Ny1Om-msUkyUPfUTQWftEqSg1g
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 10a91a91337778648e99078bcbf0c9ef25a49f86
workflow-type: tm+mt
source-wordcount: 437
ht-degree: 0%

---

# Introducción a [!DNL Catalog Service]

Una vez habilitado [!DNL Catalog Service], puede obtener acceso al servicio y utilizarlo para recuperar datos de catálogo, como información de productos y categorías, de la instancia de Adobe Commerce. El servicio está disponible como API de GraphQL a la que puede acceder desde el administrador de Commerce o desde cualquier aplicación de front-end que admita consultas de GraphQL.

{{aco-merchandising-services}}

## Acceso al servicio

[!DNL Catalog Service] está disponible como una API de GraphQL a la que puede acceder desde el administrador de Commerce o desde cualquier aplicación de front-end que admita consultas de GraphQL. El servicio está disponible en entornos SaaS y PaaS.

[!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."}

| Entorno | Extremo |
| ------------ | ----------: |
| **Pruebas** | `https://catalog-service-sandbox.adobe.io/graphql` |
| **Producción** | `https://catalog-service.adobe.io/graphql` |

[!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."}

| Entorno | Extremo |
| ----------- | --------:|
| Pruebas | `https://na1-sandbox.api.commerce.adobe.com/{{tenant-id}}/graphql` |
| Producción (aún no disponible) | `https://na1.api.commerce.adobe.com/{{tenant-id}}/graphql` |

**Estructura de URL para extremos SaaS**

```text
https://<region>-<environment>.api.commerce.adobe.com/<tenantId>/graphql
```

- `<region>` es la región de la nube donde se implementa su instancia.
- `<environment>` es el tipo de entorno, como `sandbox`. Si el entorno es de producción, este valor se omite.
- `<tenantId>` es el identificador único de la instancia específica de su organización en Adobe Experience Cloud.

Para obtener más información sobre el uso de la API de GraphQL del servicio de catálogo, consulte la [Guía del servicio de catálogo para Adobe Commerce](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/) en la *documentación para desarrolladores de Adobe Commerce*.

## Integración con una tienda sin encabezado o servicios de terceros

Para integrarse con una tienda sin encabezado, debe actualizar la configuración de la tienda para habilitar la comunicación entre la tienda y [!DNL Catalog Service] para recuperar los datos de productos y categorías.

Si utiliza la tienda de Adobe Commerce en Edge Delivery Services, agregue el punto final del servicio de catálogo a la configuración de la tienda. Para obtener más información, consulte la [documentación de Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/?lang=es#storefront-configuration).

Para otras integraciones, consulte la documentación de configuración del proyecto para obtener más información sobre cómo configurar integraciones entre el servicio y las fuentes de datos back-end.

### Configuración del cortafuegos

Para permitir que [!DNL Catalog Service] pase a través de un firewall, agregue `commerce.adobe.io` a la lista de permitidos.

## Servicio de catálogo y malla de API

La [malla de API para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) permite a los desarrolladores integrar API privadas o de terceros y otras interfaces con productos de Adobe mediante Adobe IO.

Consulte el tema [[!DNL Catalog Service] y API Mesh](mesh.md) para obtener detalles de instalación y configuración.

## Monitorización y solución de problemas de exportación de datos

{{$include /help/_includes/data-export/verify-commerce-service-data-sync.md}}

Use la [CLI de Commerce](../data-export/data-export-cli-commands.md) para resincronizar fuentes manualmente cuando sea necesario. Para ver las opciones de resincronización y los pasos adicionales de solución de problemas, consulte [Administrar sincronización](../data-export/data-sync-manage.md) en la _Guía de exportación de datos SaaS_.

{{install-data-sync-feed-status}}
