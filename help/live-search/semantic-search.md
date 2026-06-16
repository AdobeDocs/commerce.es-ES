---
title: Búsqueda semántica
description: Habilite la búsqueda semántica de IA para  [!DNL Live Search]  desde Configuración. No se requiere configuración de atributos ni cambios de tienda.
role: Admin
recommendations: noCatalog
source-git-commit: e631346aa13737ded2c14daecbb91457e15417eb
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# Búsqueda semántica

La búsqueda semántica utiliza IA para comprender qué significan los compradores, no solo las palabras exactas que escriben. Consultas como &quot;vestido para una boda en la playa&quot; o &quot;zapatos cómodos para estar de pie todo el día&quot; pueden devolver productos relevantes incluso cuando su catálogo no utiliza esas frases exactas.

[!DNL Live Search] combina la coincidencia semántica y de palabras clave en una experiencia de búsqueda. No se administran modos semánticos y de palabra clave independientes en la tienda. [!DNL Live Search] no ofrece controles semánticos avanzados (por ejemplo, reguladores de ampliación o de similitud) en el administrador. Puede habilitar o deshabilitar la búsqueda semántica.

## Habilitación por implementación

La búsqueda semántica se administra desde el área de trabajo **Settings** del administrador de [!DNL Live Search] (**Marketing** > *SEO y búsqueda* > **[!DNL Live Search]**). [!DNL Adobe Commerce as a Cloud Service] utiliza esta misma interfaz [!DNL Live Search] que los comerciantes de PaaS.

## Ventajas

- **Menos búsquedas de resultados cero**: los compradores encuentran productos cuando su redacción no coincide exactamente con el texto del catálogo.
- **Resultados más relevantes**: las consultas naturales y descriptivas devuelven coincidencias útiles basadas en el significado y el contexto.
- **Mantenimiento de sinónimos menos**: las variaciones de palabras comunes (por ejemplo, sofá y sofá) suelen manejarse sin listas de sinónimos manuales.
- **Sin trabajo de desarrollador o tienda** — La búsqueda semántica no requiere cambios en el código de tema, widget o API. Los comerciantes de PaaS lo habilitan en Configuración; los clientes de [!DNL Adobe Commerce as a Cloud Service] lo reciben habilitado de manera predeterminada.

## Cómo funciona

Cuando la búsqueda semántica está habilitada, [!DNL Live Search] usa atributos de catálogo predefinidos elegidos por el sistema (como el nombre y la descripción del producto) para interpretar el significado de la consulta junto con la búsqueda de palabras clave tradicional. No selecciona ni prioriza atributos en el Administrador.

Por ejemplo:

- Una búsqueda de &quot;sofá de cuero&quot; puede devolver productos etiquetados como &quot;sofá de cuero&quot;.
- &quot;Vestido de primavera&quot; puede salir a la superficie vestidos de temporada incluso cuando &quot;primavera&quot; no está en el nombre del producto.
- &quot;Zapatos para trail running&quot; puede hacer juego con productos descritos como calzado fuera de carretera o de senderismo.

## Qué sucede cuando se habilita la búsqueda semántica

La búsqueda semántica funciona junto con la configuración de [!DNL Live Search] existente. No reemplaces la búsqueda de palabras clave ni reconfigures la tienda.

Cuando la búsqueda semántica está activa:

- Se siguen aplicando las configuraciones de [reglas de búsqueda](rules.md), [sinónimos](synonyms.md), [facetas](facets.md), amplificaciones y [comercialización de categorías](category-merch.md).
- La búsqueda semántica agrega una comprensión basada en IA de la intención del comprador para mejorar la relevancia de los resultados junto con la coincidencia de palabras clave.
- Los atributos de catálogo predefinidos se indexan automáticamente. No seleccione atributos ni publique una configuración independiente.

## Administrar la búsqueda semántica en el administrador

