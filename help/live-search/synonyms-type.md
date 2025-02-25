---
title: Tipos de sinónimos
description: Los sinónimos unidireccionales  [!DNL Live Search] y bidireccionales amplían la definición de palabras clave.
exl-id: f5522428-c7cc-4627-a09b-d9148918c127
source-git-commit: 81bde302463a70e41318b494565694929703dff9
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# Tipos de sinónimos

Los sinónimos unidireccionales y bidireccionales amplían la definición de palabras clave. Algunos son intercambiables con la palabra clave, mientras que otros representan un subconjunto de la palabra clave.

## Bidireccional

Los sinónimos bidireccionales tienen el mismo significado y devuelven los mismos resultados de búsqueda. En el ejemplo siguiente, la primera palabra que aparece en negrita es la palabra clave que se utiliza en el catálogo, seguida de palabras que tienen el mismo significado que la palabra clave original. Puede crear un par simple de sinónimos bidireccionales o una cadena de varios sinónimos bidireccionales para la misma palabra clave.

**chaqueta** ![chaqueta de dos vías](assets/btn-two-way.png)
**pantalones** ![Selector bidireccional](assets/btn-two-way.png) pantalones ![Selector bidireccional](assets/btn-two-way.png)

## Unidireccional

Un sinónimo unidireccional es un subconjunto de una palabra clave, pero con un significado más específico. Por ejemplo, los capris y los shorts son pantalones, pero no todos son capris o shorts. Una búsqueda de pantalones incluye capris y pantalones cortos. Sin embargo, la búsqueda de pantalones cortos no devuelve capris.

**sudadera** ![selector unidireccional](assets/btn-one-way.png) con capucha
**pantalones** ![Selector unidireccional](assets/btn-one-way.png) capris ![Selector unidireccional múltiple](assets/btn-multiple-one-way.png) pantalones de pantorrilla ![Selector unidireccional múltiple](assets/btn-multiple-one-way.png) empujadores de pedales

## Prácticas recomendadas

Tenga en cuenta las siguientes prácticas recomendadas para aprovechar al máximo los sinónimos de [!DNL Live Search].

### Evite las palabras &quot;stop&quot;

[!DNL Live Search] elimina las &quot;palabras de detención&quot; comunes del inglés de los sinónimos, como:

a, y, son, como, en, ser, pero, por, porque, si, en, en, es, no, no, de, en, o, tal, que, el, su, entonces, allí, estos, ellos, esto, a, era, voluntad, con

Las palabras de detención no hacen que los sinónimos sean más significativos, sino que aumentan la cantidad de datos que deben procesarse.

### Uso del singular y el plural

No es necesario definir las formas singular y plural de una palabra como sinónimo. Si en el catálogo existe una mezcla de términos en singular y en plural, Search busca el conjunto de productos correcto. Por ejemplo, si utiliza la palabra &quot;pantalón&quot; en el nombre del producto y un comprador busca &quot;pantalones&quot;, se devuelve el conjunto correcto de productos y la palabra singular &quot;pantalón&quot; se ofrece como sugerencia. El término singular &quot;pantalón&quot; se utiliza a menudo en la industria de la moda y a veces en el comercio minorista, aunque la forma plural &quot;pantalones&quot; se utiliza más comúnmente en algunas áreas. (La palabra &quot;pantalón&quot; se refiere técnicamente a la parte de una prenda que cubre una pierna, por lo que se necesita un &quot;par de pantalones&quot; para cubrir ambas piernas).

### Coherencia

Sea coherente con la forma en que se utiliza la terminología en su catálogo. Tenga en cuenta que puede haber diferencias regionales en el uso y, a veces, diferencias dentro de una industria.

## Comportamiento de sinónimo de varias palabras

Para los sinónimos de varias palabras, Commerce considera el sinónimo como una frase. Por ejemplo, si crea un sinónimo bidireccional **mesa de comedor** ![selector bidireccional](assets/btn-two-way.png) **mesa de cocina** ![selector bidireccional](assets/btn-two-way.png) **mesa de comedor**, Commerce buscará en todos los campos establecidos para buscar la ocurrencia de **mesa de comedor**, **mesa de cocina** o **mesa de comedor**.

Si no se crea ningún sinónimo y un comprador busca **tabla de cocina**, Commerce busca los términos en cualquier lugar de los campos en los que se puede buscar, incluso en diferentes campos, por ejemplo **tabla** en el campo de nombre y **cocina** en la palabra clave meta.

Después de crear un sinónimo, el comportamiento de búsqueda cambia para buscar la frase exacta **tabla de cocina**. Esto puede reducir el número de resultados, ya que solo se mostrarán los productos con la frase exacta.

Si quieres que los términos se busquen por separado como antes, puedes [crear un ticket de asistencia](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide). Si hay suficiente demanda, Commerce considerará la posibilidad de añadir esta funcionalidad al producto en una versión futura.
