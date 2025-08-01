---
title: Resumen de facetas
description: Obtenga información acerca de las facetas de  [!DNL Adobe Commerce Optimizer]  y cómo mejoran los resultados de búsqueda.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
exl-id: cf16626e-8f85-47ca-b973-891b16c31fe3
source-git-commit: ad8fb7d1d7e1ad124647ba84377079dcfbd46a3c
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Facetas

Las facetas son un método de filtrado de alto rendimiento que utiliza varias dimensiones de valores de atributo como criterios de búsqueda.

![Resultados de búsqueda filtrados](../../assets/storefront-search-results-run.png)

Dentro de una faceta, los compradores pueden seleccionar varias opciones, como &quot;Básico&quot; y &quot;Cómodo&quot; en &quot;Estilo&quot;, y los resultados de la búsqueda se actualizan para mostrar solo esos estilos. Del mismo modo, si un comprador selecciona opciones en todas las facetas, como &quot;Básico&quot; en &quot;Estilo&quot; e &quot;Interior&quot; en &quot;Clima&quot;, los resultados de la búsqueda se actualizan para mostrar ese estilo seleccionado y ese clima seleccionado.

Cualquier faceta definida puede utilizarse como parámetro de URL y los resultados se filtrarán según los valores del parámetro: `http://yourstore.com?brand=acme&color=red`.

## Agregación de facetas

La agregación de facetas se realiza de la siguiente manera: si la tienda tiene tres facetas (categorías, color y precio) y el comprador filtra las tres (color = azul, el precio va de 10,00 a 50,00 $, categorías = `promotions`).

- Agregación `categories`: agrega `categories` y, a continuación, aplica los filtros `color` y `price`, pero no el filtro `categories`.
- Agregación `color`: agrega `color` y, a continuación, aplica los filtros `price` y `categories`, pero no el filtro `color`.
- Agregación `price`: agrega `price` y, a continuación, aplica los filtros `color` y `categories`, pero no el filtro `price`.

## Valores de atributo predeterminados

Los siguientes atributos de producto son utilizados por [!DNL Adobe Commerce Optimizer] y están habilitados de manera predeterminada.

| Propiedad | Descripción | Atributo |
|---|---|---|
| Ordenable | Se utiliza para ordenar en la lista de productos | `price` |
| Buscable | Uso en la búsqueda | `price` <br />`sku`<br />`name` |

Consulte la [API de metadatos de ingesta de datos](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#metadata) para obtener más información sobre los atributos del producto y sus propiedades.

## Propiedades de atributo predeterminadas que no son del sistema

En la tabla siguiente se muestran las propiedades de búsqueda y filtrado predeterminadas de los atributos que no son del sistema. Si establece la propiedad del atributo *Use in Search* en `Yes`, se podrá buscar en el atributo en [!DNL Adobe Commerce Optimizer].

| Código de atributo | Buscable |
|--- |--- |
| actividad | Sí |
| attributes_brand | Sí |
| marca | Sí |
| clima | Sí |
| collar | Sí |
| color | Sí |
| coste | Sí |
| eco_collection |
| género | Sí |
| fabricante | Sí |
| material | Sí |
| propósito | Sí |
| strap_bags | Sí |
| style_general | Sí |

## Propiedades predeterminadas de atributos del sistema

En la tabla siguiente se muestran la búsqueda predeterminada y las propiedades filtrables de los atributos del sistema.

| Código de atributo | Buscable |
|--- |--- |
| allow_open_amount | Sí |
| description | Sí |
| name | Sí |
| precio | Sí |
| short_description | Sí |
| sku | Sí |
| status | Sí |
| tax_class_id | Sí |
| url_key | Sí |
| peso | Sí |
