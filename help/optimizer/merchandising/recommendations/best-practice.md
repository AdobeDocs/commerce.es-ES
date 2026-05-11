---
title: Prácticas recomendadas de Recommendations
description: Descubra dónde puede colocar recomendaciones en varias páginas del sitio y sugerencias para etiquetas utilizadas con frecuencia para cada tipo de recomendación.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
exl-id: 08d7aeff-8b86-4fa3-93e6-4b72dc1ab117
TQID: https://experienceleague.adobe.com/J4vSJ4EMfSTeL7rVEv9bTr998wvU5DR4S-hXQ3HCSGg
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2: id: bcc5edb5-84c3-4940-9f84-ed88b6c16274id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 360
ht-degree: 0%

---

# Prácticas recomendadas de Recommendations

Adobe recomienda las siguientes directrices al utilizar Recommendations:

- Diversifique los tipos de recomendaciones. Los clientes empiezan a ignorar las recomendaciones si sugieren los mismos productos una y otra vez.

- No implemente las mismas recomendaciones en la página del carro de compras y en la página de confirmación de pedidos. Considere utilizar `Most Added to Cart` para la página del carro de compras y `Bought This, Bought That` para la página de confirmación de pedido.

- Mantenga su sitio ordenado. No implemente más de tres unidades de recomendación en la misma página.

- Si su tienda vende ropa, la recomendación `More like this` puede sugerir productos específicos del sexo que no coincidan con el sexo del producto que se está viendo. Considere utilizar este tipo de recomendación solo para categorías que no sean de ropa.

## Ubicación

Con tantos tipos de recomendaciones para elegir, ¿qué debería utilizar en cada página? Si no está seguro por dónde empezar, intente lo siguiente:

| Página | Tipo de recomendación |
|---|---|
| Página de inicio | `Recommended for you` |
| Página de productos | `Viewed this, viewed that` |
| Carrito | `Bought this, bought that` |

Puede hacer un seguimiento de [métricas](../../manage-results/recommendation-performance.md) y ajustarlas si es necesario. Recuerden que la experimentación es clave.

## Etiquetas de recomendación

La etiqueta asignada a una recomendación en la tienda afecta a la forma en que los compradores interpretan su relevancia para ellos. Las siguientes etiquetas se utilizan frecuentemente para cada tipo de recomendación.

| Tipo de recomendación | Etiquetas recomendadas |
|---|---|
| Más visitados<br> Más añadidos al carrito<br>Más comprados<br>Conversión (ver al carrito)<br>Conversión (ver a la compra) | Más populares<br>Artículos populares<br>Tendencias<br>Populares en este momento<br>Artículos populares<br>Recientemente populares inspirados en este artículo (PDP)<br>Principales vendedores<br>Es posible que te interese |
| Recomendado para usted | Solo para ti<br>Recomendado para ti<br>Inspirado en tus tendencias de compras |
| Vio Esto, Vio Aquello | Los clientes que vieron este artículo también vieron <br>Los clientes también vieron<br>Artículos relacionados |
| Vio esto, Compró aquello. | Los clientes que vieron esto finalmente compraron <br>En última instancia, los clientes compraron<br>¿Qué compran otros después de ver este artículo? |
| Compró Esto, Compró Aquello. | Obtén todo lo que necesitas<br>No olvides estos<br>Comprados frecuentemente juntos |
| Más como esto | Más elementos como este<br>Similar a esto |
| Genérico | Es posible que también le gusten <br>A los compradores también les gustaron<br>Opciones similares<br>Artículos relacionados |
| Tendencia | Tendencia<br>Tendencia actual<br>Tendencia reciente<br>Artículos destacados<br>Productos relacionados con la tendencia (PDP) |
| Vistos recientemente | Vistos recientemente<br>Eche otro vistazo |
