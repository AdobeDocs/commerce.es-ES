---
title: Introducción a  [!DNL Adobe Commerce Optimizer]
description: Obtenga información sobre cómo empezar a usar  [!DNL Adobe Commerce Optimizer].
hide: true
recommendations: noCatalog
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
source-git-commit: 9c3f5d1d5e7fd57d2306502d654a854bc5c66c71
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# Primeros pasos

>[!NOTE]
>
>Esta documentación describe un producto en desarrollo de acceso anticipado y no refleja todas las funcionalidades pensadas para una disponibilidad general.

Esta guía lo acompaña en la creación y el trabajo con una instancia de [!DNL Adobe Commerce Optimizer].

<!--Click the tabs below to see high-level workflow overviews for the following user types:

- Administrators
- Merchants
- Developers

>[!BEGINTABS]

>[!TAB Administrator and merchant workflow]

This diagram provides a high-level overview of how administrators and merchants access and manage [!DNL Adobe Commerce Optimizer] instances. See the [Adobe Admin Console Guide](https://helpx.adobe.com/enterprise/admin-guide.html) for more information about administrator workflows.

NEED DIAGRAM

>[!TAB Developer workflow]

This diagram provides a high-level overview of how developers create integrations for [!DNL Adobe Commerce Optimizer] using App Builder. See the [API documentation](https://developer.adobe.com/commerce/webapi/rest/) for more information.

NEED DIAGRAM

>[!ENDTABS]
-->

## Aprovisionamiento

Una vez que las instancias de [!DNL Adobe Commerce Optimizer] estén listas, el equipo de aprovisionamiento de [!DNL Adobe Commerce Optimizer] le proporcionará los siguientes extremos:

| Elemento | URL de ejemplo | Finalidad |
|---|---|---|
| IU [!DNL Adobe Commerce Optimizer] | `https://experience.adobe.com/#/@commerceprojectbeacon/commerce-optimizer-studio?tenant=<tenantId>` | Acceder a la interfaz de usuario de Commerce Optimizer para administrar el catálogo en:<br>1. Reglas de comercialización (descubrimiento de productos, recomendaciones de productos).<br>2. Administración de catálogos (creación de canales y directivas).<br>3. Perspectivas de datos (vea el estado de ingesta de datos del catálogo). |
| API de tienda | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/graphql` | Acceda a las API necesarias para configurar su tienda de Commerce con tecnología de Edge Delivery Services. |
| API de ingesta de datos de catálogo | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/v1/catalog/<entity>` | Acceda a las API necesarias para introducir los datos del catálogo. |

>[!NOTE]
>
>Consulte la [documentación para desarrolladores](https://developer-stage.adobe.com/commerce/services/composable-catalog/) para obtener más información sobre las API necesarias para la configuración de la tienda y la ingesta de catálogos.

Como participante con acceso anticipado, recibirá un mensaje de correo electrónico con un vínculo seguro que, junto con su token de IMS, le permitirá iniciar sesión en [!DNL Adobe Commerce Optimizer] o realizar llamadas a la API.

## Configurar la tienda

Ahora que tiene una instancia de [!DNL Adobe Commerce Optimizer], está listo para continuar [configurando](./storefront.md) su tienda Commerce con tecnología de Edge Delivery Services.

## Datos de catálogo disponibles para los participantes con acceso anticipado

Como participante con acceso anticipado, la instancia [!DNL Adobe Commerce Optimizer] contiene datos de catálogo ficticios basados en el [caso de uso de Carvelo](./use-case/admin-use-case.md). Los datos ficticios, junto con algunos canales y directivas preconfigurados, le ayudan a familiarizarse con la interfaz de usuario de [!DNL Adobe Commerce Optimizer].

<!--Ingest catalog data

By default, [!DNL Adobe Commerce Optimizer] instances do not include any product data.

See the [Ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) documentation to learn how you can import your catalog data into [!DNL Adobe Commerce Optimizer].

The catalog data that you ingest is visible in the [data insights](./insights-overview.md) page. Additionally, you can use the [Catalog](./catalog-overview.md) page to define the channels and policies.-->