Vaya al área de trabajo [Configuración](settings.md#semantic-search) para ver o cambiar la opción **[!UICONTROL Semantic search]**.

>[!NOTE]
>
> La búsqueda semántica solo está disponible para los catálogos **English**. Si cambia **Idioma** a un catálogo que no esté en inglés en el área de trabajo **Configuración**, **[!UICONTROL Semantic search]** se deshabilita automáticamente.

### Para comerciantes de PaaS

Los comerciantes locales y de Adobe Commerce en la nube deben habilitar manualmente la búsqueda semántica:

1. En el Administrador, vaya a **Marketing** > *SEO y búsqueda* > **[!DNL Live Search]**.
1. En el área de trabajo **Configuración**, habilite **[!UICONTROL Semantic search]**.

   Cuando está habilitada, la búsqueda coincide con los productos en función del significado y el contexto, lo que puede producir resultados más relevantes, menos búsquedas de resultados cero y una conversión mejorada.

1. Haga clic en **[!UICONTROL Save]**.

   Los resultados de la búsqueda se actualizan una vez completada la indexación. Para un catálogo de tamaño medio, la indexación puede tardar hasta media hora. Para catálogos grandes con millones de productos, puede tomar unas pocas horas.

### Para [!DNL Adobe Commerce as a Cloud Service] clientes

[!DNL Adobe Commerce as a Cloud Service] clientes usan el mismo espacio de trabajo de **Configuración** en el administrador de [!DNL Live Search]. La búsqueda semántica está **habilitada de manera predeterminada** para los catálogos en inglés aptos. Confirme que **[!UICONTROL Semantic search]** está habilitado o desactívelo si no desea que haya coincidencia semántica en la tienda.

No necesita una configuración de tienda o paso de publicación independiente después de guardar un cambio.

## Validar después de la activación

Una vez que la búsqueda semántica esté activa y la indexación se complete, Adobe recomienda validar el rendimiento de la búsqueda. Use el área de trabajo de [Rendimiento](performance.md) para revisar las métricas y las consultas de prueba que importan a su negocio. Esto se aplica si la búsqueda semántica estaba habilitada de forma predeterminada o si la habilitó manualmente.

1. Revise los términos más buscados en el informe **Búsquedas únicas**.
1. Probar consultas históricas de resultados cero a partir del informe **Resultados cero** en la tienda.
1. Compare los resultados de búsqueda para las mismas consultas antes y después de la activación.
1. Monitorice las métricas de conversión y participación de búsqueda, incluida la tasa de pulsaciones, la tasa de conversión y la tasa de resultados cero.

## Prácticas recomendadas

- Utilice nombres y descripciones de productos claros y descriptivos (idealmente 50-100 palabras) para que tanto la palabra clave como la coincidencia semántica tengan texto de catálogo sólido con el que trabajar.
- Use [sinónimos](synonyms.md) específicos de la marca o muy técnicos donde la búsqueda semántica pueda no cubrir términos especializados.

## Resolución de problemas

| Problema | Qué hacer |
| --- | --- |
| No hay cambios en la tienda justo después de guardar | Espere a que termine la indexación. Los catálogos grandes pueden tardar más. |
| La búsqueda semántica no está disponible o se desactiva automáticamente | Confirmar **idioma** en el área de trabajo de **Configuración** está establecido en **Inglés**. |
| Los resultados aún omiten términos comunes | Agregue [sinónimos](synonyms.md) para los términos de marca o del sector; la búsqueda semántica puede no resolverse. |

## Limitaciones {#semantic-search-limitations}

- **Idioma del catálogo:** La búsqueda semántica solo está disponible para los catálogos en **inglés**.
- **Controles de administración:** [!DNL Live Search] proporciona un control de habilitar/deshabilitar solamente. No puede ajustar el impulso semántico, el umbral de similitud ni la búsqueda aproximada desde el espacio de trabajo **Settings**.

## Más ayuda sobre este tema

- [Configuración](settings.md#semantic-search)
- [Sinónimos](synonyms.md)
- [Rendimiento](performance.md)
