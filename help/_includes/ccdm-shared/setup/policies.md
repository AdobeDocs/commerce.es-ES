---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%
---
Las directivas definen los filtros que se aplican a los productos en una vista de catálogo. Ayudan a adaptar el surtido de productos que se devuelve a una tienda o canal. Esto garantiza que el contenido correcto se envíe al destino correcto. Por ejemplo, tiendas físicas, mercados y canales publicitarios como Google, Facebook e Instagram.

Las directivas utilizan atributos de producto como marca, modelo o categoría de artículo para adaptar los datos del catálogo a los requisitos empresariales. &#x200B;

## Acceso al espacio de trabajo Políticas

La forma de abrir el área de trabajo *Políticas* depende del producto que utilice:

- **Administrador De Adobe Commerce** (Adobe Commerce as a Cloud Service)—Seleccione *Catálogo* > **Políticas**.
- **Adobe Commerce Optimizer Studio**—Seleccione *Configuración de tienda* > **Directivas**.

## Filtros

Los filtros definen condiciones basadas en atributos que determinan qué productos coinciden con una directiva. Cuando se asocia con una vista de catálogo, una directiva ayuda a adaptar los productos devueltos para esa vista. Utilice atributos de producto, operadores y valores para definir las condiciones de coincidencia.

### Partes de un filtro

Un filtro consta de las siguientes partes:

