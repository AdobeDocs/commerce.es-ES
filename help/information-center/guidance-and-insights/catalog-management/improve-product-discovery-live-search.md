---
title: Mejore la detección de productos con Adobe Commerce Live Search
description: Aprenda a utilizar las perspectivas de rendimiento de búsqueda y la búsqueda semántica para ayudar a los compradores a encontrar productos relevantes.
audience: Merchandisers, commerce administrators, and store owners
autotag-review: '2026-10-21T12:57:39.807Z'
TQID: 'https://experienceleague.adobe.com/vUbbKdcd7RFb3YUNNjlW4u7AgtiXJKeZeRs9uJwxYyY'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: cdfd3bc1-dc23-5cf0-b965-d3c0c55cde67
    internal-label: Best Practices
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
source-git-commit: f54c816fd23786ec519d5c890bc2664c3dcf8c6f
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%
---

# Mejore la detección de productos con Adobe Commerce Live Search

<table style="table-layout:auto">
<tr style="border: 0;">
   <td valign="middle" style="vertical-align: middle;"><img alt="Retrato de Sandra Gonzalez Mangana" src="../../assets/guidance-and-insights/live-search-author-avatar-sgonzalezmangana.png" width="96"><br><strong>Sandra Gonzalez Mangana</strong><br><em>directora de producto sénior</em></td>
</tr>
</table>

*Ayuda a los compradores a encontrar los productos que necesitan con información sobre rendimiento de búsqueda y búsqueda semántica.*

Tener los productos adecuados en su catálogo es solo parte de la experiencia de compra. Los compradores también deben poder encontrar esos productos utilizando las palabras, frases y preguntas que utilizan de forma natural.

Adobe Commerce Live Search proporciona perspectivas de rendimiento de búsqueda que pueden ayudarle a detectar problemas de detección y a refinar la experiencia. Utilice esas perspectivas para investigar dónde tienen dificultades los compradores, no solo si la búsqueda devuelve resultados.

## Buscar señales en el rendimiento de búsqueda

En el área de trabajo Rendimiento de Live Search, revise métricas como búsquedas únicas, búsquedas de resultados cero, resultados populares, tasa de pulsaciones, tasa de conversión y posición de clics promedio. Utilícelos para identificar tendencias y decidir qué consultas o productos requieren atención. [Rendimiento](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/performance)

![El espacio de trabajo Rendimiento de Live Search muestra búsquedas únicas, posición de clics promedio, tasa de pulsaciones, tasa de conversión y tasa de resultados cero, con fichas para búsquedas únicas, resultados cero y resultados populares](../../assets/guidance-and-insights/live-search-performance-dashboard.png){width="800" zoomable="yes"}

*El área de trabajo Rendimiento de Live Search muestra las métricas que se van a revisar. Los valores mostrados son datos de ejemplo.*

Considere estas señales:

- **Búsquedas sin resultados:** Es posible que las consultas sin resultados apunten a lagunas en el catálogo, la información del producto o la configuración de búsqueda. El objetivo es mantener las búsquedas de resultados cero por debajo del 5 %. Una tasa por encima de este umbral es una señal que vale la pena investigar.
- **Pulsación baja o posición de clic débil:** Es posible que los compradores estén viendo resultados que no coinciden con sus necesidades o que los productos relevantes no sean lo suficientemente destacados. Para garantizar la participación, intente que al menos el 50 % de las búsquedas den como resultado un clic de producto.
- **Baja conversión de la búsqueda:** Revisa si la búsqueda está ayudando a los compradores a pasar de una consulta a una compra. Apunte a una tasa de conversión superior al 3 %.

Trate estas señales como puntos de referencia y señales de diagnóstico, no como una superación o fallo universal. El rendimiento varía según el sector, la complejidad del catálogo, el comportamiento del cliente y la forma en que se mide cada métrica. Establezca una línea de base para su tienda y compare el rendimiento a lo largo del tiempo. Los resultados pueden variar según el catálogo, los compradores y la forma de medir los resultados.

## Coincide con la intención del comprador, no solo con las palabras exactas

