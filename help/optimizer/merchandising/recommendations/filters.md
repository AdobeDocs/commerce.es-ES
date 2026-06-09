---
title: Filtros de recomendación
description: Aprenda a utilizar filtros para controlar qué productos aparecen en  [!DNL Adobe Commerce Optimizer] recomendaciones.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
exl-id: f6100538-23c0-4e90-9834-a895d4707282
TQID: https://experienceleague.adobe.com/-pmVrAgEsSkn66K00-eaoQ4TF-7Xyxuwlniip1cR4HM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 116d8bd804df364ddc9cb1175525f08fd32c01bf
workflow-type: tm+mt
source-wordcount: 1919
ht-degree: 0%

---

# Filtrar productos

[!DNL Adobe Commerce Optimizer] aplica automáticamente filtros predeterminados no configurables a las unidades de recomendación. Si tiene varias unidades de recomendación implementadas en una página, [!DNL Adobe Commerce Optimizer] filtra los productos que se repiten en las unidades. Solo se usa la primera referencia a un producto repetido, para dejar espacio a otros productos que se recomienden. [!DNL Adobe Commerce Optimizer] también filtra los productos comprados anteriormente y los que están en el carro de compras.

Cuando [crea](create.md) una unidad de recomendación, puede definir filtros que controlen qué productos se pueden mostrar en las recomendaciones. Estos filtros se basan en un conjunto de condiciones de inclusión o exclusión que usted defina. En las recomendaciones solo aparecen los productos que cumplen todas las condiciones de inclusión. No se recomiendan los productos que coinciden con cualquiera de las condiciones de exclusión.

Puede configurar varios filtros y habilitar solo los que desee seleccionando la opción en cada página de filtro. Esto le permite crear borradores de filtros para su uso futuro. El número de filtros habilitados se muestra en cada pestaña.

## Condiciones

Las condiciones pueden ser estáticas o dinámicas.

- Una condición estática utiliza atributos de producto existentes para determinar qué productos pueden aparecer en la unidad. Por ejemplo, puede especificar que solo aparezcan en la unidad los productos en existencias con un precio mayor que 25 $.

