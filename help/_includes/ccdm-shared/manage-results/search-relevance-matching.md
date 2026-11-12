---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%
---
>[!IMPORTANT]
>
>La siguiente característica está en [versión beta privada](https://experienceleague.adobe.com/es/docs/commerce-operations/release/beta).

Los servicios de comercialización con el modelo de datos de catálogo compuesto (CCDM) clasifican los resultados para que los compradores vean primero los productos más relevantes. El servicio aumenta los productos cuyo texto de catálogo **coincide estrechamente** con la consulta del comprador; a continuación, favorece las coincidencias donde los términos aparecen juntos y, finalmente, incluye coincidencias más amplias.

## Prioridad de las coincidencias

La relevancia utiliza tres capas de intensidad coincidente (además de otros factores de puntuación que se describen a continuación):

1. **Coincidencia exacta y cercana de la frase**: la frase de búsqueda completa coincide con el texto del catálogo o con una coincidencia cercana después de la normalización, como la derivación (por ejemplo, los formularios singular y plural se resuelven en la misma raíz). Estas coincidencias reciben el impulso de relevancia más alto.

1. **Todas las palabras del mismo campo**: cada palabra de consulta aparece en un atributo en el que se puede buscar (por ejemplo, `red` y `pants` en el producto **name**). Esta capa recibe el siguiente aumento más alto.

1. **Palabras en diferentes campos**: los términos de consulta aparecen en atributos en los que se pueden realizar búsquedas diferentes (por ejemplo, `red` en **color** y `pants` en **nombre**). Esta capa de coincidencia es la más amplia y recibe el impulso de relevancia más bajo. También puede coincidir con consultas parciales utilizadas por el completado automático, por ejemplo, cuando un comprador escribe `red pan` antes de finalizar `pants`. Para ver los catálogos alemanes, consulte [Descomposición (alemán)](#decompounding-german).

### Ejemplo

Para una consulta como `red pants`:

- Los productos con la frase exacta **pantalones rojos** (o una variante cercana) tienen el rango **primero**.
- Los productos en los que **red** y **pantalones** aparecen en el **mismo campo** (por ejemplo, **name**) tienen la siguiente clasificación.
- A continuación aparecen los productos cuyos términos aparecen en **campos diferentes** (por ejemplo, **color** y **nombre**).

### Descomposición (alemán) {#decompounding-german}

Los catálogos alemanes utilizan muchas palabras compuestas. Por ejemplo, **spülbecken** y **spül becken** se pueden descomponer en tokens como **spul** y **beck** (después de la descomposición) para que un comprador que busque **spul becken** pueda encontrar **Spülbecken**. En esta capa, las subpalabras descompuestas de un término compuesto deben aparecer en el mismo campo. Otros términos de consulta pueden coincidir en diferentes campos.

Este requisito **AND** filtra coincidencias irrelevantes donde solo hay una subpalabra presente. Por ejemplo, una búsqueda de **Brauseschlauch** ya no devuelve **Schlauchstück** cuando solo parte del compuesto coincide. La búsqueda de **spülbecken** aún puede coincidir con **spülbeckventil** porque la palabra más larga contiene todos los tokens esperados.

>[!NOTE]
>
>La coincidencia exacta y cercana de frases y la coincidencia del mismo campo utilizan las reglas descritas anteriormente sin descomposición.

#### Ejemplo

Para una frase de búsqueda como `Brauseschlauch chrom`:

- **Coincidencia exacta y cercana de la frase**: busca la frase completa **brauseschlauch chrom** tal como se escribe, sin descomponer (se sigue aplicando la derivación).
- **Todas las palabras del mismo campo** — Busca **brauseschlauch** y **chrom** en el atributo **same** en el que se puede buscar, sin descomponer (por ejemplo, ambos en **name**).
- **Palabras en diferentes campos** — Descompone **Brauseschlauch** en **brause** y **schlauch**. Estos tokens deben aparecer en el campo **same** (no necesariamente como una frase adyacente). **chrom** puede coincidir en un campo **diferente** (por ejemplo, **brause** y **schlauch** en **name**, **chrom** en **color**).

Establece **Idioma** a **Alemán** en la ficha [Idioma](../settings.md#language) de [Configuración](../settings.md), de modo que se apliquen las reglas de descomposición. Valide consultas alemanas de alto valor en una tienda de ensayo antes de habilitar los cambios en la producción.

La descomposición se basa en reglas y puede añadir casos extremos en esta capa. Si falta una subpalabra en el diccionario, la tokenización está incompleta y devuelve coincidencias más amplias de lo esperado; por ejemplo, **gas** que falta en **gaszähler** emite solamente **zahl**, o **stat** que falta en **thermostat**. El stemmer también puede producir raíces inesperadas (por ejemplo, **schrauber** que se derivan de **schraub** o **schelle** a **schell**). Adobe actualiza el diccionario y las invalidaciones de sistema para los casos conocidos a medida que se identifican problemas.

## Qué más afecta a la clasificación

La coincidencia de frases por sí sola no determina la relevancia. Interactúan varias señales:

- Aumento desde **exacto / cerca de** coincidencia de frase
- Aumentar cuando **todos los términos de consulta** aparezcan en el campo **igual**
- **Clasificación inteligente** (cuando está habilitada), que mezcla la relevancia textual con señales de comportamiento. Vea [Cómo funciona la puntuación de clasificación inteligente](../merchandising/rules/add.md#how-intelligent-ranking-scoring-works-search)
- **[Peso de búsqueda](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/catalog/search/search-results)** en cada atributo y otros factores de relevancia textual (por ejemplo, la frecuencia con la que se producen los términos en la longitud del nombre o la descripción). En *Configuración*, configure qué atributos participan en la búsqueda de palabras clave y sus **[pesos relativos de búsqueda de palabras clave](../settings.md)**.
- **[Reglas de comercialización](../merchandising/rules/overview.md)** como fijar, aumentar y enterrar

Debido a que las señales interactúan, una coincidencia amplia a veces se clasifica por encima de una coincidencia de frase más estricta cuando **los pesos de búsqueda** o la frecuencia de los términos superan a una coincidencia de frase más débil.

**Ejemplo:** Si **pantalones rojos** aparecen en **descripción** con **peso de búsqueda = 1**, pero **rojo** y **pantalones** aparecen por separado en **nombre** y **color** con **peso de búsqueda = 10**, la coincidencia dividida supera a la coincidencia de la frase.

Las reglas **pin** y **bury** manuales siguen siendo sólidas; las reglas **boost** pueden requerir un ajuste para superar los nuevos aumentos de frase y del mismo campo. Valide consultas importantes después de cambiar pesos o reglas.

### Peso de búsqueda 1 e indexación combinada

Los atributos con **peso mínimo de búsqueda** (peso **1**) y sin modos de coincidencia especiales se combinan en un único campo interno (`defaultSearchField`) para reducir la sobrecarga de asignación. Trátelo como una superficie en la que se puede buscar la coincidencia de **mismo campo**: los tokens que solo aterrizan en esos campos combinados de bajo peso se evalúan juntos en lugar de como campos independientes por atributo. Adobe puede refinar esta optimización con el tiempo a medida que evolucionan las correspondencias.

## Temas relacionados

- [Configuración](../settings.md)
- [Rendimiento de búsqueda](search-performance.md)
- [Resumen sobre reglas de comercialización](../merchandising/rules/overview.md)
- [Agregar reglas de búsqueda](../merchandising/rules/add.md)
- [Resumen de sinónimos](../merchandising/synonyms/overview.md)
