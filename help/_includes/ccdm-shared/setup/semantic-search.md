---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%
---
La búsqueda semántica utiliza IA para comprender qué significan los compradores, no solo las palabras exactas que escriben. Consultas como &quot;vestido para una boda en la playa&quot; o &quot;zapatos cómodos para estar de pie todo el día&quot; pueden devolver productos relevantes incluso cuando su catálogo no utiliza esas frases exactas.

El sistema de detección de productos combina la coincidencia de palabras clave y la coincidencia semántica en una experiencia de búsqueda. No se administran modos semánticos y de palabra clave independientes en la tienda.

## Configuración de la búsqueda semántica

La búsqueda semántica está **habilitada de manera predeterminada** para los catálogos en inglés aptos. Lo administra en la ficha **[!UICONTROL Advanced search]** del área de trabajo [Configuración](../settings.md#advanced-search), donde puede confirmar o cambiar la configuración y, opcionalmente, ajustar el aumento semántico, el umbral de similitud y la búsqueda difusa. Consulte [Configuración](../settings.md#access-the-settings-workspace) para ver cómo abrir el área de trabajo.

No es necesario publicar una configuración independiente ni cambiar la configuración de la tienda después de guardar.

## Ventajas

- **Menos páginas de búsqueda vacías**: los compradores encuentran productos cuando su redacción no coincide exactamente con el texto del catálogo.
- **Mejor coincidencia de intención**: las consultas naturales y descriptivas devuelven resultados útiles.
- **Mantenimiento de sinónimos menos**: las variaciones de palabras comunes (por ejemplo, sofá y sofá) suelen manejarse sin listas de sinónimos manuales.
- **No hay tienda ni trabajo de desarrollador**: la búsqueda semántica está habilitada de manera predeterminada y no requiere ningún cambio de código de tema, lista desplegable o API.

## Cómo funciona

Cuando la búsqueda semántica está habilitada, el sistema utiliza atributos de catálogo predefinidos (como el nombre y la descripción del producto) para interpretar el significado de la consulta junto con la búsqueda de palabras clave tradicional. No selecciona ni prioriza atributos en Configuración.

Por ejemplo:

- Una búsqueda de &quot;sofá de cuero&quot; puede devolver productos etiquetados como &quot;sofá de cuero&quot;.
- &quot;Vestido de primavera&quot; puede salir a la superficie vestidos de temporada incluso cuando &quot;primavera&quot; no está en el nombre del producto.
- &quot;Zapatos para trail running&quot; puede hacer juego con productos descritos como calzado fuera de carretera o de senderismo.

## Qué sucede cuando se habilita la búsqueda semántica

La búsqueda semántica funciona junto con la configuración de búsqueda existente. No reemplaces la búsqueda de palabras clave ni reconfigures la tienda.

Cuando la búsqueda semántica está activa:

- Se siguen aplicando las [reglas de comercialización](../merchandising/rules/overview.md), los [sinónimos](../merchandising/synonyms/overview.md), las [facetas](../merchandising/facets/overview.md), los amplificadores y los filtros existentes.
- La búsqueda semántica agrega una comprensión basada en IA de la intención del comprador para mejorar la relevancia de los resultados junto con la coincidencia de palabras clave.
- Los atributos de catálogo predefinidos se indexan automáticamente. No seleccione atributos ni publique una configuración independiente.

## Validar después de la activación

Una vez que la búsqueda semántica esté activa y la indexación se complete, Adobe recomienda validar el rendimiento de la búsqueda. Utilice la página [Rendimiento de la búsqueda](../manage-results/search-performance.md) para revisar las métricas y las consultas de prueba que importan a su negocio.

1. Revise los términos más buscados en el informe **Búsquedas únicas**.
1. Probar consultas históricas de resultados cero a partir del informe **Resultados cero** en la tienda.
1. Compare los resultados de búsqueda para las mismas consultas antes y después de la activación.
1. Monitorice las métricas de conversión y participación de búsqueda, incluida la tasa de pulsaciones, la tasa de conversión y la tasa de resultados cero.

## Prácticas recomendadas

- Utilice nombres y descripciones de productos claros y descriptivos (idealmente 50-100 palabras) para que tanto la palabra clave como la coincidencia semántica tengan texto de catálogo sólido con el que trabajar.
- Comience con la configuración predeterminada **[!UICONTROL Enable semantic search]** y, a continuación, ajuste **[!UICONTROL Semantic boost]** o **[!UICONTROL Similarity threshold]** solo si los resultados son demasiado amplios o demasiado estrechos.
- Use [sinónimos](../merchandising/synonyms/overview.md) específicos de la marca o muy técnicos donde la búsqueda semántica pueda no cubrir términos especializados.

## Resolución de problemas

| Problema | Qué hacer |
| --- | --- |
| No hay cambios en la tienda justo después de guardar | Espere a que termine la indexación. Los catálogos grandes pueden tardar más. |
| Los resultados parecen demasiado amplios | Subir **[!UICONTROL Similarity threshold]** o bajar **[!UICONTROL Semantic boost]** en la ficha **[!UICONTROL Advanced search]**. |
| Los resultados se sienten demasiado estrechos | Bajar **[!UICONTROL Similarity threshold]** o subir **[!UICONTROL Semantic boost]**. |
| La búsqueda semántica no está disponible | Confirmar que **[!UICONTROL Language]** está establecido en **inglés**. |

## Limitaciones {#semantic-search-limitations}

- **Idioma del catálogo:** La búsqueda semántica solo está disponible para los catálogos en **inglés**.

## Más ayuda sobre este tema

- [Búsqueda avanzada](../settings.md#advanced-search)
- [Sinónimos](../merchandising/synonyms/overview.md)
- [Rendimiento de búsqueda](../manage-results/search-performance.md)
