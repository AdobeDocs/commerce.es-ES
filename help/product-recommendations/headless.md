---
title: Headless
description: Aprenda a integrar [!DNL Product Recommendations] en una tienda sin encabezado.
exl-id: c40dac31-f87e-402a-ba50-e8aa4c1d66aa
source-git-commit: 1548b7e11249febc2cd8682581616619f80c052f
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Headless

Puede integrar a [!DNL Product Recommendations] en una tienda sin encabezado usando [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) o una tecnología de front-end personalizada, como React o Vue JS.

Los integradores personalizados y sin encabezado deben consultar estas instrucciones de Luma y PWA como una implementación sugerida. Existen muchas maneras de implementar Recomendaciones de producto en soluciones sin encabezado, y esta documentación no cubre todos los escenarios. Los integradores deben cubrir eventos, diseño y pruebas para sus implementaciones.

[!DNL Product Recommendations] requiere [datos de catálogo y comportamiento](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/development-overview.html?lang=es) para funcionar. El proceso de sincronización de datos del catálogo permanece sin cambios en una implementación sin encabezado, pero se necesitan cambios para la recopilación de datos de comportamiento.

>[!NOTE]
>
>Las instancias sin encabezado deben implementar eventos para activar el panel Recomendaciones de productos.

Para integrar [!DNL Product Recommendations] en una tienda sin encabezado, debes:

1. Envíe datos de comportamiento a Adobe Sensei para analizar y calcular los resultados de recomendaciones de productos. También puede enviar datos adicionales para habilitar la recomendación de productos [informes de métricas](workspace.md).

1. Busque resultados de recomendaciones de productos y procese esos resultados en la página.

Puede realizar ambas acciones utilizando los SDK disponibles como se describe en el siguiente flujo de trabajo.

1. [Instalar](install-configure.md) el módulo [!DNL Product Recommendations].

1. Instale y use [Adobe Commerce Storefront Event SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/) para activar [eventos de comportamiento](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations).

   El mínimo de eventos requeridos para devolver [!DNL Product Recommendations] resultados:

   | Evento | Categoría |
   |--- | ---|
   | `view` | producto |
   | `add-to-cart` | producto |
   | `place-order` | pago y envío |

   Para habilitar [métricas que informan](workspace.md), se requieren los siguientes eventos adicionales:

   | Evento | Categoría |
   |--- | ---|
   | `impression-render` | recommendation-unit |
   | `view` | recommendation-unit |
   | `rec-click` | recommendation-unit |
   | `rec-add-to-cart-click` | recommendation-unit (si hay un botón &quot;Agregar al carro de compras&quot; en la plantilla de recomendaciones) |

1. Cuando se activen los eventos, usa el [Recopilador de eventos de Adobe Commerce Storefront](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/) para controlar los eventos y enviarlos a Adobe Sensei.

1. Una vez recopilados los datos de comportamiento, puede [crear](create.md) [!DNL Product Recommendations] en el administrador.

1. Use [Recommendations SDK](https://developer.adobe.com/commerce/services/product-recommendations/) para recuperar las unidades de recomendación en la tienda. SDK devuelve los datos de producto necesarios para procesar las unidades de recomendación en una página.

1. Aprenda a utilizar la consulta de GraphQL [`recommendations` &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) para devolver información sobre bloques de recomendaciones de productos para una SKU determinada y mucho más.
