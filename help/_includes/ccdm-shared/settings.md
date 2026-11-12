---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%
---
Use el área de trabajo *Configuración* para configurar la búsqueda y la detección de productos en su tienda. Las pestañas disponibles son las siguientes:

- **Facetas**: configure los grupos de intervalos de precios y los intervalos utilizados como filtros de búsqueda.
- **Idioma**: establezca el idioma del catálogo utilizado para la indexación y la búsqueda.
- **Búsqueda avanzada**: habilita la búsqueda semántica y la búsqueda difusa y ajusta los umbrales de similitud y de aumento semántico.

## Acceso al espacio de trabajo Configuración

La forma de abrir el área de trabajo *Settings* depende del producto que use:

- **Administrador De Adobe Commerce** (Adobe Commerce as a Cloud Service)—Seleccione *Comercialización* > **Configuración De Comercialización**.
- **Adobe Commerce Optimizer Studio**—Seleccione *Comercialización* > **Configuración**.

>[!BEGINTABS]

>[!TAB Facetas de precio]

## Facetas de precio {#price-facets}

Puede especificar el número de grupos de intervalos de precios y cómo se distribuyen los valores de precios entre ellos. Cada rango de precios se superpone con el grupo anterior por uno. Por ejemplo, cinco grupos con un intervalo de 20 crean intervalos de precios: 0-20, 20-40, 40-60, 60-80 y >80. Si no hay suficientes productos en el catálogo para rellenar todos los intervalos definidos, la visualización de los grupos disponibles se ajusta en consecuencia. Por ejemplo: 0-20, 60-80, >80.

**Para configurar las facetas de precios:**

1. En el área de trabajo **Configuración**, seleccione **[!UICONTROL Facets]**.
1. En la sección **Faceta de precio**, haga lo siguiente:
   - Escriba **[!UICONTROL Number of selections]** o las agrupaciones de precios para que estén disponibles. Se pueden definir hasta 100 agrupaciones de precios.
   - Escriba **[!UICONTROL Interval value]** o el rango de precios de cada grupo. El valor máximo es 40 000 000.
1. Haga clic en **[!UICONTROL Save]**.

   La configuración actualizada tarda unos 15 minutos en estar disponible en la tienda.

### Descripciones de los campos de faceta de precio

| Campo | Descripción |
| --- | --- |
| Número de selecciones | Especifica el número de agrupaciones de intervalos de precios que se pueden usar como filtros de búsqueda en la tienda. Valor predeterminado: 8, Valor máximo: 100 |
| Valor de intervalo | Especifica el intervalo de rango de precios para cada grupo. Por ejemplo, cinco selecciones con un valor de intervalo de 20 generan agrupaciones de 0-20, 20-40, 40-60, 60-80 y >80. Valor predeterminado: 5, Valor máximo: 40 000 000 |

>[!TAB Idioma]

## Idioma {#language}

La configuración Idioma indica al sistema qué idioma esperar al leer el catálogo y escribir el índice.

Los idiomas tienen diferentes conjuntos de reglas gramaticales: cómo se separan las palabras, tiempos verbales y formas de palabras, por ejemplo.
La configuración Idioma garantiza que se aplique el conjunto correcto de reglas al mecanismo de indexación.

Establezca la configuración Idioma en el idioma principal del catálogo. Cambiar el idioma del índice tarda de 5 a 60 minutos en aparecer en la tienda, según el tamaño y la complejidad del catálogo.

| Idioma | Código |
|----|----|
| Árabe | ar |
| Armenio | hy |
| Vasco | eu |
| Bengalí | bn |
| brasileño | pt-br |
| Búlgaro | bg |
| Catalán | ca |
| Chino (simplificado) | zh-cn |
| Chino (tradicional) | zh-tw |
| Checo | cs |
| Danés | da |
| Neerlandés | nl |
| Inglés | en |
| Estonio | et |
| Finés | fi |
| francés | fr |
| Gallego | gl |
| Alemán | de |
| Griego | el |
| Hindi | hola |
| Húngaro | hu |
| Indonesio | id |
| Irlandés | ga |
| Italiano | it |
| Japonés (Katakana) | ja |
| Coreano | ko |
| Letón | lv |
| Lituano | lt |
| Noruego | no |
| persa | fa |
| Portugués | pt |
| Rumano | ro |
| Ruso | ru |
| Sorani | ku |
| Español | es |
| Sueco | sv |
| Turco | tr |
| Tailandés | th |

