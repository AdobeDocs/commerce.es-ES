---
title: Políticas
description: Obtenga información sobre cómo crear y administrar directivas en  [!DNL Adobe Commerce Optimizer].
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 356b10704c9e7c7329d3e9c0e10baa15d5142ec0
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---

# Políticas

Las directivas son filtros de acceso a datos contenidos en vistas de catálogo que refinan aún más los datos enviados a cada vista de catálogo. Las políticas garantizan que el contenido correcto se envíe al destino correcto. Por ejemplo, tiendas físicas, mercados, canalizaciones de publicidad (Google, Facebook, Instagram).

Las directivas se basan en atributos de producto, como marca, modelo o categoría de artículo, y se utilizan para adaptar los datos del catálogo a los requisitos comerciales específicos. palo de golf

## Filtros

Los filtros son el mecanismo dentro de una directiva que aplica la segmentación de catálogos. Los filtros permiten a las empresas adaptar las tiendas y las vistas de catálogo a conjuntos de productos específicos en función de las necesidades operativas. Los criterios, como atributos de producto, operadores y valores, se utilizan para definir una regla o condición que indique qué productos se incluyen o excluyen de una vista de catálogo o de una tienda.

### Partes de un filtro

Un filtro consta de las siguientes partes:

| Parte | Descripción | Ejemplo |
|---|---|---|
| **Atributo** | Atributo de producto utilizado para el filtrado. | `part_category` |
| **Operador** | La condición aplicada al atributo. | `IN`, `EQUALS`, `CONTAINS` |
| **Origen del valor** | Especifica si los valores son `STATIC` o `TRIGGER`. | `STATIC` [Más información](#value-source-types) |
| **Valor** | Los valores específicos que cumplen la condición. | `brakes, suspension` |

### Ejemplo

Un filtro con el atributo `part_category`, un operador de `IN` y valores `brakes, suspension` garantiza que la directiva filtre y muestre únicamente los productos con un atributo `part_category` que tenga un valor de `brake` o `suspension`.

### Tipos de origen de valor

Existen dos tipos de orígenes de valores: **STATIC** y **DÉCLENCHEUR**.

Las directivas con un **origen Value** de **STATIC** se consideran directivas universales. Las políticas universales definen la experiencia de un sitio web en su conjunto. Esto significa que la vista de catálogo siempre ejecutará esa directiva. En otras palabras, la ejecución de esa política no se basa en ninguna interacción del usuario en la tienda.

Las directivas con un **origen de valor** de **DÉCLENCHEUR** se denominan directivas exclusivas. Esto significa que la vista de catálogo ejecutará esa directiva solo cuando el déclencheur se especifique en el encabezado de la llamada de API. En la tienda, esto significa que la información se muestra en función de lo que seleccione el comprador. Por ejemplo, en la siguiente imagen, hay dos menús desplegables: **Marca** y **Modelo**.

![origen de valor de Déclencheur en tienda](../assets/policy-trigger.png)

**Marca** y **Modelo** son déclencheur definidos:

- `AC-Policy-Brand`
- `AC-Policy-Model`

Si el comprador hace clic en la lista desplegable **Marca**, el encabezado de la llamada de API contiene `AC-Policy-Brand`, que está configurado para mostrar únicamente los productos específicos de la directiva `AC-Policy-Brand`.

## Crear política

En esta sección, se crea una directiva nueva. La directiva puede ser **STATIC** o **DÉCLENCHEUR**.

### Crear una política STATIC

1. En el menú de la izquierda, abra la sección **[!UICONTROL Catalog]** y haga clic en **[!UICONTROL Policies]**.

1. Haga clic en el botón **[!UICONTROL Add Policy]**.

   Se abre una nueva página para que rellene los detalles de la directiva. palo de golf

1. Introduzca el nombre de la política, por ejemplo &quot;Celport Part Categories&quot;.

1. Haga clic en el botón **[!UICONTROL Add Filter]**.

   Se abrirá un cuadro de diálogo para que pueda añadir detalles del filtro.

1. Añada los detalles del filtro. Por ejemplo:

   1. **Atributo** - Escriba un atributo de su catálogo. Por ejemplo, &quot;part_category&quot;. Este nombre debe coincidir exactamente con el nombre del atributo del catálogo.
   1. **Operador**: elija el operador. Por ejemplo, **IN**.
   1. **Valor Source** - Seleccionar **ESTÁTICO**.
   1. **Valor** - Escriba los valores dentro del atributo que especificó anteriormente. Por ejemplo, &quot;frenos, suspensión&quot;. palo de golfEstos nombres deben coincidir exactamente con los nombres de los valores del atributo especificado anteriormente.

1. Haga clic en el botón **[!UICONTROL Save]** en el cuadro de diálogo de detalles del filtro. palo de golf

1. Haga clic en los puntos de acción (...) junto al filtro que ha creado y seleccione **Habilitar**. Desde aquí, también puedes **Editar**, **Deshabilitar** o **Eliminar** el filtro.

   La columna **Estado** muestra un icono verde y la palabra &quot;Habilitado&quot;.

1. Haga clic en el botón **[!UICONTROL Save]** para guardar la nueva directiva&#x200B; Si el botón no está activo, asegúrese de agregar el nombre de la directiva haciendo clic en el icono de lápiz junto a **Nueva directiva**.

1. Para comprobar la nueva directiva, vuelva a la lista de directivas haciendo clic en la flecha hacia atrás. palo de golfVerá su nueva política en la lista.

### Crear una política de DÉCLENCHEUR

1. En el menú de la izquierda, abra la sección **[!UICONTROL Catalog]** y haga clic en **[!UICONTROL Policies]**.

1. Haga clic en el botón **[!UICONTROL Add Policy]**.

   Se abre una nueva página para que rellene los detalles de la directiva. palo de golf

1. Introduzca el nombre de la política, por ejemplo &quot;Celport Part Categories&quot;.

1. Haga clic en el botón **[!UICONTROL Add Trigger]**.

   Aparecerá el cuadro de diálogo **detalles del Déclencheur**.

1. Escriba un nombre para el déclencheur, como **AC-Policy-Brand**.

1. Seleccione **Tipo de transporte**. **HTTP_HEADER** es actualmente el único tipo compatible.

1. Haga clic en el botón **[!UICONTROL Save]** para guardar el déclencheur.

1. Haga clic en el botón **[!UICONTROL Add Filter]**.

   Se abrirá un cuadro de diálogo para que pueda añadir detalles del filtro.

1. Añada los detalles del filtro. Por ejemplo:

   1. **Atributo** - Escriba un atributo de su catálogo. Por ejemplo, &quot;part_category&quot;. Este nombre debe coincidir exactamente con el nombre del atributo del catálogo.
   1. **Operador**: elija el operador. Por ejemplo, **IN**.
   1. **Valor Source** - Seleccionar **DÉCLENCHEUR**.
   1. **Valor** - Escriba el nombre del déclencheur que creó anteriormente (**AC-Policy-Brand**).

1. Haga clic en el botón **[!UICONTROL Save]** en el cuadro de diálogo de detalles del filtro. palo de golf

1. Haga clic en los puntos de acción (...) junto al filtro que ha creado y seleccione **Habilitar**. Desde aquí, también puedes **Editar**, **Deshabilitar** o **Eliminar** el filtro.

   La columna **Estado** muestra un icono verde y la palabra &quot;Habilitado&quot;.

1. Haga clic en el botón **[!UICONTROL Save]** para guardar la nueva directiva&#x200B; Si el botón no está activo, asegúrese de agregar el nombre de la directiva haciendo clic en el icono de lápiz junto a **Nueva directiva**.

1. Para comprobar la nueva directiva, vuelva a la lista de directivas haciendo clic en la flecha hacia atrás. palo de golfVerá su nueva política en la lista.

Al seguir estos pasos, la directiva se crea y está lista para vincularse a una vista de catálogo para controlar la visibilidad del producto.