Los compradores no siempre describen los productos utilizando la terminología del catálogo. Alguien que busca &quot;zapatos cómodos para estar de pie todo el día&quot;, por ejemplo, puede estar interesado en productos descritos como &quot;zapatillas para caminar acolchadas&quot;.

La búsqueda semántica utiliza el significado y el contexto junto con la coincidencia de palabras clave, lo que ayuda a conectar las consultas en lenguaje natural a productos relevantes incluso cuando la consulta no coincide exactamente con la redacción del catálogo. Live Search combina la coincidencia semántica y de palabras clave en una experiencia de búsqueda. [Búsqueda semántica](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/semantic-search)

La coincidencia semántica puede ayudar con las búsquedas exploratorias, pero la relevancia aún depende de los productos y la información disponibles en el catálogo. Para las búsquedas que impliquen un modelo, especificación o requisito de compatibilidad exactos, compruebe que los resultados siguen siendo precisos.

## Compruebe la búsqueda semántica de la implementación

La configuración depende del producto de Adobe Commerce que utilice:

- **Adobe Commerce en infraestructura en la nube o local:** La búsqueda semántica de Live Search está disponible para Adobe Commerce 2.4.4 y versiones posteriores. En el Administrador, vaya a Marketing > SEO y búsqueda > Búsqueda en directo, abra Configuración, habilite la búsqueda semántica y guarde. Admite catálogos en inglés. [Configuración—Búsqueda semántica](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/settings)
- **Adobe Commerce as a Cloud Service:** El sistema habilita la búsqueda semántica de forma predeterminada. Admite catálogos en inglés. [Búsqueda semántica](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/semantic-search)
- **Adobe Commerce Optimizer:** El sistema habilita la búsqueda semántica de forma predeterminada. Si lo desea, puede ajustar controles como el aumento semántico y el umbral de similitud. La configuración también incluye opciones de búsqueda difusa. [Búsqueda semántica](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/semantic-search) · [Configuración—Ajuste opcional](https://experienceleague.adobe.com/en/docs/commerce/optimizer/settings)

## Convierta perspectivas de búsqueda en acción

Utilice un ciclo de revisión continua para mejorar la detección de productos:

1. **Buscar consultas para investigar.** Revise las búsquedas sin resultados, las consultas populares y las búsquedas con poca participación.
2. **Comprueba lo que pide el comprador.** Determine si la consulta señala a un producto que falta, si la redacción no coincide o si los datos del producto no son claros.
3. **Mejorar la información del producto.** Haga que los atributos y las descripciones de los productos sean precisos y útiles para los términos que utilizan los compradores. Para Live Search, Adobe recomienda configurar los atributos y pesos en los que se puede buscar y garantizar que los datos de atributos sean relevantes. [Prácticas recomendadas de Live Search](https://experienceleague.adobe.com/en/docs/commerce/live-search/best-practice)
4. **Refine la experiencia de búsqueda.** Si procede, utilice reglas de búsqueda, sinónimos y facetas para ayudar a los compradores a encontrar y reducir los resultados relevantes. [Prácticas recomendadas de Live Search](https://experienceleague.adobe.com/en/docs/commerce/live-search/best-practice)
5. **Revisar los resultados y repetir.** Supervise las mismas consultas y señales de rendimiento después de realizar cambios y, a continuación, ajuste en función de lo que hagan los compradores.

## Hacer que cada búsqueda cuente

Una consulta de búsqueda es una señal de lo que desea un comprador. Al combinar las perspectivas de rendimiento de la búsqueda con información relevante del producto y las capacidades de búsqueda adecuadas, puede facilitar a los compradores el descubrimiento de productos que satisfacen sus necesidades.

### Más información

- [¿Qué es Live Search?](../../../live-search/overview.md)
- [Prácticas recomendadas de Live Search](../../../live-search/best-practice.md)
- [Búsqueda semántica](../../../live-search/semantic-search.md) de Adobe Commerce en la infraestructura en la nube
- [Búsqueda semántica](../../../optimizer/setup/semantic-search.md) para Adobe Commerce Optimizer