| Parte | Descripción | Ejemplo |
|---|---|---|
| **Atributo** | Atributo de producto utilizado para el filtrado. | `part_category` |
| **Operador** | La condición aplicada al atributo. | `IN`, `EQUALS`, `CONTAINS` |
| **Origen del valor** | Especifica si los valores son `STATIC` o `TRIGGER`. | `STATIC` [Más información](#value-source-types) |
| **Valor** | Los valores específicos que cumplen la condición. | `brakes, suspension` |

### Ejemplo

Un filtro en `part_category` que usa el operador `IN` con los valores `brakes` y `suspension` coincide con productos cuyo `part_category` es un valor.

### Tipos de origen de valor

Existen dos tipos de orígenes de valores: **STATIC** y **DÉCLENCHEUR**.

Las directivas con un **origen Value** de **STATIC** se consideran directivas universales. Las políticas universales definen la experiencia de un sitio web en su conjunto. Esto significa que la vista de catálogo siempre ejecuta esa directiva. La ejecución de la directiva no depende de la interacción del usuario de la tienda.

Las directivas con un **origen de valor** de **DÉCLENCHEUR** se denominan directivas exclusivas. Esto significa que la vista de catálogo ejecuta esa directiva únicamente cuando el déclencheur se especifica en el encabezado de la llamada de API. En la tienda, esto significa que la información se muestra en función de lo que seleccione el comprador. Por ejemplo, en la siguiente imagen, hay dos menús desplegables: **Marca** y **Modelo**.

![origen de valor de Déclencheur en tienda](/help/assets/ccdm-shared/setup/policy-trigger.png)

**Marca** y **Modelo** son déclencheur definidos:

- `AC-Policy-Brand`
- `AC-Policy-Model`

Si el comprador hace clic en la lista desplegable Modelo, el encabezado de la llamada de API contiene `AC-Policy-Model`, que está configurado para mostrar solo los productos específicos de la directiva `AC-Policy-Model`.

### Déclencheur de encabezado HTTP de varios valores {#multi-value-http-header-triggers}

Una directiva de déclencheur que use el tipo de transporte `HTTP_HEADER` puede recibir varios valores en un solo encabezado. Los valores deben separarse con comas y el operador de filtro debe ser `IN`. Cada valor se trata como una coincidencia aceptable. Los valores se evalúan con `OR` semántica.

Por ejemplo, un filtro de directiva que usa `IN` con el siguiente encabezado:

```
AC-Policy-Vehicle: UNIVERSAL,veh-bolt-mammoth-limited-2025
```

coincide con productos cuyo atributo `vehicle` es `UNIVERSAL` o `veh-bolt-mammoth-limited-2025`.

Mientras que un operador de filtro de `EQUALS`, `GREATER_THAN_EQUAL` o `LESS_THAN_EQUAL` se rechaza con un error de validación.

#### Notas de sintaxis

- El nombre del encabezado coincide con el nombre del déclencheur que configuró, por ejemplo `AC-Policy-Vehicle`.
- Las comas separan los valores individuales dentro del encabezado. Si el mismo encabezado `AC-Policy-_Name_` aparece más de una vez, sus valores se combinan en un único valor de encabezado separado por comas
- El operador de filtro es `IN`.
- Un filtro de directiva con **origen de valor** establecido en `TRIGGER`.
- Un déclencheur cuyo **tipo de transporte** es `HTTP_HEADER`.

## Crear política

En esta sección, se crea una directiva nueva. La directiva puede ser **STATIC** o **DÉCLENCHEUR**.

### Crear una política STATIC

1. En el área de trabajo **[!UICONTROL Policies]**, haga clic en el botón **[!UICONTROL Add Policy]**.

   Se abre una nueva página para que rellene los detalles de la directiva. &#x200B;

1. Introduzca el nombre de la política, por ejemplo &quot;Celport Part Categories&quot;.

1. Haga clic en el botón **[!UICONTROL Add Filter]**.

   Se abrirá un cuadro de diálogo para que pueda añadir detalles del filtro.

1. Añada los detalles del filtro. Por ejemplo:

   1. **Atributo** - Escriba un atributo de su catálogo. Por ejemplo, &quot;part_category&quot;. Este nombre debe coincidir exactamente con el nombre del atributo del catálogo.
   1. **Operador**: elija el operador. Por ejemplo, **IN**. &#x200B;
   1. **Valor Source** - Seleccionar **ESTÁTICO**. &#x200B;
   1. **Valor**: escriba un valor de la definición de atributo que especificó anteriormente. Por ejemplo, introduzca &quot;frenos&quot; para crear un filtro para las piezas de freno.
   1. Para guardar el valor, presione **Intro**.

      Si la directiva está diseñada para filtrar por varios valores, introduzca cada valor por separado.

1. Haga clic en el botón **[!UICONTROL Save]** en el cuadro de diálogo de detalles del filtro. &#x200B;

1. Haga clic en el icono de menú (...) junto al filtro que creó y seleccione **Habilitar**. Desde aquí, también puedes **Editar**, **Deshabilitar** o **Eliminar** el filtro.

   La columna **Estado** muestra un icono verde y la palabra &quot;Habilitado&quot;.

1. Haga clic en el botón **[!UICONTROL Save]** para guardar la nueva directiva.&#x200B; Si el botón no está activo, asegúrese de agregar el nombre de la directiva haciendo clic en el icono de lápiz situado junto a **Nueva directiva**.

1. Para comprobar la nueva directiva, haga clic en la flecha hacia atrás para volver al área de trabajo **[!UICONTROL Policies]**.

### Crear una política de DÉCLENCHEUR

1. En el área de trabajo **[!UICONTROL Policies]**, haga clic en el botón **[!UICONTROL Add Policy]**.

   Se abre una nueva página para que rellene los detalles de la directiva. &#x200B;

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
   1. **Operador**: elija el operador. Por ejemplo, **IN**. &#x200B;
   1. **Valor Source** - Seleccionar **DÉCLENCHEUR**. &#x200B;
   1. **Valor** - Escriba el nombre del déclencheur que creó anteriormente (**AC-Policy-Brand**).

   En el momento de la configuración, el filtro hace referencia al déclencheur configurado. En tiempo de ejecución, el encabezado de la solicitud de API proporciona el valor o los valores evaluados por ese filtro.

1. Haga clic en el botón **[!UICONTROL Save]** en el cuadro de diálogo de detalles del filtro. &#x200B;

1. Haga clic en el icono de menú (...) junto al filtro que creó y seleccione **Habilitar**. Desde aquí, también puedes **Editar**, **Deshabilitar** o **Eliminar** el filtro.

   La columna **Estado** muestra un icono verde y la palabra &quot;Habilitado&quot;.

1. Haga clic en el botón **[!UICONTROL Save]** para guardar la nueva directiva.&#x200B; Si el botón no está activo, asegúrese de agregar el nombre de la directiva haciendo clic en el icono de lápiz situado junto a **Nueva directiva**.

1. Para comprobar la nueva directiva, haga clic en la flecha hacia atrás para volver al área de trabajo **[!UICONTROL Policies]**.

Siguiendo estos pasos se crea la directiva que luego se puede vincular a una vista de catálogo para controlar la visibilidad del producto.
