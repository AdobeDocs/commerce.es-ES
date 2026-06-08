---
title: Búsqueda semántica
description: Habilite la búsqueda semántica de IA en  [!DNL Adobe Commerce Optimizer]  desde Configuración. No se requiere configuración de atributos ni cambios de tienda.
role: Admin, User
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
source-git-commit: 015f88e540fe5bf7acc4469d7c91b4f606709809
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---

# Búsqueda semántica

La búsqueda semántica utiliza IA para comprender qué significan los compradores, no solo las palabras exactas que escriben. Consultas como &quot;vestido para una boda en la playa&quot; o &quot;zapatos cómodos para estar de pie todo el día&quot; pueden devolver productos relevantes incluso cuando su catálogo no utiliza esas frases exactas.

[!DNL Adobe Commerce Optimizer] combina la coincidencia semántica y de palabras clave en una experiencia de búsqueda. No se administran modos semánticos y de palabra clave independientes en la tienda. En el Administrador, vaya al área de trabajo [Configuración](../settings.md#advanced-search) para administrar la búsqueda semántica y, opcionalmente, ajuste los controles avanzados en la ficha **[!UICONTROL Advanced search]**.

## Ventajas

- **Menos páginas de búsqueda vacías**: los compradores encuentran productos cuando su redacción no coincide exactamente con el texto del catálogo.
- **Mejor coincidencia de intención**: las consultas naturales y descriptivas devuelven resultados útiles.
- **Mantenimiento de sinónimos menos**: las variaciones de palabras comunes (por ejemplo, sofá y sofá) suelen manejarse sin listas de sinónimos manuales.
- **No hay tienda ni trabajo de desarrollador**: la búsqueda semántica está habilitada de manera predeterminada y no requiere ningún cambio de código de tema, lista desplegable o API.

## Cómo funciona

Cuando la búsqueda semántica está habilitada, [!DNL Adobe Commerce Optimizer] usa atributos de catálogo predefinidos elegidos por el sistema (como el nombre y la descripción del producto) para interpretar el significado de la consulta junto con la búsqueda de palabras clave tradicional. No selecciona ni prioriza atributos en el Administrador.

Por ejemplo:

- Una búsqueda de &quot;sofá de cuero&quot; puede devolver productos etiquetados como &quot;sofá de cuero&quot;.
- &quot;Vestido de primavera&quot; puede salir a la superficie vestidos de temporada incluso cuando &quot;primavera&quot; no está en el nombre del producto.
- &quot;Zapatos para trail running&quot; puede hacer juego con productos descritos como calzado fuera de carretera o de senderismo.

## Qué sucede cuando se habilita la búsqueda semántica

La búsqueda semántica funciona junto con la configuración de búsqueda [!DNL Adobe Commerce Optimizer] existente. No reemplaces la búsqueda de palabras clave ni reconfigures la tienda.

Cuando la búsqueda semántica está activa:

- Se siguen aplicando las [reglas de comercialización](../merchandising/rules/overview.md), los [sinónimos](../merchandising/synonyms/overview.md), las [facetas](../merchandising/facets/overview.md), los amplificadores y los filtros existentes.
- La búsqueda semántica agrega una comprensión basada en IA de la intención del comprador para mejorar la relevancia de los resultados junto con la coincidencia de palabras clave.
- Los atributos de catálogo predefinidos se indexan automáticamente. No seleccione atributos ni publique una configuración independiente.

## Administrar la búsqueda semántica en el administrador

La búsqueda semántica está **habilitada de manera predeterminada** para los catálogos en inglés aptos. Vaya a **[!UICONTROL Settings]** > **[!UICONTROL Advanced search]** para confirmar la configuración o cambiarla:

1. En el Administrador, vaya a **[!UICONTROL Settings]**.
1. En la ficha **[!UICONTROL Advanced search]**, revise **[!UICONTROL Enable semantic search]**.

   Cuando está habilitada, la búsqueda coincide con los productos en función del significado y el contexto, lo que puede producir resultados más relevantes, menos páginas de búsqueda vacías y una conversión mejorada.

1. Haga clic en **[!UICONTROL Save]** si cambia los controles de alternancia o ajuste.

   Los resultados de la búsqueda se actualizan una vez completada la indexación. Para un catálogo de tamaño medio, la indexación puede tardar hasta media hora. Para catálogos grandes con millones de productos, puede tomar unas pocas horas.

>[!NOTE]
>
> La búsqueda semántica solo está disponible para los catálogos **English**. Si cambia **[!UICONTROL Language]** a un catálogo que no está en inglés, **[!UICONTROL Enable semantic search]** se deshabilita automáticamente.

No es necesario publicar una configuración independiente ni cambiar la configuración de la tienda después de guardar.

## Validar después de la activación

Una vez que la búsqueda semántica esté activa y la indexación se complete, Adobe recomienda validar el rendimiento de la búsqueda. Utilice la página [Rendimiento de la búsqueda](../manage-results/search-performance.md) para revisar las métricas y las consultas de prueba que importan a su negocio.

1. Revise los términos más buscados en el informe **Búsquedas únicas**.
1. Probar consultas históricas de resultados cero a partir del informe **Resultados cero** en la tienda.
1. Compare los resultados de búsqueda para las mismas consultas antes y después de la activación.
1. Monitorice las métricas de conversión y participación de búsqueda, incluida la tasa de pulsaciones, la tasa de conversión y la tasa de resultados cero.

## Ajuste opcional

En la ficha **[!UICONTROL Advanced search]**, puede ajustar el comportamiento de la búsqueda una vez habilitada la búsqueda semántica:

- **[!UICONTROL Semantic boost]**: aumente o disminuya la influencia de las coincidencias basadas en significados en la clasificación. Por ejemplo, supongamos que una coincidencia de producto recuperada a través de una búsqueda semántica se muestra al final del resultado. Añadir un impulso lo mueve hacia arriba en el resultado.
- **[!UICONTROL Similarity threshold]**: establezca lo cerca que debe estar una coincidencia antes de que aparezca un producto. Los valores más bajos muestran más resultados; los valores más altos muestran menos coincidencias y más ajustadas.
- **[!UICONTROL Fuzzy search]** y **[!UICONTROL Fuzzy search similarity threshold]**: ayuda a los compradores a encontrar productos cuando las consultas incluyen pequeñas diferencias ortográficas.

Consulte [Búsqueda avanzada](../settings.md#advanced-search) para obtener descripciones de los controles e instrucciones paso a paso.

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
