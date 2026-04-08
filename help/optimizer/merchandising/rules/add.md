---
title: Crear y administrar reglas
description: Obtenga información sobre cómo crear y administrar reglas de comercialización para búsquedas, listados de productos predeterminados y páginas de categorías.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
exl-id: fd4df2b2-83de-4c5c-b18c-e97aa07ef8f6
source-git-commit: 0d1ebaddada8be82645164368ebfbb6dd0a569cd
workflow-type: tm+mt
source-wordcount: '2714'
ht-degree: 0%

---

# Crear y administrar reglas

Para generar una regla, abra el editor de reglas, elija un **tipo de regla** (condiciones de búsqueda, lista predeterminada o páginas de categoría), luego defina las condiciones y la clasificación donde se apliquen, pruebe los resultados y publique la regla.

## Crear una regla {#create-a-rule}

1. En el carril izquierdo, vaya a _Reglas de comercialización_ > **Reglas de comercialización**.
1. (Opcional) Utilice la lista desplegable **Vista de catálogo** para seleccionar la vista de catálogo donde se debe aplicar la regla. La regla que cree se vinculará a la vista seleccionada (o a todas las vistas de catálogo si está seleccionada la opción **Todas las vistas**). Consulte [Seleccionar vista de catálogo](workspace.md#select-catalog-view) para ver cómo funciona el ámbito de la vista de catálogo.

   >[!IMPORTANT]
   >
   >Las vistas del catálogo se encuentran actualmente en [beta](https://experienceleague.adobe.com/es/docs/commerce-operations/release/beta#merchandising-rules-globally-and-per-catalog-view-public-beta). Los participantes de Beta deberán volver a crear las reglas de comercialización existentes para aprovechar el nuevo ámbito de vista de catálogo.

1. Haga clic en **[!UICONTROL Create rule]** para iniciar el editor de reglas.

![Crear regla](../../assets/create-rule.png)

### Tipos de reglas

Cada tipo de regla tiene un icono de información en el editor con una breve explicación. Utilice el tipo que coincida con el lugar en el que los compradores deben ver la lógica de comercialización:

| Tipo de regla | Finalidad |
| --- | --- |
| **Regla de todos los productos** | Clasificación y comercialización predeterminadas en todas las listas de productos cuando no se aplica ninguna regla de categoría o búsqueda más específica. Solo puede crear una de estas reglas; no puede contener condiciones. |
| **Regla de categoría** (Beta) | Aplica la comercialización y la clasificación a una o varias categorías seleccionadas y controla el orden de los productos en esas páginas de categorías. |
| **Regla de búsqueda** | Aplica la comercialización y la clasificación cuando los compradores ejecutan una búsqueda que coincide con las condiciones de consulta de la regla. |

En la sección **Generar la regla**, define el nombre de la regla, la programación, si la regla se aplica a todos los listados o a condiciones de búsqueda específicas y los tipos de clasificación.

1. En el campo **[!UICONTROL Name]**, escriba un nombre para la regla. Todos los nombres de reglas deben ser únicos.
1. En el campo **[!UICONTROL Description]**, escriba una descripción para la regla.
1. En el campo **[!UICONTROL Date range]**, especifique la fecha o el intervalo de fechas en que desea que la regla esté activa.
1. En la sección **[!UICONTROL Rule applies to]**, seleccione [tipo de regla](#rule-types) que desee usar.

>[!BEGINTABS]

>[!TAB Regla de búsqueda]

Una regla de búsqueda aplica lógica de comercialización y clasificación cuando los compradores realizan una búsqueda que coincide con las condiciones definidas.

Las condiciones son los requisitos para almacenar en déclencheur un evento. Una regla puede tener hasta diez condiciones y 25 eventos. Una regla predeterminada no puede tener ninguna condición.

![Seleccionar condición de regla](../../assets/rule-set-condition.png)

**Condición única**

1. En *Generar la regla*, seleccione la **condición** que se debe cumplir y siga las instrucciones para completar la instrucción.

   - La consulta de búsqueda contiene: introduzca la cadena de texto que debe estar en la consulta del comprador. La configuración Coincidencia determina el grado de coincidencia de la consulta del comprador con el catálogo. Opciones:<br /> Cualquiera: cualquier parte del texto de consulta del comprador puede coincidir con la condición.<br />Todo: toda la consulta del comprador debe coincidir con la condición.
   - La consulta de búsqueda es: introduzca una cadena de texto que coincida exactamente con la consulta del comprador. Por ejemplo: &quot;pantalones de yoga&quot;. Las reglas con `Search query is` y Coincidencia `All` solo pueden tener una condición.
   - La consulta de búsqueda comienza con: introduzca un carácter o cadena de texto que debe estar al principio de la consulta del comprador.
   - La consulta de búsqueda termina con: introduzca un carácter o cadena de texto que debe estar al final de la consulta del comprador.

   Los resultados aparecen inmediatamente en el panel *Probar la regla* y están numerados por prioridad. Puede usar el control deslizante *Resultados por fila* en la esquina superior derecha para cambiar el número de productos en cada fila.

1. Para probar otras consultas, cambia el texto de la consulta en el cuadro de búsqueda *Probar la regla* y pulsa **Devolver**.
Inicialmente, el panel de prueba procesa la consulta desde el cuadro de búsqueda Condiciones. Pero ahora está procesando la consulta desde el cuadro de consulta de prueba. El panel de prueba procesa solo una consulta a la vez.
1. Si te gusta el resultado, actualiza el texto en el cuadro de búsqueda *Condiciones*. A continuación, haga clic en cualquier lugar de la página para actualizar los resultados en el panel de pruebas.
1. Defina la [clasificación inteligente](#intelligent-ranking) y la [clasificación manual](#manual-ranking) tal como se describe en las secciones siguientes. Los mismos controles se aplican a las páginas de categorías, con todas las diferencias.

**Varias condiciones**

1. Para generar una regla con varias condiciones, haga clic en **Agregar condición**.
Una regla puede tener hasta diez condiciones. El operador lógico que une dos condiciones se basa en la configuración actual de *Match*. De manera predeterminada, *Match* es `All` y el operador lógico es `AND`.

1. Seleccione la segunda condición e introduzca el texto de consulta requerido.

1. Para cambiar la lógica de la regla, cambie la configuración **Match** para determinar en qué medida los criterios de búsqueda del comprador deben coincidir con la condición de consulta. Establezca **Match** en una de las siguientes opciones:

   - Cualquiera - (predeterminado) Todos los operadores lógicos de la regla están configurados en `OR` y los resultados aparecen en el panel de prueba.
   - Todos: todos los operadores lógicos de la regla están configurados en `AND` y los resultados aparecen en el panel de prueba.

   El valor *Match* determina el operador lógico que se usa para unir varias condiciones. Si se cambia la configuración *Match*, se cambiarán todos los operadores lógicos de la regla. No es posible combinar `AND` y `OR` en la misma regla.

   En este ejemplo, en lugar de buscar &quot;pantalones de yoga&quot;, hay dos consultas independientes que buscan &quot;yoga&quot; o &quot;pantalones&quot;. Esta regla es menos específica y se activa con más frecuencia en la tienda que la otra.

1. Para agregar otra condición, haga clic en **Agregar condición** y repita el proceso.
1. Defina la [clasificación inteligente](#intelligent-ranking) y la [clasificación manual](#manual-ranking) tal como se describe en las secciones siguientes. Los mismos controles se aplican a las páginas de categorías, con todas las diferencias.

>[!TAB Regla de categoría]

>[!IMPORTANT]
>
>Las reglas de categoría están en versión beta.

Las reglas de categoría controlan cómo se ordenan los productos en **páginas de categoría**. Combinas **reglas de categoría** con **clasificación inteligente** (incluidas las señales controladas por IA) y **acciones manuales** como fijar, impulsar y enterrar, para que puedas revisar la detección, ejecutar promociones y alinear las páginas de categoría con tu estrategia sin depender de herramientas externas.

1. En **Categorías**, seleccione la categoría o categorías a las que se debe aplicar la regla. Las categorías seleccionadas aparecen debajo del control para que pueda confirmar el ámbito.
1. En la lista de categorías que aparecen, puede hacer clic en los tres puntos y seleccionar lo siguiente:

   - **Eliminar** - Elimina la categoría de la regla.
   - **Aplicar a subcategorías**: aplica la regla a subcategorías que aún no tienen definida una regla de comercialización activa.
   - **Vista previa**: muestra cómo aparecería la página de la categoría en tu tienda.

1. Defina la [clasificación inteligente](#intelligent-ranking) y la [clasificación manual](#manual-ranking) tal como se describe en las secciones siguientes. Los mismos controles se aplican a las reglas de búsqueda, con cualquier diferencia destacada.

>[!ENDTABS]

### Clasificación inteligente {#intelligent-ranking}

La clasificación inteligente ordena los productos mediante **señales de comportamiento** y, cuando corresponde, IA. Se aplica a **reglas de búsqueda**, **todas las listas de productos** (reglas predeterminadas) y **reglas de categoría** (páginas de categoría). Para las **búsquedas** del comprador, la clasificación también pesa **relevancia textual** para la consulta; las **páginas de categoría** no utilizan el texto de consulta de la misma manera: el editor se centra en estrategias de comportamiento.

Los propietarios de tiendas pueden definir estrategias como las siguientes. Las etiquetas exactas y las ventanas de tiempo coinciden con el editor de reglas y pueden diferir ligeramente por tipo de regla.

![Clasificaciones inteligentes](../../assets/rule-intelligent-ranking.png)

- **Más comprados** / **Más comprados** — Clasifica por frecuencia de compra por SKU en una ventana reciente (por ejemplo, los 7 días anteriores para contextos de búsqueda).
- **Más agregados al carro** — Clasifica por actividad total de complemento al carro en una ventana reciente (por ejemplo, los 7 días anteriores para contextos de búsqueda).
- **Más visitados**: clasifica por vistas por SKU en una ventana reciente (por ejemplo, los 7 días anteriores para contextos de búsqueda).
- **Recomendado para usted** — Utiliza la señal `viewed-viewed`: los compradores que vieron este SKU también vieron otros SKU; admite pedidos personalizados en páginas de categoría donde estén disponibles.
- **Tendencia**: Enfatiza la popularidad reciente (para búsquedas, vistas de página de las últimas 72 horas para eventos en segundo plano y 24 horas para eventos en primer plano).
- **Ninguno**: para la búsqueda y los listados predeterminados, los productos se solicitan por **Relevancia**. Para **reglas de categoría**, utiliza el orden de comercialización predeterminado para la categoría cuando no elige otra estrategia inteligente.

Seleccione la estrategia para la regla. El panel **Probar la regla** muestra los resultados esperados para las reglas orientadas a la búsqueda; **las reglas de categoría** utilizan la vista previa de categoría.

#### Funcionamiento de la puntuación de clasificación inteligente (búsqueda)

Para **resultados de búsqueda** (y la consulta de prueba en el editor de reglas), la clasificación inteligente determina el orden final del producto combinando dos factores clave: **relevancia textual** y **señales de comportamiento**. Comprender cómo interactúan estos factores le ayuda a establecer expectativas realistas en los resultados de búsqueda.

**Componentes de puntuación:**

- **Relevancia textual**: El factor dominante en la puntuación. Esto mide en qué medida coinciden el nombre, la descripción y los atributos de un producto con la consulta de búsqueda. La puntuación de relevancia del texto es ilimitada (no tiene un límite superior específico) y se ve afectada por factores como:

   - Frecuencia de aparición de palabras coincidentes.
   - Longitud (en palabras) de los nombres y descripciones de los productos.

- **Señales de comportamiento**: un aumento limitado aplicado sobre la puntuación de relevancia de texto. Al seleccionar una estrategia de clasificación inteligente como &quot;Más visitados&quot; o &quot;Más comprados&quot;, los productos con señales de comportamiento más altas reciben un impulso fijo en sus puntuaciones. Sin embargo, este impulso tiene un límite definido.

**Es posible que el producto más visitado no aparezca primero:**

La relevancia textual suele dominar la clasificación porque su puntuación es ilimitada, mientras que los aumentos de comportamiento son fijos. Como resultado, los productos con texto fuerte coinciden a menudo con los que tienen señales de participación más altas. Los aumentos de comportamiento por sí solos pueden no compensar las grandes brechas en la relevancia del texto. La clasificación inteligente soluciona esto al tener en cuenta la calidad de las coincidencias y la interacción con el comprador, lo que mejora la relevancia general. Sin embargo, la calidad de la coincidencia de texto sigue siendo el principal motor de la clasificación.

**Ejemplo:**

Un comerciante usa la estrategia de clasificación inteligente &quot;Más visto&quot; y busca &quot;vela&quot;. Se espera que el SKU del producto YAN-K-E-512 aparezca en la parte superior de los resultados porque tiene el recuento de vistas más alto. Sin embargo, otros productos tienen una clasificación más alta:

- **Vela de Texas** (primera posición): tiene un nombre de producto más corto y limpio que crea una puntuación de relevancia de texto muy alta. Aunque tiene menos vistas que YAN-K-E-512, su coincidencia de texto superior supera el impulso de comportamiento.

- **YAN-K-E-512** (posición inferior): a pesar de tener el percentil de vista más alto en los datos de comportamiento &quot;Más visitados&quot;, su nombre complejo basado en SKU genera una puntuación de relevancia de texto más baja. El impulso de comportamiento fijo no es suficiente para superar esta brecha de relevancia del texto.

Consulte [reglas de búsqueda](./best-practice.md#tips-to-optimize-search-rules) para obtener información sobre cómo mejorar la capacidad de búsqueda de productos mediante el uso de reglas.

#### Advertencias

- Los apóstrofos y las citas en las consultas pueden llevar a algunos problemas menores con clasificación y relevancia en algunos idiomas.
- Para garantizar que la clasificación inteligente funcione correctamente en **search**, asegúrate de que **Search Weight** para cualquier atributo que se use para la búsqueda o el filtrado (facetas) sea `5` o menos. (Esta guía se aplica a la indexación de búsqueda, no a los flujos de comercialización solo de categoría).

Para obtener información acerca de cómo establecer pesos de búsqueda, consulte la [API de metadatos](https://developer.adobe.com/commerce/services/reference/rest/).

### Clasificación manual {#manual-ranking}

**La clasificación manual** eventos ajusta el orden del producto para **resultados de búsqueda** (cuando se cumplen las condiciones de la regla), para **listados de productos predeterminados** y para **listados de páginas de categorías**. Una sola regla puede tener hasta 25 eventos.

- **Aumentar**: mueve un producto a una posición superior en el listado.
- **Enterrar**: mueve un SKU a una posición inferior en el anuncio.
- **Anclar un producto**: corrige un producto en la posición seleccionada del listado.
- **Ocultar un producto**: excluye un SKU de los resultados (orientado a la búsqueda; confirme el comportamiento de las reglas de categoría en el editor).

La forma más sencilla de anclar un producto es arrastrando y soltando.

1. Haga clic y arrastre un producto en el panel Prueba. Arrástrela y suéltela en la posición deseada. Los campos Producto y Posición se rellenan automáticamente en el panel Eventos.

También puede hacer clic en el icono de anclaje para anclar un producto a su ubicación actual. Utilice el menú contextual de los tres puntos para &quot;Anclar al principio&quot; o &quot;Anclar al final&quot;.

>[!NOTE]
>
>**Reglas de búsqueda**: solo puede anclar productos que aparezcan en los resultados de búsqueda para las condiciones de consulta y regla configuradas. Los productos deben estar indexados, ser visibles, estar en stock y cumplir todos los filtros de regla para poder anclarlos. Si un producto no aparece en la vista previa o en los resultados de la regla, el anclaje no tiene ningún efecto.
>
>**Orden predeterminado**: las posiciones manuales se aplican cuando el comprador usa la ordenación predeterminada: **Ordenar por: Más relevante** para la búsqueda o **relevancia** / **posición** para los listados de categoría. Si el comprador cambia la ordenación; por ejemplo, por nombre, comportamiento anclado, aumentado, enterrado u oculto, puede que ya no coincida con la vista previa.

O los eventos se pueden configurar manualmente:

1. En *Eventos*, elija el **Evento** que se llevará a cabo cuando se cumplan las condiciones asociadas.

   Por ejemplo, elija `Hide a product`. A continuación, introduzca el nombre del producto que desea ocultar. Los productos se sugieren a medida que escribe.

1. Para varios eventos, elija cualquier otro evento que desee almacenar en déclencheur cuando se cumplan las condiciones.

### Finalización de la regla {#finalizing-the-rule}

1. Examine los resultados de la regla en el panel de prueba.
1. Si la regla tiene varias consultas, pruebe cada una de ellas que pueda verse afectada por la regla.
1. Una vez finalizado, haga clic en **Guardar y publicar**.

   La regla se agrega a la lista del área de trabajo *Reglas*.

1. Aunque las reglas activas entran en vigor inmediatamente, es posible que tenga que esperar hasta 15 minutos para que se actualicen los resultados de la consulta en caché en la tienda.

>[!NOTE]
>
>Las reglas y los productos clasificados manualmente se aplican a los resultados de **search** cuando se selecciona el criterio de ordenación predeterminado, &quot;Ordenar por: Más relevante&quot;. Si un comprador cambia el criterio de ordenación a algo parecido a ordenar por nombre, las reglas y las clasificaciones manuales ya no estarán en vigor. Para los anuncios de **category**, el comportamiento de ordenación predeterminada se describe en [Clasificación manual](#manual-ranking).

## Editar, ver y eliminar reglas {#edit-view-and-delete-rules}

Siga estas instrucciones para actualizar las propiedades de las reglas existentes. No se puede cambiar la vista de catálogo (ámbito) de una regla una vez creada; el ámbito se establece al crear la regla. Ver [Seleccionar vista de catálogo](workspace.md#select-catalog-view).

### Editar regla

1. En el área de trabajo *Reglas de comercialización*, busque la regla en la cuadrícula que desea editar y haga clic en las opciones **Más** (...).
1. Haga clic en **Editar** para acceder al editor de reglas.
1. Actualice las condiciones, los operadores y los eventos según sea necesario.
1. Actualice los campos Nombre, Fecha de inicio y finalización y Descripción según sea necesario. Todos los nombres de reglas deben ser únicos.
1. Pruebe la regla.
1. Publique los cambios.
La regla se agrega a la lista del área de trabajo *Reglas*. Aunque las reglas activas entran en vigor inmediatamente, los resultados de las consultas en caché de la tienda pueden tardar hasta 15 minutos en actualizarse.

### Ver detalles

Esta opción proporciona una forma rápida de ver todos los parámetros de regla mientras se mantiene en la tabla *Rules*.

1. En el área de trabajo *Reglas de comercialización*, busque la regla en la cuadrícula que desee editar y haga clic en las opciones **Más** (...).
1. Haga clic en **Ver detalles** para ver los parámetros de la regla.
1. Elija **Editar** o **Eliminar**, o haga clic en la X para cerrar el panel.

### Eliminar regla

1. En el área de trabajo *Reglas*, busque la regla en la cuadrícula que desea editar y haga clic en las opciones **Más** (...).
1. Haga clic en **Eliminar**.

## Descripciones de campos {#field-descriptions}

### Condiciones (si)

| Condición | Descripción |
|--- |--- |
| La consulta de búsqueda contiene | Un carácter o cadena de texto que se incluye en la consulta del comprador. La consulta del comprador debe coincidir con un solo carácter para cumplir esta condición. |
| La consulta de búsqueda es | Carácter o cadena de texto que coincide exactamente con la consulta del comprador. Las consultas complejas con varias condiciones no se pueden crear cuando se utiliza esta condición. |
| La consulta de búsqueda comienza con | La consulta del comprador comienza con este carácter o cadena de texto. |
| La consulta de búsqueda termina con | La consulta del comprador termina con este carácter o cadena de texto. |

### Operadores lógicos

| Operador | Descripción |
|--- |--- |
| O | (Predeterminado) El operador lógico `OR` compara dos condiciones y cumple los requisitos para almacenar en déclencheur un evento si al menos una condición es verdadera. |
| Y | El operador lógico `AND` compara dos condiciones y cumple los requisitos para almacenar en déclencheur un evento si ambas condiciones son verdaderas. |

### Operadores de coincidencia

| Operador | Descripción |
|--- |--- |
| Cualquiera | Cambia todos los operadores lógicos de la regla a `OR` y devuelve el conjunto de productos coincidentes. |
| Todo | Cambia todos los operadores lógicos de la regla a `AND` y devuelve el conjunto de productos coincidentes. |

### Eventos de clasificación manual

| Evento | Descripción |
|--- |--- |
| Aumentar | Sube un SKU o un rango de SKU en el anuncio (búsqueda o categoría). Cada uno está marcado con un distintivo de vista previa &quot;potenciado&quot; en los resultados de la prueba. |
| Enterrar | Mueve un SKU o un rango de SKU a una posición inferior del anuncio. Cada una está marcada con un distintivo de vista previa &quot;enterrado&quot; en los resultados de la prueba. |
| Fijar un producto | Adjunta un único SKU a una posición específica del anuncio. El producto está marcado con un distintivo de vista previa &quot;anclado&quot; en los resultados de la prueba. |
| Ocultar un producto | Excluye un SKU o un rango de SKU de los resultados (orientado a la búsqueda; confirme las reglas de categoría en el editor). |

### Detalles

| Campo | Descripción |
|--- |--- |
| Nombre | Nombre de la regla. Los nombres de las reglas deben ser únicos. |
| Tipo de regla | **Predeterminado** (todas las listas de productos), **Consulta** (condiciones de búsqueda específicas) o **Categoría** (páginas de categoría), según **La regla se aplica a**. |
| Fecha de inicio | La fecha de inicio de la regla, si está programada. |
| Fecha de finalización | La fecha de finalización de la regla, si está programada. |
| Descripción | Breve descripción de la regla. |
