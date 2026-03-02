---
title: Prácticas recomendadas de [!DNL Live Search]
description: Conozca las prácticas recomendadas para implementar  [!DNL Live Search] en su tienda.
role: Admin, Developer
exl-id: f7700339-fb13-42fe-a249-17cd4ba36e1b
source-git-commit: c3d431a6536c3c5528b9aee45f03b0b94b4ea64e
workflow-type: tm+mt
source-wordcount: '2892'
ht-degree: 0%

---

# Prácticas recomendadas

Este artículo ayuda a los comerciantes a mejorar la funcionalidad de búsqueda del sitio, lo que garantiza una experiencia de comprador sencilla y eficaz que maximiza las tasas de conversión. Al seguir las estrategias descritas, aprenderá a implementar características de búsqueda avanzada y a refinar continuamente su herramienta de búsqueda para obtener un rendimiento óptimo con Adobe Commerce [!DNL Live Search].

Existen varios factores clave que determinan la relevancia y eficacia de los resultados de búsqueda:

- Los datos de productos bien estructurados garantizan que los algoritmos de búsqueda puedan hacer coincidir de forma eficaz los productos con las consultas. Los datos de productos de baja calidad conducen a resultados de búsqueda poco relevantes. Para afectar directamente al éxito de su estrategia de comercialización:
   - Configure los atributos correctos según se pueda buscar con su peso correspondiente.
   - Asegúrese de que los datos de esos atributos sean relevantes.
- Una experiencia de búsqueda bien diseñada crea confianza con los clientes e infunde confianza en que pueden encontrar lo que necesitan.
- Las reglas de búsqueda son esenciales, ya que pueden aumentar la visibilidad de ciertos productos en función de la popularidad, las nuevas llegadas, los criterios promocionales o cualquier otra estrategia de comercialización para satisfacer los requisitos comerciales.
- La navegación con facetas permite a los compradores refinar su búsqueda y obtener resultados relevantes rápidamente.

Para administrar [!DNL Live Search], ve a **Marketing** > *SEO y búsqueda* > **[!DNL Live Search]** en el administrador de Adobe [!DNL Commerce]. 

## Optimización de la funcionalidad de búsqueda

En esta sección, aprenderá a optimizar la funcionalidad de búsqueda mediante funciones como autocompletar para proporcionar sugerencias en tiempo real como tipo de comprador, sinónimos y ortografía para garantizar que los compradores encuentren productos incluso si utilizan palabras diferentes y facetas que permitan a los compradores reducir los resultados de búsqueda.

### Autocompletar

Autocompletar, también conocido como escritura anticipada o autosugerir, es una función de búsqueda interactiva que muestra dinámicamente sugerencias a los compradores cuando introducen sus términos de búsqueda. Esto ayuda a los compradores a encontrar productos de forma rápida y sencilla, ya que ofrece sugerencias en tiempo real en función de sus comentarios.

El widget [!DNL Live Search] [[!DNL popover]](storefront-popover.md) habilita las opciones de búsqueda de autocompletar para sugerir productos populares. Con cada carácter escrito por el comprador, la ventana emergente se actualiza con productos sugeridos e imágenes en miniatura de los principales resultados de búsqueda.

[!DNL Live Search] comienza a devolver resultados cuando el usuario ha escrito dos caracteres. Para una coincidencia parcial, el número máximo de caracteres por palabra es 20. El número de caracteres de una consulta &quot;buscar mientras escribe&quot; no se puede configurar.

Más información sobre el widget [ventana emergente](storefront-popover.md).

### Sinónimos y errores ortográficos