- Una condición dinámica elimina el contexto actual de un comprador, como la categoría o el producto que se está viendo en ese momento. Por ejemplo, al crear una recomendación de producto para implementarla en páginas de detalles de producto, puede usar un [filtro de precio dinámico](#dynamic-price-filters-relative-to-current-product) para incluir o excluir productos dentro de un rango de precios relativo del producto visualizado actualmente.

### Operadores lógicos

Los operadores lógicos `AND` y `OR` se utilizan para unir varias condiciones. Si utiliza filtros de inclusión y exclusión en distintos tipos de filtros, las inclusiones se evalúan primero para determinar todos los productos posibles que se pueden recomendar y, a continuación, se eliminan de la lista los productos que coinciden con cualquier filtro de exclusión. Los filtros de **Price** usan un orden diferente entre las reglas de precios: primero las exclusiones, luego las inclusiones. Ver [Cómo incluir y excluir reglas que utilizan price](#how-include-and-exclude-rules-use-price).

- `AND` - Une dos condiciones de filtrado de inclusión
- `OR` - Une dos condiciones de filtrado de exclusión

## Tipos de filtros

Cada tipo de filtro se dirige a un aspecto diferente del catálogo, como el producto y el precio, para que pueda reducir o ampliar qué productos son aptos para una unidad. Elija los tipos que coincidan con sus objetivos de comercialización y, a continuación, combine las condiciones de inclusión y exclusión según sea necesario; las subsecciones siguientes describen cómo se comporta cada tipo y cómo lo aplica [!DNL Adobe Commerce Optimizer].

>[!NOTE]
>
>Solo se pueden recomendar los productos que coincidan con los filtros de **inclusión** y se eliminará cualquier producto que coincida con un filtro de **exclusión**.

### Precio {#price}

>[!IMPORTANT]
>
>El filtrado de precios está en versión beta.

El filtrado de precios usa el **precio calculado final** de cada producto del **libro de precios activo** de la tienda, que es el libro de precios asignado a la tienda donde se representa la unidad de recomendación.

Ese valor:

- **Incluye** descuentos, promociones y precios especiales definidos en ese libro de precios (no solo el precio de lista).
- **Excluye** ajustes de nivel de carro y envío.
- **Sólo se aplica** al libro de precios activo de esa tienda; no se usan otras tiendas ni libros de precios.

Configure cómo se asignan los libros de precios a una tienda del catálogo y la configuración de [libros de precios](../../setup/pricebooks.md).

#### Cómo se incluyen y excluyen las reglas para utilizar el precio {#how-include-and-exclude-rules-use-price}

- **Reglas de exclusión**: los productos cuyo precio final **coincide con cualquier** exclusión de precios definida se eliminan primero.
- **Reglas de inclusión**: entre los demás candidatos, solo los productos cuyo precio final **coincida con todas** las condiciones de inclusión de precios definidas siguen siendo elegibles. Esto incluye todos los filtros de inclusión habilitados (por ejemplo, la regla de precio más cualquier otra regla de inclusión).

Las reglas de precios **filtran** el conjunto de candidatos de recomendación; no **no** vuelven a clasificar productos. El motor genera una lista clasificada, las reglas de inclusión y exclusión de precios eliminan los productos de esa lista y el orden relativo de los productos restantes permanece igual. Si se clasifican menos productos que las solicitudes de unidad, solo se muestran los artículos válidos. Si no cumple los requisitos, la unidad no se procesa (no hay marcador de posición vacío).

El precio que se muestra en los productos dentro de la unidad de recomendación es el mismo **precio final** del libro de precios de esa tienda, por lo que lo que los compradores ven coincide con el valor utilizado para el filtrado. En la vista previa del administrador, los productos configurables pueden mostrar un rango de precios cuando los precios de variante difieren; consulte [Productos configurables en la vista previa](#configurable-products-in-preview).

#### Intervalo de precios estático

Use un filtro de precio **estático** cuando quiera un precio mínimo o máximo fijo en la moneda base de su tienda, independientemente del producto que esté viendo un comprador.

##### Configuración de un filtro de precios estático

1. Mientras [crea o edita](create.md) una unidad de recomendación, abra **[!UICONTROL Filter products]** (o vaya al paso _Filtros_ del flujo de trabajo de la unidad).
1. Seleccione la ficha **[!UICONTROL Inclusions]** o **[!UICONTROL Exclusions]**, en función de si desea permitir sólo los productos de un intervalo de precios o bloquear los productos de un intervalo. El distintivo de cada pestaña muestra cuántos filtros de ese tipo están habilitados.
1. En la lista de la izquierda, seleccione **[!UICONTROL Price]**.
1. Activar **[!UICONTROL Enable filter]**.

   Los valores de precio utilizan la **moneda base del sitio web**, como se indica en la página.

1. Abra **[!UICONTROL Include products based on]** (en la ficha **[!UICONTROL Inclusions]**) o el control equivalente de la ficha **[!UICONTROL Exclusions]** y elija **[!UICONTROL Set price range]**.
1. Establezca un(a) **[!UICONTROL Min price]** y/o **[!UICONTROL Max price]** opcional(a) utilizando los campos junto al símbolo de moneda. Puede escribir cantidades o utilizar los controles **-** y **+** para ajustar los valores. Deje un límite vacío si no necesita un mínimo o un máximo. La gama se compara con el precio calculado final de cada producto para el libro de precios activo de la tienda.
1. Termine de configurar la unidad de recomendación y guarde o publique como lo haría normalmente para que el filtro surta efecto.

![Filtro de precio](../../assets/filter-price.png)

#### Filtros de precios dinámicos (en relación con el producto actual) {#dynamic-price-filters-relative-to-current-product}

Use un filtro de precio **dinámico** cuando las recomendaciones deban limitarse en relación con el **producto visualizado actualmente** en una página de detalles del producto (PDP). El filtro usa el precio final de ese producto como **anclaje** y compara los productos recomendados con los límites definidos.

Los operadores dinámicos solo están disponibles para [tipos de recomendaciones relacionadas con SKU](types.md) que se ejecutan en un contexto de producto, como:

- Vio esto, vio aquello.
- Vio esto, compró aquello.
- Compré esto, compré aquello.
- Más parecido a esto
- Similitud visual

Están **no** disponibles para los tipos basados en popularidad (por ejemplo, **Más visitados** o **Más comprados**) porque esas unidades no tienen un solo producto actual para anclar el filtro.

En la tienda, la lista desplegable de recomendaciones lee el precio del producto actual del contexto de PDP y lo envía con la solicitud de recomendación. [!DNL Adobe Commerce Optimizer] utiliza ese valor como anclaje al evaluar reglas de precios dinámicas. Para los productos configurables, el anclaje es la **variante más baja** del precio final (`priceRange.minimum`).

##### Operadores

En **[!UICONTROL Include products based on]** (o las exclusiones equivalentes), puede elegir:

| Operador | Finalidad |
| --- | --- |
| **Menor o igual que el precio actual del producto** | Incluya o excluya productos en un límite o por debajo de este derivado del precio de anclaje más un desplazamiento. |
| **Precio de producto actual mayor o igual que** | Incluya o excluya productos en un límite o por encima de este derivado del precio de anclaje más un desplazamiento. |
| **Dentro de un intervalo de valores del producto actual** | Incluya o excluya productos cuyo precio final se encuentre dentro de una banda de moneda fija alrededor del anclaje (desplazamientos respecto al precio actual). |
| **Dentro de un intervalo porcentual del producto actual** | Incluya o excluya productos cuyo precio final esté dentro de una banda porcentual alrededor del anclaje. |

##### Semántica de desplazamiento

Para **Menor o igual que el precio actual del producto** y **Mayor o igual que el precio actual del producto**, el valor que introduce es un **desplazamiento numérico agregado al precio de anclaje** para formar el límite:

- Un desplazamiento **negativo** mueve el límite **por debajo** del precio actual del producto.
- Un desplazamiento **positivo** mueve el límite **por encima** del precio actual del producto.
- **Vacío** o **0** significa **sin límite** en ese lado; el backend los trata igual.
- No se puede usar **0** para que signifique &quot;exactamente el precio del producto actual&quot; como límite.

Esto coincide con [!DNL Product Recommendations] en PaaS. Las etiquetas del Administrador reflejan esta semántica directamente.

##### Configuración de un filtro de precios dinámico

1. [Cree o edite](create.md) una unidad de recomendación **relacionada con SKU** que esté implementada en la página de **detalles del producto** (o en otra ubicación donde un producto actual siempre esté en contexto).
1. Abra **[!UICONTROL Filter products]** y seleccione la ficha **[!UICONTROL Inclusions]** o **[!UICONTROL Exclusions]**.
1. Seleccione **[!UICONTROL Price]** y active **[!UICONTROL Enable filter]**.
1. Abra **[!UICONTROL Include products based on]** (o las exclusiones equivalentes) y elija un operador dinámico (por ejemplo, **Dentro de un intervalo de valores del producto actual**).
1. Introduzca desplazamientos o valores de rango cuando se le solicite. Utilice la vista previa para confirmar los resultados de un producto de ejemplo.
1. Guarde o publique la unidad.

Los valores no válidos (cantidades no numéricas, combinaciones no admitidas o intervalos en los que el mínimo es mayor que el máximo) se guardan y muestran errores de validación; **[!UICONTROL Save]** permanece deshabilitado hasta que el filtro sea válido.

##### Cuando no hay disponible un precio de anclaje

Si se habilita un filtro de precio dinámico pero la tienda no puede proporcionar un precio de producto actual (por ejemplo, la unidad se procesa fuera de un contexto de PDP), [!DNL Adobe Commerce Optimizer] no devuelve recomendaciones sin filtrar. La unidad muestra **ninguna recomendación**, ya que al mostrar resultados sin filtrar no coincidiría la regla que configuró.

##### Productos configurables en vista previa {#configurable-products-in-preview}

En el panel de administración **vista previa**, los precios de los productos recomendados se muestran de la siguiente manera:

- **Productos simples** - Precio final único de la respuesta de GraphQL.
- **Productos configurables**: si los precios de variante mínimos y máximos difieren, la vista previa muestra un intervalo (por ejemplo, `$min – $max`). Si son iguales, se muestra un solo precio.

El precio de anclaje utilizado para los cálculos de filtros dinámicos en un producto configurable es siempre el precio final de variante **mínimo**, coherente con la tienda.

#### Ejemplos de filtros de precios

Los siguientes ejemplos usan un precio de producto actual de **$500**. Ajuste la inclusión y la exclusión para que coincidan con su objetivo de comercialización.

| Operador | Ficha | Meta | Límite de ejemplo |
| --- | --- | --- | --- |
| Menor o igual que el precio actual del producto | Exclusiones | Fomente las ventas adicionales ocultando alternativas de menor precio | Excluir productos ≤ 500 $ |
| Menor o igual que el precio actual del producto | Inclusiones | Ofrecer alternativas económicas | Incluir productos ≤ 500 $ |
| Mayor o igual que el precio actual del producto | Exclusiones | Evite aumentar las ventas en un flujo centrado en el presupuesto | Excluir productos ≥ 500 $ |
| Mayor o igual que el precio actual del producto | Inclusiones | Alternativas Surface Premium | Incluir productos ≥ 500 $ |
| Dentro de una gama de valores del producto actual | Exclusiones | Diversificar para evitar puntos de precios similares | Excluir de 400 a 600 dólares |
| Dentro de una gama de valores del producto actual | Inclusiones | Mostrar alternativas comparables en una banda estrecha | Incluir $400-$600 |
| Dentro de un rango porcentual del producto actual | Exclusiones | Reduzca los artículos con precios similares (por ejemplo, ±20%) | Excluir aproximadamente $400-$600 |
| Dentro de un rango porcentual del producto actual | Inclusiones | Comparación equitativa dentro de una banda comparable | Incluye aproximadamente $400-$600 |

### Product

Los filtros de producto están destinados a elementos de catálogo individuales por **SKU**. Agrega una o más SKU para permitir solo esos productos (**Inclusiones**) o para bloquearlos (**Exclusiones**), con la misma página de **[!UICONTROL Filter products]** que [filtros de precio](#price). No puede mostrar productos deshabilitados ni productos que no sean visibles individualmente en una unidad de recomendación; esos productos nunca aparecen en la tienda, independientemente de los filtros.

#### Configuración de un filtro de producto

1. Mientras [crea o edita](create.md) una unidad de recomendación, abra **[!UICONTROL Filter products]** (o vaya al paso _Filtros_ del flujo de trabajo de la unidad).
1. Seleccione la ficha **[!UICONTROL Inclusions]** o **[!UICONTROL Exclusions]**. El distintivo de cada pestaña muestra cuántos filtros de ese tipo están habilitados.
1. En la lista de la izquierda, seleccione **[!UICONTROL Product]**.
1. Activar **[!UICONTROL Enable filter]**.

   El encabezado del panel derecho refleja la pestaña, por ejemplo **[!UICONTROL Product inclusions]** o el equivalente para las exclusiones.

1. En **[!UICONTROL Product SKU]**, escriba un SKU y haga clic en **[!UICONTROL Add]**. Repita el proceso para añadir más SKU.

   En **[!UICONTROL Product SKUs]**, cada SKU aparece como una etiqueta extraíble. Haz clic en **X** en una etiqueta para eliminar esa SKU, o haz clic en **[!UICONTROL Clear All]** para eliminar todas las SKU de la lista.

1. Termine de configurar la unidad de recomendación y guarde o publique como lo haría normalmente para que el filtro surta efecto.

Para **inclusiones**, solo se pueden recomendar productos cuyas SKU estén en la lista (y que cumplan con los otros filtros de inclusión habilitados). Para **exclusiones**, no se recomienda ningún producto cuya SKU se haya enumerado, aunque de lo contrario se clasificaría.

![Filtro de producto](../../assets/filter-product.png)

>[!NOTE]
>
>Los productos secundarios de un producto configurable no se muestran en una unidad de recomendación porque tienen la visibilidad de _No visible individualmente_.

<!--
### Attribute

You can filter products based on attribute criteria, including attribute values. Selected values use OR logic to either include or exclude products when any of the specified values are found.
-->
