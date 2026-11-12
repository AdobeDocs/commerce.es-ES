---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%
---
Los sinónimos unidireccionales y bidireccionales amplían la definición de palabras clave. Algunos son intercambiables con la palabra clave, mientras que otros representan un subconjunto de la palabra clave.

## Bidireccional

Los sinónimos bidireccionales tienen el mismo significado y devuelven los mismos resultados de búsqueda. En el ejemplo siguiente, la primera palabra que aparece en negrita es la palabra clave que se utiliza en el catálogo, seguida de palabras que tienen el mismo significado que la palabra clave original. Puede crear un par simple de sinónimos bidireccionales o una cadena de varios sinónimos bidireccionales para la misma palabra clave.

**chaqueta** ![chaqueta de dos vías](/help/assets/ccdm-shared/synonyms/two-way.png)
**pantalones** ![Selector bidireccional](/help/assets/ccdm-shared/synonyms/two-way.png) pantalones ![Selector bidireccional](/help/assets/ccdm-shared/synonyms/two-way.png)

## Unidireccional

Un sinónimo unidireccional es un subconjunto de una palabra clave, pero con un significado más específico. Por ejemplo, los capris y los shorts son pantalones, pero no todos son capris o shorts. Una búsqueda de pantalones incluye capris y pantalones cortos. Sin embargo, la búsqueda de pantalones cortos no devuelve capris.

**sudadera** ![selector unidireccional](/help/assets/ccdm-shared/synonyms/one-way.png) con capucha
**pantalones** ![Selector unidireccional](/help/assets/ccdm-shared/synonyms/one-way.png) capris ![Selector unidireccional](/help/assets/ccdm-shared/synonyms/one-way.png) pantalones de pantorrilla ![Selector unidireccional](/help/assets/ccdm-shared/synonyms/one-way.png) empujadores de pedales

## Comportamiento de sinónimo de varias palabras

Para los sinónimos de varias palabras, el sistema considera el sinónimo como una frase. Por ejemplo, si crea un sinónimo bidireccional de **tabla de comedor** ![selector bidireccional](/help/assets/ccdm-shared/synonyms/two-way.png) **tabla de cocina** ![selector bidireccional](/help/assets/ccdm-shared/synonyms/two-way.png) **tabla de comedor**, el sistema buscará en todos los campos configurados para buscar la ocurrencia de **tabla de comedor**, **tabla de cocina** o **tabla de comedor**.

Si no se crea ningún sinónimo y un comprador busca **tabla de cocina**, el sistema busca los términos en cualquier lugar de los campos en los que se puede buscar, incluso en diferentes campos, por ejemplo **tabla** en el campo de nombre y **cocina** en la palabra clave meta.

Después de crear un sinónimo, el comportamiento de búsqueda cambia para buscar la frase exacta **tabla de cocina**. Esto puede reducir el número de resultados, ya que solo se mostrarán los productos con la frase exacta.

Si quieres que los términos se busquen por separado como antes, puedes [crear un ticket de asistencia](https://experienceleague.adobe.com/es/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide).
