---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '1555'
ht-degree: 0%
---
Cuando crea una recomendación, crea una _unidad de recomendación_ o widget que contiene _elementos_ del producto recomendado.

![Unidad de recomendación](/help/assets/ccdm-shared/recommendations/unit.png)
_Unidad de recomendación_

Cuando activa la unidad de recomendación, Adobe Commerce empieza a [recopilar datos](/help/optimizer/manage-results/recommendation-performance.md) para medir impresiones, vistas, clics, etc. La tabla Recommendations muestra las métricas de cada unidad de recomendación para ayudarle a tomar decisiones comerciales fundadas.

1. En el menú, ve a _Comercialización_ > **Recomendaciones** para mostrar el espacio de trabajo de _Recommendations_.

1. En el campo **Vista de catálogo**, seleccione la vista de catálogo en la que desea que la recomendación esté disponible. Más información acerca de [usar vistas de catálogo para recommendations](/help/optimizer/manage-results/recommendation-performance.md#select-catalog-view).

1. Haga clic en **Crear recomendación**.

   La recomendación que cree estará disponible en la vista de catálogo seleccionada anteriormente.

1. En la sección _Asigne un nombre a la recomendación_, escriba un nombre descriptivo para la referencia interna, como `Home page most popular`.

1. En la sección **Referencia de tienda**, escribe una clave de referencia para identificar esta unidad de recomendación en tu configuración de tienda. Después de crear la recomendación, puede [copiar su valor](#get-the-storefront-reference-key) de **Detalles de la unidad de recomendación** y utilizarlo como `referenceKey` en el bloque de recomendaciones. La clave de referencia es para la configuración de tienda; la etiqueta de visualización de tienda es el texto que ven los compradores.

1. En la sección _Seleccionar tipo de recomendación_, especifique el [tipo de recomendación](types.md) que desee en función de su estrategia.

1. En la sección _Etiqueta para mostrar en la tienda_, escribe la [etiqueta](best-practice.md#recommendation-labels) que sea visible para tus compradores, como &quot;Principales vendedores&quot;.

1. En la sección _Elegir número de productos_, use el control deslizante para especificar cuántos productos desea que aparezcan en la unidad de recomendación.

   El valor predeterminado es `5`, con un máximo de `20`.

1. (Opcional) En la sección _Filtros_, [aplique filtros](filters.md) para controlar qué productos aparecen en la unidad de recomendación.

1. Utilice el panel _Vista previa de productos recomendados_ para comprender mejor cómo afectan los filtros a los productos que se muestran en la unidad de recomendación. Obtenga más información sobre cómo [obtener una vista previa de las recomendaciones](#preview-recommendations).

1. Cuando termine, haga clic en una de las siguientes opciones:

   - **Guardar como borrador** para editar la unidad de recomendación más adelante. No se puede modificar el tipo de recomendación para una unidad de recomendación en estado de borrador.

   - **Activar** para habilitar la unidad de recomendación en tu tienda.

   La recomendación aparecerá en el área de trabajo de Recommendations. Para usar tu recomendación en tu tienda, necesitas el [ID de recomendación o la clave de referencia](#get-the-storefront-reference-key).

>[!NOTE]
>
>Puede crear hasta 50 unidades de recomendación activas. Consulte [Límites y límites](/help/optimizer/boundaries-limits.md) para obtener detalles.

>[!IMPORTANT]
>
>Algunos exploradores pueden bloquear los scripts esenciales que impiden que Recommendations funcione según lo esperado.

## Previsualizar recomendaciones

El panel _Vista previa de productos recomendados_ siempre está disponible con una selección de muestra de productos que pueden aparecer en la unidad de recomendación cuando se implemente en la tienda.

![Vista previa de recomendaciones](/help/assets/ccdm-shared/recommendations/rec-preview.png)

Para probar una recomendación cuando se trabaja en un entorno que no es de producción, puede recuperar datos de recomendación de una fuente diferente. Esto permite a los comerciantes experimentar con las reglas y previsualizar las recomendaciones antes de implementarlas en la producción.

| Campo | Descripción |
|---|---|
| Vista de catálogo |  |
| Nombre | El nombre del producto. |
| SKU | La unidad de stock asignada al producto |
| Precio | El precio del producto. |
| Tipo de resultado | Principal: Indica que hay suficientes datos de formación recopilados para mostrar una recomendación.<br />Copia de seguridad: indica que no se recopilaron suficientes datos de formación, por lo que se usa una recomendación de copia de seguridad para rellenar el espacio. Vaya a [Datos de comportamiento](/help/optimizer/setup/events/overview.md) para obtener más información acerca de los modelos de aprendizaje automático y las recomendaciones de copia de seguridad. |

Para obtener comentarios inmediatos en tiempo real sobre los productos que se incluirán, experimente con el tipo de recomendación y los filtros a medida que crea su unidad de recomendación. Para satisfacer sus necesidades comerciales, configure la unidad de recomendación a medida que empiece a comprender qué productos aparecen.

[!DNL Product Recommendations] [filtrar](filters.md) recomendaciones para evitar mostrar productos duplicados cuando se implementan varias unidades de recomendación en una sola página. Como resultado, los productos que aparecen en el panel de vista previa pueden diferir de los que aparecen en la tienda.

Para configuraciones de varias tiendas, idiomas o marcas, puede configurar si cada recomendación se aplica a todas las vistas de catálogo (globales) o a una sola [vista de catálogo](/help/optimizer/setup/catalog-view.md). Obtenga más información sobre cómo [establecer la vista de catálogo](/help/optimizer/manage-results/recommendation-performance.md#select-catalog-view) al trabajar con recomendaciones.

## Obtener la clave de referencia de tienda

Después de crear una recomendación, use su clave de referencia para configurar la unidad de recomendación en la tienda.

1. En la página **Recommendations**, haga clic en el icono de información (![icono de información](/help/assets/ccdm-shared/recommendations/info-icon.png)) situado junto al nombre de la recomendación para abrir la página **Detalles de la unidad de recomendación**.

   ![Obtener ID de recomendación](/help/assets/ccdm-shared/recommendations/get-ref-id.png)

1. Copie el valor de la sección **Clave de referencia de tienda**.

1. En el bloque de la tienda `product-recommendations`, usa esta clave de referencia para configurar la [entrega de recomendaciones](https://experienceleague.adobe.com/en/tools/commerce-storefront/merchants/blocks/product-recommendations/) en tu tienda de Edge Delivery Services.

## Administrar recomendaciones existentes

Puede editar, desactivar o eliminar una recomendación existente.

1. En el menú, ve a _Comercialización_ > **Recomendaciones**.

1. Seleccione la recomendación que desee modificar.

1. Haga clic en el selector más (![Más](/help/assets/ccdm-shared/recommendations/btn-more.png)).

1. En el menú, puedes **Desactivar**, **Eliminar** o **Editar** la recomendación. Si selecciona **Editar**, puede ajustar la siguiente configuración según sea necesario:

   - Nombre de recomendación
   - Clave de referencia
   - Etiqueta de tienda
   - Número de productos
   - Filtrar productos

   No se puede cambiar el tipo de recomendación ni la vista de catálogo. La vista de catálogo se establece al crear la recomendación. Para obtener más información, consulte [seleccionar vista de catálogo](/help/optimizer/manage-results/recommendation-performance.md#select-catalog-view).

1. Una vez finalizado, haga clic en **Guardar cambios**.

## Indicadores de preparación

Los indicadores de preparación muestran qué tipos de recomendación funcionan mejor según los datos de catálogo y de comportamiento disponibles. También pueden ayudarle a identificar posibles problemas con [la colección de eventos](/help/optimizer/setup/events/overview.md) o a determinar si un tipo de recomendación no está recibiendo tráfico suficiente para generar resultados.

Los indicadores de preparación se clasifican en [estáticos](#static-based) o [dinámicos](#dynamic-based). Las recomendaciones estáticas solo utilizan datos de catálogo, mientras que las recomendaciones dinámicas utilizan datos de comportamiento de los compradores. Esos datos de comportamiento se usan para [entrenar modelos de aprendizaje automático](/help/optimizer/setup/events/overview.md) para generar recomendaciones personalizadas y calcular su puntuación de preparación.

### Cálculo de los indicadores de disponibilidad

Los indicadores de disponibilidad indican cuánto se ha entrenado el modelo. Los indicadores dependen de los tipos de eventos recopilados, la amplitud de los productos con los que interactuó y el tamaño del catálogo.

El porcentaje del indicador de preparación se deriva de un cálculo que indica cuántos productos se pueden recomendar según el tipo de recomendación. Las estadísticas se aplican a los productos en función del tamaño total del catálogo, el volumen de interacción (vistas, clics, complementos a los carros de compras) y el porcentaje de SKU que registran esos eventos en un período de tiempo determinado. Por ejemplo, durante el tráfico máximo de la temporada de vacaciones, los indicadores de disponibilidad pueden mostrar valores más altos que en tiempos de volumen normal.

Como resultado de estas variables, el porcentaje del indicador de disponibilidad puede fluctuar. Esta fluctuación explica por qué los tipos de recomendación cambian entre &quot;Listo para implementar&quot; y no.

Los indicadores de preparación se calculan en función de varios factores:

- Tamaño suficiente del conjunto de resultados: ¿Se devuelven suficientes resultados en la mayoría de los casos para evitar el uso de [recomendaciones de copia de seguridad](/help/optimizer/setup/events/overview.md#backup-recommendations)?
- Variedad del conjunto de resultados suficiente: ¿los productos que se devuelven representan una variedad de productos del catálogo? El objetivo con este factor es evitar tener una minoría de productos como los únicos recomendados en todo el sitio.

En función de los factores anteriores, se calcula un valor de disponibilidad y se muestra de la siguiente manera:

- 75 % o más significa que las recomendaciones sugeridas para ese tipo de recomendación son altamente relevantes.
- Al menos el 50 % significa que las recomendaciones sugeridas para ese tipo de recomendación son menos relevantes.
- Menos del 50 % significa que las recomendaciones sugeridas para ese tipo de recomendación pueden no ser relevantes. En este caso, se utilizan [recomendaciones de copia de seguridad](/help/optimizer/setup/events/overview.md#backup-recommendations).

Obtenga más información acerca de [por qué los indicadores de preparación pueden ser bajos](#what-to-do-if-the-readiness-indicator-is-low).

### Basado en estáticas

Los siguientes tipos de recomendación son de base estática porque solo requieren datos de catálogo. No se utilizan datos de comportamiento.

- _Más como este_

### Basado en dinámico

Los siguientes tipos de recomendación son dinámicos, ya que utilizan datos de comportamiento de tienda.

Últimos seis meses de datos de comportamiento de la tienda:

- _Vio esto, vio aquello_
- _Vio esto, compró aquello_
- _Compró esto, compró aquello_
- _Recomendado para usted_

Últimos siete días de datos de comportamiento de la tienda:

- _Más visitados_
- _Más comprados_
- _Más Añadidos al Carro_
- _Tendencia_
- _Conversión de vista a compra_
- _Conversión de vista a carro_

Datos más recientes del comportamiento del comprador (solo vistas):

- _Vistos recientemente_

### Visualización del progreso

Para ayudarle a visualizar el progreso de formación de cada tipo de recomendación, la sección _Seleccionar tipo de recomendación_ muestra una medida de preparación para cada tipo.

![Tipo de recomendación](/help/assets/ccdm-shared/recommendations/create-recommendation-select-type.png)
_Tipo de recomendación_

>[!NOTE]
>
>Los indicadores nunca pueden alcanzar el 100%.

El indicador de preparación para los tipos de recomendación que dependen de los datos del catálogo no cambia mucho, ya que el catálogo del comerciante rara vez cambia. Sin embargo, el indicador de preparación para los tipos de recomendación basados en los datos de comportamiento del comprador puede cambiar a menudo según la actividad diaria del comprador.

#### Qué hacer si el indicador de disponibilidad está bajo

Un porcentaje de preparación bajo indica que no hay muchos productos del catálogo que puedan incluirse en las recomendaciones de este tipo de recomendación. Esto significa que existe una alta probabilidad de que se devuelvan [recomendaciones de copia de seguridad](/help/optimizer/setup/events/overview.md#backup-recommendations) si implementa este tipo de recomendación de todos modos.

>[!IMPORTANT]
>
>Cualquier SKU con espacios puede reducir la relevancia de la recomendación y debe evitarse.

A continuación se enumeran los posibles motivos y soluciones para puntuaciones de preparación bajas comunes:

- **Basado en estáticas**: La falta de datos de catálogo para los productos mostrables causa porcentajes bajos para estos indicadores. Si son inferiores a lo esperado, una sincronización completa puede solucionar este problema.
- **Basado en dinámica**: los siguientes factores causan porcentajes bajos para los indicadores basados en dinámica:

  - Faltan campos en los [eventos de tienda](/help/optimizer/setup/events/overview.md) necesarios para los tipos de recomendación respectivos (requestId, contexto de producto, etc.).
  - Poco tráfico al almacén, por lo que el volumen de eventos de comportamiento recibidos es bajo.
  - La variedad de eventos de comportamiento de la tienda en diferentes productos es baja. Por ejemplo, si solo el diez por ciento de sus productos se ven o se compran la mayor parte del tiempo, los indicadores de preparación respectivos son bajos.
