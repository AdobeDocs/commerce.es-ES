---
title: '[!DNL Live Search] eventos'
description: Descubra cómo los eventos recopilan datos para  [!DNL Live Search].
feature: Services, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# [!DNL Live Search] eventos

[!DNL Live Search] utiliza eventos para activar algoritmos de búsqueda como &quot;Más visitados&quot; y &quot;Visualizó esto, Visualizó aquello&quot;. Mientras que el [tema de Luma de muestra de Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/design/themes/themes#the-default-theme) obtiene eventos de forma predeterminada, las implementaciones sin encabezado y otras personalizadas tienen que implementar eventos para sus propias necesidades.

En esta tabla se describen los eventos utilizados por [!DNL Live Search] [estrategias de clasificación](rules-add.md#intelligent-ranking).

| Estrategia de clasificación | Eventos | Página |
| --- | --- | --- |
| Más visitados | `page-view`<br>`product-view` | Página de detalles del producto |
| Más comprados | `page-view`<br>`complete-checkout` | Carro/cierre de compra |
| Más añadidos al carro | `page-view`<br>`add-to-cart` | Página de detalles del producto<br>Página de lista de productos<br>Carro<br>Lista de deseos |
| Vio esto, vio aquello. | `page-view`<br>`product-view` | Página de detalles del producto |

>[!NOTE]
>
>La recopilación de datos a los efectos de [!DNL Live Search] no incluye información de identificación personal (PII). Todos los identificadores de usuario, como los ID de cookie y las direcciones IP, se anonimizan estrictamente. [Más información](https://www.adobe.com/privacy/experience-cloud.html).

## Eventos de panel requeridos

Se requieren algunos eventos para rellenar el [tablero de Live Search](performance.md)

| Área de panel | Eventos | Campo de combinación |
| ------------------- | ------------- | ---------- |
| Búsquedas únicas | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Búsquedas sin resultados | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Tasa de resultados cero | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Búsquedas frecuentes | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| El Promedio de posición del clic | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click` | `searchRequestId` |
| Tasa de pulsaciones | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click` | `searchRequestId`, `sku`, `parentSku` |
| Tasa de conversión | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click`, `product-view`, `add-to-cart`, `place-order` | `searchRequestId`, `sku`, `parentSku` |

### Contextos requeridos

Todos los eventos requieren los contextos `Page` y `Storefront`. Esto debería suceder en el nivel de página/capa de aplicación de tienda en lugar de cuando se generan eventos individuales (por ejemplo, en una tienda PHP, el contenedor de la aplicación PHP es responsable de configurarlos durante la ejecución).

## Uso

Esta es una implementación de ejemplo del evento `search-request-sent`:

```javascript
const mse = window.magentoStorefrontEvents;

/* set in application container */
// mse.context.page(pageCtx);
// mse.context.setStorefrontInstance(storefrontCtx);

/* set before firing event */
mse.context.setSearchInput(searchInputCtx);
mse.publish.searchRequestSent("search-bar");
```

## Advertencias

- Los bloqueadores de anuncios y la configuración de privacidad pueden impedir que se recopilen eventos y provocar que las [métricas](performance.md) de participación e ingresos no se comuniquen correctamente. Además, es posible que algunos eventos no se envíen debido a que los compradores abandonan la página o a problemas de red.
- Las implementaciones sin encabezado deben implementar eventos para potenciar la comercialización inteligente.

>[!NOTE]
>
>Si el [Modo de restricción de cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html) está habilitado, Adobe Commerce no recopilará datos de comportamiento hasta que el comprador acepte el uso de cookies. Si el modo de restricción de cookies está deshabilitado, Adobe Commerce recopila datos de comportamiento de forma predeterminada.