Live Search administra los errores ortográficos de forma predeterminada. Puede configurar sinónimos para incluir palabras que los compradores pueden utilizar y que difieren de las palabras especificadas en el catálogo. Usted no quiere perder una venta porque alguien está buscando un &quot;sofá&quot;, mientras que su producto aparece como un &quot;sofá&quot;. Puede capturar una amplia gama de términos de búsqueda introduciendo todas las palabras posibles que los clientes podrían utilizar para encontrar sus productos. Puede [establecer sinónimos de una o dos maneras](synonyms-add.md#step-2-define-the-synonym-by-type) para mejorar los resultados.

#### Sugerencias para optimizar los sinónimos

- Asigne nombres de marcas y abreviaturas a sus nombres completos, como &quot;HP&quot; a &quot;Hewlett-Packard&quot; y apodos de productos comunes, como &quot;iPhone&quot; a &quot;Apple iPhone&quot;.
- Incluya jerga y términos específicos del sector que los compradores puedan utilizar indistintamente, como &quot;zapatillas de deporte&quot; y &quot;zapatillas de running&quot;.
- Actualice con regularidad la lista de sinónimos en función de las nuevas tendencias de búsqueda, las adiciones de productos y el comportamiento del comprador.
- Pruebe la eficacia de las asignaciones de sinónimos analizando los resultados de búsqueda y los comentarios del comprador. Refine las asignaciones para mejorar la precisión y la relevancia.

Más información sobre los sinónimos:

- [Tipos de sinónimos](synonyms-type.md)
- [Crear sinónimos](synonyms-add.md)
- [Administrar sinónimos](synonyms-manage.md)
- [Compatibilidad de idiomas](settings.md#language)

### Facetas

La funcionalidad de filtro y faceta es un componente crítico del sitio [!DNL Commerce], diseñado para mejorar la experiencia del comprador, ya que permite que los compradores reduzcan los resultados de búsqueda y encuentren los productos de manera más eficiente. Esta funcionalidad ayuda a los compradores a revisar vastos catálogos de artículos mediante la aplicación de criterios específicos, lo que hace que el proceso de compra sea más rápido, fácil y satisfactorio. Al implementar filtros y facetas eficaces y fáciles de usar para los compradores, puede ayudar a los clientes a encontrar exactamente lo que necesitan de forma rápida y eficaz, lo que a la larga aumenta la satisfacción y las tasas de conversión.

Para configurar un atributo de producto como faceta, debe tener las siguientes [propiedades establecidas](facets-add.md#step-1-add-a-facet):

- **[!UICONTROL Use in Search]** -  `Yes`
- **[!UICONTROL Use in Layered Navigation]** -  `Filterable (with results)`
- **[!UICONTROL Use in Search Results Layered Navigation]** -  `Yes`

#### Sugerencias para optimizar las facetas

- Determine los atributos más relevantes y útiles para sus productos, tales como título, categoría, marca, rango de precios, color y tamaño, y configúrelos como [facetas dinámicas](facets-type.md). 
- Establezca y ordene atributos de producto que sean coherentes en todo el catálogo y altamente relevantes para sus productos a fin de mejorar la relevancia y las capacidades de filtrado para sus compradores.
- Asegúrese de que las etiquetas de faceta sean fáciles de entender y de que tengan nombres coherentes en todo el sitio. Por ejemplo, utilice &quot;Intervalo de precios&quot; en lugar de &quot;Costo&quot;.
- Evite abrumar a los compradores limitando el número de facetas a las más importantes. Demasiadas opciones pueden causar fatiga de decisión. De manera predeterminada, [!DNL Live Search] está limitado a un máximo de 100 atributos configurados como facetas y 30 contenedores devueltos dentro de cada faceta. Más información sobre [limitaciones de facetas](boundaries-limits.md#facets). 
- Permite que los compradores seleccionen varios criterios de filtro simultáneamente para restringir los resultados. Por ejemplo, permitir que los compradores seleccionen los colores &quot;Rojo&quot; y &quot;Azul&quot;.
- Muestre el número de productos disponibles junto a cada opción de faceta para que los compradores tengan una idea de los resultados de búsqueda que pueden esperar.
- Implemente secciones de facetas contraíbles para mantener la interfaz limpia y manejable, especialmente en dispositivos móviles.
- Permite que los compradores restablezcan fácilmente facetas individuales o todos los filtros seleccionados para iniciar una nueva búsqueda.

Más información sobre las facetas:

- [Tipos de facetas](facets-type.md)
- [Añadir facetas](facets-add.md)
- [Administrar facetas](facets-manage.md) (editar, fijar una faceta, eliminar, publicar)
- [Facetado de precios](settings.md#price-faceting)

## Mejorar la relevancia de los resultados de búsqueda

En esta sección se explica cómo mejorar la relevancia de los resultados de búsqueda mediante la implementación de reglas de búsqueda eficaces y el uso de metadatos de productos para garantizar que se puedan buscar atributos precisos y detallados.

### Imágenes

Asegúrese de que los productos secundarios de los productos configurables tengan imágenes con las funciones correctas. Si tiene productos principales o secundarios, el resultado de la búsqueda podría no tener imágenes.

>[!NOTE]
>
>Las imágenes de los resultados de búsqueda pueden variar según el término de búsqueda. Si el término de búsqueda determina que un producto secundario es más relevante, se utilizarán imágenes del producto secundario en lugar de imágenes del producto principal.

### Buscar reglas

Para optimizar la tasa de conversión y los ingresos, debe implementar reglas de búsqueda efectivas. Ajuste las clasificaciones de productos en función de los datos de ventas, los niveles de existencias y las promociones con [Buscar comercialización](rules.md).

Es crucial establecer una regla de búsqueda predeterminada bien pensada. La [regla predeterminada](rules.md#default-rule) determina cómo se ordenan y muestran inicialmente los resultados de búsqueda a los compradores, lo que mejora su experiencia general y aumenta la probabilidad de compra. La supervisión y el ajuste regulares de esta regla garantizan que siga satisfaciendo las necesidades de los compradores y los objetivos comerciales de forma eficaz.

#### Sugerencias para optimizar las reglas de búsqueda

- Fije o aumente productos con altos volúmenes de ventas o actividad de ventas reciente.
- Priorice los productos con altas calificaciones y críticas positivas.
- Asegúrese de que los artículos en stock tengan una clasificación más alta.
- Priorice ligeramente los productos con márgenes de beneficio más altos sin poner en riesgo la relevancia.
- Resaltar productos que están a la venta o que forman parte de promociones especiales.
- Defina automáticamente reglas de búsqueda durante los periodos de promoción o ventas utilizando el intervalo de fechas durante el periodo de promoción.
- Utilice siempre el panel &quot;Probar la regla&quot; para obtener una vista previa de cómo la estrategia de clasificación inteligente afecta a los resultados de búsqueda reales de diferentes consultas.
- Adapte los resultados de búsqueda según el comportamiento de cada comprador mediante [clasificación inteligente](rules-add.md#intelligent-ranking), como &quot;recomendado para usted&quot;, &quot;más visitados&quot;, etc. Para adaptar el comportamiento del comprador, debe asegurarse de que el evento se implementa correctamente. Para los comerciantes de Luma, los eventos están disponibles de forma predeterminada. Para implementaciones sin encabezado o personalizadas, debe [implementar eventos](https://developer.adobe.com/commerce/services/shared-services/storefront-events/) según sus necesidades específicas.

Más información sobre las reglas de búsqueda:

- [Merchandising Workspace](rules-workspace.md#set-the-scope)
- [Requisitos](rules.md#requirements)
- [Regla de búsqueda predeterminada](rules.md#default-rule)
- Administrar reglas de búsqueda
   - [Crear](rules-add.md)
   - [Editar, ver y eliminar](rules-manage.md)
- Recopilación de datos
   - [[!DNL Live Search] eventos](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search)
   - [Recopilador de eventos de Adobe Commerce](https://developer.adobe.com/commerce/services/shared-services/storefront-events/reference/event-framework/)
   - [Eventos de Commerce en GitHub](https://github.com/adobe/commerce-events/tree/main/examples) 

### Aprovechamiento de metadatos de productos

Asegúrese de que los atributos de producto precisos y detallados estén [configurados para realizar búsquedas](workspace.md#set-attributes-as-searchable). Tenga en cuenta que los atributos SKU, nombre y categoría se pueden buscar de forma predeterminada y no se pueden excluir de la búsqueda. Para obtener los mejores resultados, no utilice espacios en los SKU.

Elegir qué atributos permiten búsquedas tiene un gran impacto en la calidad de la búsqueda. Si se pueden buscar demasiados atributos, la relevancia puede reducirse y provocar coincidencias inesperadas, incluso si aumenta el número de resultados devueltos. En esta sección se explica cómo seleccionar atributos en los que se pueden realizar búsquedas deliberadamente para equilibrar la cobertura y la relevancia.

**Atributos en los que se puede buscar recomendados:**

- **Nombre del producto** - Intento alto, describe directamente el producto.
- **Descripción principal** - Detalles concisos del producto que los compradores esperan encontrar.
- **Marca**: los compradores buscan con frecuencia por marca.
- **Número/estilo de modelo**: identificadores específicos con intención clara.
- **Características principales** - Características distintivas importantes (por ejemplo, &quot;impermeable&quot;, &quot;inalámbrico&quot;).
- **Material/Tela** - Para las categorías de moda y muebles.

**Evite permitir búsquedas en estos atributos:**

- **Descripciones o especificaciones largas**: si hay demasiado texto, se generará ruido y coincidencias inesperadas.
- **Rutas de categorías**: puede causar resultados irrelevantes debido a términos de taxonomía amplios.
- **Códigos SKU internos con caracteres mixtos**: crea falsos positivos en coincidencias parciales.
- **Campos administrativos**: Las notas internas o los códigos de almacén no son relevantes para los compradores.
- **Etiquetas de contenido o formato de HTML**: el contenido técnico no mejora la relevancia.

#### Problemas comunes causados por atributos incorrectos en los que se puede buscar

Hacer que se puedan buscar los atributos incorrectos puede frustrar a los compradores y crear escalaciones de soporte.

| Ejemplo | Escenario | Recomendación |
|---------|----------|----------------|
| **Transformación y autocompletar efectos secundarios** | Un comerciante hace que las descripciones de productos largas puedan buscarse. Un comprador busca &quot;lata&quot; (buscando contenedores). Debido a la segmentación y a la coincidencia parcial, aparecen productos con &quot;puede&quot; como parte de palabras más grandes en sus descripciones, como &quot;americano&quot;, &quot;dosel&quot; o &quot;lienzo&quot;. Los productos no están relacionados con la superficie de intención del comprador y pierden confianza en la búsqueda. | Reduzca los campos en los que se pueden buscar a atributos de alta intención como el nombre del producto y la descripción principal. Valide los términos de búsqueda principales para identificar coincidencias problemáticas. Utilice reglas de comercialización o redirecciones de búsqueda para administrar casos extremos conocidos específicos. |
| **La clasificación por popularidad amplifica la coincidencia ruidosa** | Un comerciante establece la clasificación en &quot;Más comprados&quot; e incluye rutas de categoría y descripciones largas como atributos en los que se puede buscar. Un comprador busca &quot;bolsa de ordenador portátil&quot;. La combinación amplia devuelve bolsas para portátiles, accesorios para portátiles, bolsas para otros fines y los propios portátiles. Puesto que los portátiles se adquieren con mayor frecuencia que las maletas para portátiles, ocupan el primer puesto. El comprador percibe la clasificación como incorrecta, aunque el sistema funcione según lo configurado. | Elimine los atributos en los que se pueden realizar búsquedas ruidosas como las rutas de categoría. Una vez que el conjunto de coincidencias sea más preciso, aplique estrategias de clasificación basadas en la popularidad. Monitorice los análisis de búsqueda para identificar consultas donde se produce este patrón. |
| **La ruta de categoría crea falsos positivos** | Un comerciante puede buscar en la ruta de categoría completa (por ejemplo, &quot;Hogar > Cocina > Electrodomésticos > Electrodomésticos pequeños&quot;). Un comprador busca &quot;escritorio de oficina en casa&quot;. Los productos de la categoría &quot;Inicio&quot; coinciden incluso si son artículos de cocina, ya que &quot;hogar&quot; existe en su ruta de categoría. Aparatos de cocina, decoración del hogar y otros productos no relacionados aparecen en los resultados, diluyendo la relevancia. | No permita que se puedan buscar en las rutas de categorías; utilice facetas en su lugar para permitir que los compradores filtren por categoría. Si el filtrado de categorías es esencial para la estrategia de búsqueda, impleméntelo a través de reglas de comercialización en lugar de atributos en los que se pueda buscar. |

#### Ponderación adecuada de atributos en los que se puede buscar

Para aumentar la relevancia de la búsqueda, asigne una ponderación a cada atributo en el que se pueda buscar. Los atributos con un peso mayor deben aparecer más arriba en los resultados de búsqueda. La ordenación por relevancia se ve afectada por varios criterios, como el peso de la búsqueda. Esto significa que, a veces, los atributos con una ponderación de búsqueda menor pueden seguir teniendo más relevancia que los atributos con una ponderación de búsqueda mayor. Otros criterios pueden incluir el número de coincidencias en cualquier atributo determinado, la posición del término de búsqueda encontrado y la estructura de texto general antes y después de un término de búsqueda.

**Prioridades de peso:**

- **Peso más alto (9-10):** Nombre del producto, marca
- **Peso de Medium (6-8):** Número de modelo, descripción principal, características clave
- **Menor peso (3-5):** Descripciones secundarias, materiales, especificaciones

Asegúrese de que cada producto tenga contenido relevante dentro de cada atributo en el que se puede buscar. No se recomienda establecer un atributo como en el que se pueda buscar si tiene grandes cantidades de contenido, ya que esto puede reducir la relevancia de los resultados de búsqueda.

#### Resolución de problemas

Si los resultados de búsqueda parecen aleatorios o irrelevantes, utilice esta lista de comprobación antes de escalar como defecto de producto:

1. **Revisar la configuración de atributos en los que se puede buscar:**

   - Enumerar todos los atributos configurados actualmente como en los que se puede buscar.
   - Identifique cualquier atributo amplio o ruidoso (descripciones largas, rutas de categoría, campos administrativos).
   - Elimine el estado en el que se puede buscar de los atributos que no representan la intención del comprador.

1. **Validar coincidencias de consulta con atributos principales:**

   - Pruebe las consultas de búsqueda más comunes.
   - Compruebe que los resultados coinciden principalmente en el nombre del producto y la marca en lugar de en el texto tangencial.
   - Compruebe si los resultados inesperados solo comparten coincidencias débiles en el contenido de formulario largo.

1. **Prueba con y sin campos ruidosos:**

   - Eliminar temporalmente el estado en el que se puede buscar de la ruta de categoría y los campos de descripción larga.
   - Vuelva a ejecutar las consultas problemáticas para ver si la relevancia mejora.
   - Si los resultados mejoran, ajuste la configuración de forma permanente.

1. **Usar reglas de comercialización para excepciones:**

   - Para consultas conocidas específicas que necesiten un tratamiento especial, cree reglas de búsqueda segmentadas.
   - No intente resolver casos extremos haciendo que se puedan buscar más atributos.
   - Utilice redirecciones para búsquedas de nombres de marcas o errores ortográficos comunes.

1. **Supervisar e iterar:**

   - Use [espacio de trabajo de rendimiento](performance.md) para rastrear la tasa de resultados cero y las tasas de clics.
   - Revise las consultas de búsqueda principales semanalmente para identificar nuevos patrones.
   - Ajuste los atributos y pesos que permiten búsqueda en función de los datos, no de las suposiciones.

Obtenga más información sobre los atributos de producto para la búsqueda:

- [Definir atributos como en los que se puede buscar](workspace.md#set-attributes-as-searchable)
- [Asignar peso a atributos](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results#weighted-search)

## Monitorización de resultados de búsqueda

Para optimizar los resultados de búsqueda con [!DNL Live Search], supervise los indicadores clave de rendimiento (KPI) relevantes, como las consultas únicas, la posición de clics promedio, las tasas de pulsaciones, la tasa de conversión y la tasa de resultados cero, a fin de comprender cómo los compradores interactúan con la funcionalidad de búsqueda. Estos datos le guían para actualizar y perfeccionar regularmente las reglas de búsqueda.

Puede supervisar estos KPI en el [!DNL Live Search] [espacio de trabajo de rendimiento](performance.md) donde encuentra las siguientes métricas: 

- **Búsquedas únicas**: El recuento de consultas de búsqueda distintas realizadas en el sitio [!DNL Commerce]. Cada búsqueda única se cuenta solo una vez, incluso si la repite varias veces el mismo comprador o distintos compradores. Esta métrica le ayuda a comprender la diversidad de términos de búsqueda utilizados por los clientes y proporciona información sobre los productos o la información que buscan los compradores. El seguimiento de búsquedas únicas le permite:

   - Identificar las tendencias de búsqueda populares y los elementos buscados con frecuencia.
   - Detecte posibles lagunas en el catálogo de productos o en el contenido.
   - Optimice la funcionalidad de búsqueda agregando [sinónimos](synonyms.md), creando o actualizando reglas de búsqueda.

- **Posición de clic promedio**: indica que la posición promedio de los resultados de búsqueda en los que hicieron clic los compradores después de realizar una consulta de búsqueda en el sitio. Esta métrica proporciona perspectivas sobre la relevancia y la eficacia de los resultados de búsqueda.

  Una posición de clic promedio más baja (más cercana a 1) sugiere que los compradores encuentran resultados relevantes rápidamente, lo que indica que la estrategia de búsqueda es eficaz. Ayuda a comprender el comportamiento del comprador y hasta dónde está dispuesto a desplazarse para encontrar el producto deseado. Si la posición del clic promedio es alta, puede indicar que los resultados más relevantes no aparecen en la parte superior, lo que requiere una revisión y optimización de su estrategia de búsqueda.

- **Tasa de clics (CTR)**: mide el porcentaje de compradores que hacen clic en un resultado de búsqueda después de realizar una consulta de búsqueda. Un CTR alto indica que los resultados de búsqueda son relevantes y atractivos para los compradores, ya que están haciendo clic en los resultados que encuentran. La monitorización del CTR puede ayudar a identificar áreas de mejora. Un CTR bajo puede sugerir que los resultados de búsqueda no coinciden con la intención del comprador, lo que provoca la necesidad de refinar las reglas de búsqueda, mejorar los datos del producto o mejorar la presentación de los resultados.

- **Tasa de conversión**: indica la eficacia de la característica de búsqueda para impulsar las ventas y lograr los objetivos empresariales. Refleja la eficacia general de la funcionalidad de búsqueda para satisfacer las necesidades del comprador y facilitar una experiencia de compra sin problemas. Una tasa de conversión alta indica que los resultados de búsqueda son muy relevantes y persuasivos, lo que lleva a los compradores a completar compras. Si la tasa de conversión es baja, puede sugerir problemas con la relevancia de la búsqueda, la disponibilidad del producto o el recorrido general del comprador desde la búsqueda hasta la compra.

- **Resultados cero**: mide el porcentaje de consultas de búsqueda en el sitio [!DNL Commerce] que no devuelven resultados. Esta métrica es crucial para comprender con qué frecuencia las búsquedas de los compradores no tienen éxito y puede proporcionar perspectivas sobre posibles lagunas en el catálogo de productos o la configuración de búsqueda. Una tasa de resultados cero alta puede frustrar a los compradores, lo que conduce a una mala experiencia de compra y a una posible pérdida de clientes. Puede indicar productos o categorías que faltan en el catálogo que los compradores están buscando, lo que guía las decisiones de inventario y lista de productos.

  Para reducir la tasa de resultados cero, puede:

   - Ofrezca términos de búsqueda alternativos o relacionados, como [sinónimos](synonyms.md), cuando no se encuentren coincidencias exactas.
   - Revise con regularidad las consultas de resultados cero para identificar patrones y realizar los ajustes necesarios en el catálogo de productos y la configuración de búsqueda.

- **Resultados populares**: puede mejorar significativamente los resultados de búsqueda al alinearlos con las preferencias y los comportamientos de los compradores.

Puede utilizar estos datos de métricas para optimizar la funcionalidad de búsqueda de las siguientes maneras:

- Implemente reglas para clasificar automáticamente los productos más populares en los resultados de búsqueda. Los productos en los que se hace clic con frecuencia o que se compran pueden tener prioridad para aparecer en la parte superior. Seleccione manualmente listas de productos populares para consultas de búsqueda específicas y asegúrese de que estos artículos se muestran de forma destacada.
- Resaltar productos que actualmente son tendencias o que recientemente han visto un pico en popularidad. Esto puede ser especialmente eficaz durante eventos de temporada, festivos o períodos promocionales. Para conseguirlo, utilice la clasificación inteligente que mejor se adapte a su caso de uso y a sus necesidades comerciales al configurar una regla de búsqueda.
- Resalte los filtros o facetas populares, si los compradores filtran con frecuencia por determinadas marcas o intervalos de precios, resalte esas opciones fijando esas facetas y ordenándolas en consecuencia.
- Cuando una búsqueda no genere resultados, use datos de resultados populares para sugerir productos alternativos o categorías relacionadas que tengan una alta participación del comprador.
- Analice los términos de búsqueda populares y los datos del producto para identificar palabras clave importantes. Optimice los atributos en los que se puede buscar productos con estas palabras clave para mejorar la relevancia de la búsqueda.
- Analice con regularidad los datos de resultados para comprender los cambios en las tendencias, las preferencias y el comportamiento de los compradores, identificar los términos de búsqueda principales y detectar problemas. Utilice este bucle de comentarios para refinar y mejorar continuamente sus reglas de búsqueda y ofertas de productos

Para obtener los datos correctos en el informe [!DNL Live Search], debe asegurarse de que el evento se implementa correctamente. Para los comerciantes de Luma, los eventos están disponibles de forma predeterminada. Para implementaciones sin encabezado o personalizadas, debe [implementar eventos](https://developer.adobe.com/commerce/services/shared-services/storefront-events/) según sus necesidades específicas.
