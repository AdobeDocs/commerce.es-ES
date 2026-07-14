---
title: Configuración
description: Configure la búsqueda semántica, los intervalos de facetas de precios y el idioma de indización predeterminado para el servicio  [!DNL Live Search] s.
exl-id: 6387a365-7e23-4023-95ac-27908164d81c
TQID: https://experienceleague.adobe.com/Dn4x8Boo-1F5RQgMXVx6Dpt7iYWFIlqOlO5QwhJrjVU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 1f5246b6f5853f8b53a356ae2d6d58077b07a9a5
workflow-type: tm+mt
source-wordcount: 679
ht-degree: 0%

---

# Configuración

Use el área de trabajo **Configuración** para configurar la búsqueda semántica, los intervalos y rangos de facetas de precios y el idioma predeterminado del índice.

![Configuración](assets/settings.png)

## Búsqueda semántica {#semantic-search}

>[!AVAILABILITY]
>
>La búsqueda semántica está disponible para los comerciantes que utilizan las versiones 2.4.4 y posteriores de Adobe Commerce.

La búsqueda semántica utiliza IA para hacer coincidir productos en función del significado y el contexto, no solo palabras clave exactas. Si se habilita **[!UICONTROL Semantic search]**, los compradores que usen lenguaje natural o palabras que no coincidan literalmente con el catálogo podrán encontrar productos relevantes. [!DNL Live Search] ofrece coincidencias semánticas y de palabras clave en una experiencia de búsqueda unificada en la tienda. La búsqueda semántica funciona junto con la configuración existente; [reglas de búsqueda](rules.md), [sinónimos](synonyms.md), [facetas](facets.md), amplificaciones y [comercialización de categorías](category-merch.md) siguen aplicándose.

**Para habilitar la búsqueda semántica (solo PaaS):**

1. En el Administrador, vaya a **Marketing** > *SEO y búsqueda* > **[!DNL Live Search]**.
1. En el área de trabajo **Configuración**, habilite **[!UICONTROL Semantic search]**.

   Cuando está habilitada, la búsqueda coincide con los productos en función del significado y el contexto, lo que da como resultado resultados más relevantes, menos búsquedas de resultados cero y una conversión mejorada.

1. Haga clic en **[!UICONTROL Save]**.

   Los resultados de la búsqueda se actualizan una vez completada la indexación. Para un catálogo de tamaño medio, la indexación puede tardar hasta media hora. Para catálogos grandes con millones de productos, puede tomar unas pocas horas.

>[!NOTE]
>
> La búsqueda semántica solo está disponible para los catálogos **English**. Si establece **Idioma** en un catálogo que no sea inglés (consulte [Idioma](#language)), **[!UICONTROL Semantic search]** se deshabilita automáticamente.

Para obtener beneficios, instrucciones de validación, prácticas recomendadas, solución de problemas y limitaciones, vea [Búsqueda semántica](semantic-search.md).

### Descripciones de campos

| Campo | Descripción |
| --- | --- |
| Búsqueda semántica | Cuando está habilitado, [!DNL Live Search] usa significado y contexto junto con la coincidencia de palabras clave. Los atributos de catálogo predefinidos se utilizan automáticamente; no se requiere ninguna configuración de atributos en el administrador. Habilitado de forma predeterminada para [!DNL Adobe Commerce as a Cloud Service]; los comerciantes de PaaS lo habilitan manualmente. |

## Facetado de precios {#price-faceting}

Puede especificar el número de grupos de intervalos de precios y cómo se distribuyen los valores de precios entre ellos. Cada rango de precios se superpone con el grupo anterior por uno. Por ejemplo, cinco grupos con un intervalo de 20 crean los siguientes intervalos de precios: 0-20, 20-40, 40-60, 60-80 y >80. Si no hay suficientes productos en el catálogo para rellenar todos los intervalos definidos, la visualización de los grupos disponibles se ajusta en consecuencia. Por ejemplo: 0-20, 60-80, >80.

**Para configurar facetas de precios:**

1. En el Administrador, vaya a **Marketing** > *SEO y búsqueda* > **[!DNL Live Search]**.
1. En el área de trabajo **Configuración** en *Faceteo de precios*, haga lo siguiente:
   * Escriba el **número de selecciones** o las agrupaciones de precios que estarán disponibles. Con [!DNL Live Search] 4.4.0, puede definir hasta 100 agrupaciones de precios. Las versiones anteriores permitían 50 agrupaciones de precios.
   * Escriba el **valor de intervalo** o el rango de precios de cada grupo. El valor máximo es 40 000 000.
1. Haga clic en **[!UICONTROL Save]**.

   La configuración actualizada tarda unos 15 minutos en estar disponible en la tienda.

### Descripciones de campos

| Campo | Descripción |
|--- |--- |
| Número de selecciones | Especifica el número de agrupaciones de intervalos de precios que se pueden usar como filtros de búsqueda en la tienda. Valor predeterminado: 8, Valor máximo: 100 (a partir de [!DNL Live Search] 4.4.0) |
| Valor de intervalo | Especifica el intervalo de rango de precios para cada grupo. Por ejemplo, cinco selecciones con un valor de intervalo de 20 crean cinco agrupaciones de 0-20, 20-40, 40-60, 60-80 y >80. Valor predeterminado: 5, Valor máximo: 40 000 000 |

## Idioma {#language}

La configuración de idioma indica a [!DNL Live Search] qué idioma esperar al leer el catálogo y escribir el índice.

Los idiomas tienen diferentes conjuntos de reglas gramaticales: cómo se separan las palabras, tiempos verbales y formas de palabras, por ejemplo.La configuración Idioma garantiza que se aplique el conjunto correcto de reglas al mecanismo de indexación.

Establezca la configuración Idioma en el idioma principal del catálogo. Al cambiar el idioma del índice, puede tardar entre 5 y 60 minutos en reflejar el cambio en la tienda, según el tamaño y la complejidad del catálogo.

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