>[!TAB Búsqueda avanzada]

## Búsqueda avanzada {#advanced-search}

Utilice la ficha **[!UICONTROL Advanced search]** para administrar la búsqueda en un solo lugar. El sistema ofrece una experiencia de búsqueda unificada en la tienda; no configura la búsqueda de palabras clave y la búsqueda semántica por separado para los compradores. **[!UICONTROL Enable semantic search]** está **habilitado de forma predeterminada** para los catálogos en inglés aptos. La búsqueda semántica funciona junto con la configuración existente; se siguen aplicando [reglas de comercialización](./merchandising/rules/overview.md), [sinónimos](./merchandising/synonyms/overview.md), [facetas](./merchandising/facets/overview.md), amplificaciones y filtros. El sistema utiliza automáticamente atributos de catálogo predefinidos; no selecciona ni prioriza atributos en Configuración. No se requieren cambios de tienda o desarrollador.

![Configuración de búsqueda avanzada](/help/assets/ccdm-shared/advanced-search.png)

**Para administrar la búsqueda semántica:**

1. En el área de trabajo **Configuración**, seleccione la ficha **[!UICONTROL Advanced search]**.
1. En **[!UICONTROL Enable semantic search]**, confirme que la búsqueda semántica está habilitada o desactívela si no desea que haya coincidencias semánticas.
1. Haga clic en **[!UICONTROL Save]** si cambia los controles de alternancia o ajuste.

   Los resultados de la búsqueda se actualizan una vez completada la indexación. Para un catálogo de tamaño medio, la indexación puede tardar hasta 30 minutos. Para catálogos grandes con millones de productos, puede tomar unas pocas horas.

### Ajuste opcional

Una vez habilitada la búsqueda semántica, puede ajustar lo siguiente en la misma pestaña:

- **[!UICONTROL Semantic boost]**: para priorizar los resultados semánticamente relevantes en la clasificación, aplique un impulso. Aumente el valor cuando las coincidencias semánticas deban tener un mayor peso en el conjunto de resultados; bájelo cuando los resultados sean demasiado amplios.
- **[!UICONTROL Similarity threshold]**: establezca la puntuación de similitud mínima (como porcentaje) para una coincidencia semántica. Los valores más bajos devuelven más resultados (mayor recuperación), pero pueden incluir coincidencias más débiles. Los valores más altos devuelven menos coincidencias y más ajustadas (mayor precisión).
- **[!UICONTROL Fuzzy search]**: para buscar coincidencias cercanas para las consultas de búsqueda y corregir errores tipográficos y variaciones menores, active **2&rbrace;.**
- **[!UICONTROL Fuzzy search similarity threshold]**: establezca la similitud mínima (como porcentaje) necesaria para que aparezcan las coincidencias aproximadas. Los umbrales más bajos devuelven coincidencias más aproximadas; eleve el umbral si los resultados difusos parecen demasiado amplios.

>[!NOTE]
>
> La búsqueda semántica solo es compatible con los catálogos **English**. Si se selecciona otro idioma en la ficha **[!UICONTROL Language]**, se deshabilita **[!UICONTROL Enable semantic search]**.

Para obtener beneficios, instrucciones de validación, prácticas recomendadas, solución de problemas y limitaciones, vea [Búsqueda semántica](/help/optimizer/setup/semantic-search.md).

### Descripciones de campos de búsqueda avanzada

| Control | Descripción |
| --- | --- |
| Habilitar la búsqueda semántica | Cuando está habilitada, la búsqueda utiliza el significado y el contexto junto con la coincidencia de palabras clave. Los atributos de catálogo predefinidos se utilizan automáticamente; no se requiere ninguna configuración de atributos en Configuración. Habilitado de forma predeterminada. |
| Aumento semántico | Aumento aplicado para priorizar los resultados semánticamente relevantes en la clasificación. |
| Umbral de similitud | Puntuación de similitud mínima (porcentaje) para una coincidencia semántica. Los valores más bajos favorecen la recuperación; los valores más altos favorecen la precisión. |
| Búsqueda aproximada | Si se selecciona **en**, la búsqueda buscará coincidencias cercanas para las consultas (por ejemplo, variaciones menores). |
| Umbral de similitud de búsqueda aproximada | Las coincidencias aproximadas de similitud mínima (porcentaje) deben cumplirse para que aparezcan en los resultados. |

>[!ENDTABS]
