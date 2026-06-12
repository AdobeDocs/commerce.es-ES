---
title: Coincidencia y clasificación de búsqueda
description: Aprenda cómo  [!DNL Adobe Commerce Optimizer] prioriza las coincidencias exactas y cercanas, las coincidencias del mismo campo y las coincidencias entre campos, y cómo la clasificación interactúa con las ponderaciones de búsqueda, la clasificación inteligente y las reglas de comercialización.
role: Admin, Leader, User
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
hide: true
autotag-review: '2026-06-12T19:49:25.241Z'
TQID: 'https://experienceleague.adobe.com/GBfssL1pTVx4FKjsi45mDsTx2XyCr0aViexH3OpPjVo'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
subfeature_v2: id: faf75e43-5608-48b8-8169-3f8a9b8a5caf
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: d378ca77-2da1-4f39-ad92-1917fe974a38
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: da5950c0f2071f48f163dd02f6c38953804ae152
workflow-type: tm+mt
source-wordcount: 946
ht-degree: 0%

---

# Coincidencia y clasificación de búsqueda

>[!IMPORTANT]
>
>La siguiente característica está en [versión beta privada](https://experienceleague.adobe.com/en/docs/commerce-operations/release/beta).

[!DNL Adobe Commerce Optimizer] clasifica los resultados para que los compradores vean primero los productos más relevantes. El servicio da el mayor impulso a los productos cuyo texto de catálogo **coincide de cerca** con lo que el comprador escribe; a continuación, favorece las coincidencias donde los términos de consulta aparecen juntos de manera significativa y, finalmente, incluye coincidencias más amplias (incluido el comportamiento que admite la coincidencia de estilo autocompletado).

## Prioridad de las coincidencias

En un nivel superior, la relevancia utiliza tres capas de intensidad coincidente (además de otros factores de puntuación descritos a continuación):

1. **Coincidencia exacta y cercana de la frase**: la frase de búsqueda completa coincide con el texto del catálogo o con una coincidencia cercana después de la normalización, como la derivación (por ejemplo, los formularios singular y plural se resuelven en la misma raíz). Estas coincidencias reciben el impulso de relevancia más alto.

1. **Todas las palabras del mismo campo**: todas las palabras de la consulta aparecen en un atributo en el que se puede buscar (por ejemplo, tanto `red` como `pants` en el producto **name**). Esta capa recibe el siguiente aumento más alto.

1. **Palabras en diferentes campos**: los términos de consulta aparecen en atributos en los que se pueden realizar búsquedas diferentes (por ejemplo, `red` en **color** y `pants` en **nombre**). Esta es la capa de coincidencia más amplia y recibe el impulso de relevancia más bajo. También puede coincidir con consultas parciales utilizadas por el completado automático, por ejemplo, cuando un comprador escribe `red pan` antes de finalizar `pants`. Para ver los catálogos alemanes, consulte [Descomposición (alemán)](#decompounding-german).

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

Establece **Idioma** a **Alemán** en la ficha [Idioma](./settings.md#language) de [Configuración](./settings.md), de modo que se apliquen las reglas de descomposición. Valide consultas alemanas de alto valor en una tienda de ensayo antes de habilitar los cambios en la producción.

La descomposición se basa en reglas y puede añadir casos extremos en esta capa. Si falta una subpalabra en el diccionario, la tokenización puede estar incompleta y devolver coincidencias más amplias de lo esperado; por ejemplo, **gas** que falta en **gaszähler** puede emitir solamente **zahl**, o **stat** que falta en **thermostat**. El stemmer también puede producir raíces inesperadas (por ejemplo, **schrauber** que se derivan de **schraub** o **schelle** a **schell**). Adobe actualiza el diccionario y las invalidaciones de sistema para los casos conocidos a medida que se identifican problemas.

## Qué más afecta a la clasificación

La relevancia no está determinada únicamente por la coincidencia de frases. Interactúan varias señales:

- Aumento desde **exacto / cerca de** coincidencia de frase
- Aumentar cuando **todos los términos de consulta** aparezcan en el campo **igual**
- **Clasificación inteligente** (cuando está habilitada), que mezcla la relevancia textual con señales de comportamiento. Vea [Cómo funciona la puntuación de clasificación inteligente](./merchandising/rules/add.md#how-intelligent-ranking-scoring-works-search)
- **[Busque peso](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results)** en cada atributo y otros factores de relevancia textual (por ejemplo, la frecuencia con la que se producen los términos y la longitud del nombre o la descripción). En *Configuración*, configure qué atributos participan en la búsqueda de palabras clave y sus **[pesos relativos de búsqueda de palabras clave](./settings.md)**.
- **[Reglas de comercialización](./merchandising/rules/overview.md)** como fijar, aumentar y enterrar

Debido a que estas señales interactúan, un producto que coincide solamente en el nivel más amplio a veces puede clasificarse por encima de una coincidencia de frase más ajustada; por ejemplo, cuando **los pesos de búsqueda** o la frecuencia de término en un campo de alto peso superan a una coincidencia de frase más débil en cualquier otra parte.

**Ejemplo:** Si **pantalones rojos** aparece como una frase en **descripción** con **peso de búsqueda = 1**, pero **pantalones rojos** y **11} aparecen por separado en** nombre **y** color **con** peso de búsqueda = 10 **, es posible que la frase que coincida en** descripción **no supere la coincidencia dividida, dependiendo de la puntuación general.**

Las reglas **pin** y **bury** manuales siguen siendo sólidas; las reglas **boost** pueden requerir un ajuste para superar los nuevos aumentos de frase y del mismo campo. Valide consultas importantes después de cambiar pesos o reglas.

### Peso de búsqueda 1 e indexación combinada

Los atributos configurados con **peso mínimo de búsqueda** (peso **1**) y **no** configurados para modos de coincidencia especiales (como contiene o empieza por) pueden combinarse en el índice de búsqueda en un único campo interno (`defaultSearchField`) para reducir la sobrecarga de asignación de campos. Trátelo como una superficie en la que se puede buscar la coincidencia de **mismo campo**: los tokens que solo aterrizan en esos campos combinados de bajo peso se evalúan juntos en lugar de como campos independientes por atributo. Adobe puede refinar esta optimización con el tiempo a medida que evolucionan las correspondencias.

## Temas relacionados

- [Configuración](./settings.md)
- [Rendimiento de búsqueda](./manage-results/search-performance.md)
- [Resumen sobre reglas de comercialización](./merchandising/rules/overview.md)
- [Agregar reglas de búsqueda](./merchandising/rules/add.md)
- [Resumen de sinónimos](./merchandising/synonyms/overview.md)
