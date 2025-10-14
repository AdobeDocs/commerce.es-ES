---
title: Introducción a  [!DNL Catalog Service]
description: Obtenga información sobre cómo acceder a  [!DNL Catalog Service]  e integrarlo con aplicaciones de front-end y servicios de terceros.
role: Admin, Developer
exl-id: ee178e67-519d-4283-8de8-2634ae1f347a
source-git-commit: 377a2b9e42378640aee034eda1426b049c173aad
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Introducción a [!DNL Catalog Service]

Una vez habilitado [!DNL Catalog Service], puede obtener acceso al servicio y utilizarlo para recuperar datos de catálogo, como información de productos y categorías, de la instancia de Adobe Commerce. El servicio está disponible como API de GraphQL a la que puede acceder desde el administrador de Commerce o desde cualquier aplicación de front-end que admita consultas de GraphQL.

## Acceso al servicio

[!DNL Catalog Service] está disponible como una API de GraphQL a la que puede acceder desde el administrador de Commerce o desde cualquier aplicación de front-end que admita consultas de GraphQL. El servicio está disponible en entornos SaaS y PaaS.

[!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."}

| Entorno | Extremo |
| ------------ | ----------: |
| **Pruebas** | `https://catalog-service-sandbox.adobe.io/graphql` |
| **Producción** | `https://catalog-service.adobe.io/graphql` |

[!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."}

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

Si utiliza la tienda de Adobe Commerce en Edge Delivery Services, agregue el punto final del servicio de catálogo a la configuración de la tienda. Para obtener más información, consulte la [documentación de Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/#storefront-configuration).

Para otras integraciones, consulte la documentación de configuración del proyecto para obtener más información sobre cómo configurar integraciones entre el servicio y las fuentes de datos back-end.

### Configuración del cortafuegos

Para permitir que [!DNL Catalog Service] pase a través de un firewall, agregue `commerce.adobe.io` a la lista de permitidos.

## Servicio de catálogo y malla de API

La [malla de API para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) permite a los desarrolladores integrar API privadas o de terceros y otras interfaces con productos de Adobe mediante Adobe IO.

Consulte el tema [[!DNL Catalog Service] y API Mesh](mesh.md) para obtener detalles de instalación y configuración.

## Uso del panel de administración de datos

Use [Panel de administración de datos](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard) para supervisar la sincronización de datos entre [!DNL Catalog Service] y su instancia de Adobe Commerce. El panel proporciona información sobre el proceso de transferencia de datos, incluido el estado de las exportaciones de datos y una lista de productos sincronizados.