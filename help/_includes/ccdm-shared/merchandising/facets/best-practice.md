---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%
---
La funcionalidad de filtro y faceta es un componente esencial de las experiencias de Commerce, diseñado para mejorar la experiencia del comprador, ya que permite que los compradores reduzcan los resultados de búsqueda y encuentren los productos de forma más eficaz. Esta funcionalidad ayuda a los compradores a revisar vastos catálogos de artículos mediante la aplicación de criterios específicos, lo que hace que el proceso de compra sea más rápido, fácil y satisfactorio. Al implementar filtros y facetas eficaces y fáciles de usar para los compradores, puede ayudar a los clientes a encontrar exactamente lo que necesitan de forma rápida y eficaz, lo que a la larga aumenta la satisfacción y las tasas de conversión.

## Sugerencias para optimizar las facetas

- Determine los atributos del producto relevantes, tales como título, categoría, marca, rango de precios, color y tamaño, y configúrelos como [facetas dinámicas](type.md). 
- Establezca y ordene atributos de producto que sean coherentes en todo el catálogo y altamente relevantes para sus productos a fin de mejorar la relevancia y las capacidades de filtrado para sus compradores.
- Asegúrese de que las etiquetas de faceta sean fáciles de entender y de que tengan nombres coherentes en todo el sitio. Por ejemplo, use `Price Range` en lugar de `Cost`.
- Evite abrumar a los compradores limitando el número de facetas a las más importantes. Demasiadas opciones pueden causar fatiga de decisión. De forma predeterminada, la configuración de faceta está limitada a un máximo de 100 atributos configurados como facetas y 30 contenedores devueltos dentro de cada faceta. Más información sobre [limitaciones de facetas](/help/optimizer/boundaries-limits.md#catalog-views-and-policies). 
- Permite que los compradores seleccionen varios criterios de filtro simultáneamente para restringir los resultados. Por ejemplo, permitir que los compradores seleccionen los colores &quot;Rojo&quot; y &quot;Azul&quot;.
- Muestre el número de productos disponibles junto a cada opción de faceta para que los compradores tengan una idea de los resultados de búsqueda que pueden esperar.
- Para mantener la interfaz limpia y manejable, especialmente en dispositivos móviles, implemente secciones de faceta contraíbles.
- Permite que los compradores restablezcan facetas individuales o todos los filtros seleccionados para iniciar una nueva búsqueda fácilmente.
- Si tiene un gran número de atributos, considere la posibilidad de combinar atributos en un único metaatributo. Por ejemplo, los zapatos tienen tallas numéricas, mientras que las camisas suelen tener el tamaño &quot;S/M/L/XL&quot;. Estos dos tipos de tamaños se pueden combinar en un único atributo en el que se puede buscar.
