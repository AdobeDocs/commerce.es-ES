---
title: Prácticas recomendadas para facetas
description: Conozca las prácticas recomendadas para implementar facetas en su tienda.
role: Admin, Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# Prácticas recomendadas para facetas

La funcionalidad de filtro y faceta es un componente crítico del sitio [!DNL Adobe Commerce Optimizer], diseñado para mejorar la experiencia del comprador, ya que permite que los compradores reduzcan los resultados de búsqueda y encuentren los productos de manera más eficiente. Esta funcionalidad ayuda a los compradores a revisar vastos catálogos de artículos mediante la aplicación de criterios específicos, lo que hace que el proceso de compra sea más rápido, fácil y satisfactorio. Al implementar filtros y facetas eficaces y fáciles de usar para los compradores, puede ayudar a los clientes a encontrar exactamente lo que necesitan de forma rápida y eficaz, lo que a la larga aumenta la satisfacción y las tasas de conversión.

## Sugerencias para optimizar las facetas

- Determine los atributos más relevantes y útiles para sus productos, tales como título, categoría, marca, rango de precios, color y tamaño, y configúrelos como [facetas dinámicas](type.md). 
- Establezca y ordene atributos de producto que sean coherentes en todo el catálogo y altamente relevantes para sus productos a fin de mejorar la relevancia y las capacidades de filtrado para sus compradores.
- Asegúrese de que las etiquetas de faceta sean fáciles de entender y de que tengan nombres coherentes en todo el sitio. Por ejemplo, utilice &quot;Intervalo de precios&quot; en lugar de &quot;Costo&quot;.
- Evite abrumar a los compradores limitando el número de facetas a las más importantes. Demasiadas opciones pueden causar fatiga de decisión. De manera predeterminada, [!DNL Adobe Commerce Optimizer] está limitado a un máximo de 100 atributos configurados como facetas y 30 contenedores devueltos dentro de cada faceta. Más información sobre [limitaciones de facetas](../../boundaries-limits.md#catalog-views-and-policies). 
- Permite que los compradores seleccionen varios criterios de filtro simultáneamente para restringir los resultados. Por ejemplo, permitir que los compradores seleccionen los colores &quot;Rojo&quot; y &quot;Azul&quot;.
- Muestre el número de productos disponibles junto a cada opción de faceta para que los compradores tengan una idea de los resultados de búsqueda que pueden esperar.
- Implemente secciones de facetas contraíbles para mantener la interfaz limpia y manejable, especialmente en dispositivos móviles.
- Permite que los compradores restablezcan fácilmente facetas individuales o todos los filtros seleccionados para iniciar una nueva búsqueda.
- Si tiene un gran número de atributos con los que lidiar, considere la posibilidad de combinar atributos en un único &quot;metaatributo&quot;. Por ejemplo, los zapatos generalmente tienen tallas numéricas, mientras que las camisas suelen tener el tamaño &quot;S/M/L/XL&quot;. Estos dos tipos de tamaños se pueden combinar en un único atributo en el que se puede buscar.
