---
title: Editar recomendación
description: Obtenga información sobre cómo editar una recomendación de producto.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# Editar recomendación

La página Editar recomendación permite ajustar la configuración individual que compone la recomendación. Todos los ajustes se pueden editar excepto el tipo de página y el tipo de recomendación. Se pueden editar las siguientes opciones de configuración:

- [Nombre de recomendación](#name)
- [Etiqueta de tienda](#label)
- [Número de productos](#number)
- [Ubicación y posición](#placement)
- [Filtrar productos](#filters)

La vista previa en la parte derecha de la página muestra cómo puede aparecer la recomendación con la configuración actual en la tienda. La _vista previa de productos recomendados_ permanece visible como referencia al desplazarse hacia abajo en la página. La vista previa muestra una imagen en miniatura del producto, el nombre del producto, el SKU, el precio y el tipo de resultado de cada producto devuelto. El tipo de resultado indica si hay suficientes datos de comportamiento primarios para generar la recomendación o si está utilizando datos de comportamiento de copia de seguridad.

![Editar recomendaciones](assets/edit-recommendation.png)

## Editar una recomendación

1. En la barra lateral de _Admin_, vaya a **Marketing** > _Promociones_ > **Recomendaciones de productos**.

1. Seleccione la recomendación que desee editar.

1. Haga clic en **Editar**. A continuación, siga las instrucciones que se indican a continuación para realizar los cambios que necesite.

1. Una vez finalizado, haga clic en **Guardar cambios**.

### Nombre de recomendación {#name}

Elija un nombre descriptivo que indique el propósito de la recomendación. El nombre es para referencia interna y no aparece en la tienda.

![Editar nombre](assets/edit-name.png)

### Etiqueta de tienda {#label}

Escriba el texto que desee usar como etiqueta para la unidad de recomendación en la tienda.

![Editar etiqueta](assets/edit-storefront-label.png)

### Número de productos {#number}

Ajuste el control deslizante para mostrar hasta 20 productos en la unidad de recomendación.

![Editar número de productos](assets/edit-number-of-products.png)

### Ubicación y posición {#placement}

1. Elija la ubicación de la página donde aparecerá la unidad de recomendación en la tienda.

   - Al final del contenido principal
   - Al principio del contenido principal

   ![Editar ubicación](assets/edit-placement.png)

1. Para cambiar el orden de las recomendaciones que se incluyen en la unidad, use el control **Mover** ![Selector de movimiento](assets/icon-move.png) para arrastrar las recomendaciones a su posición.

   ![Editar posición](assets/edit-position.png)

### Filtrar productos {#filters}

Cualquier cambio realizado en los [filtros](filters.md) del producto se reflejará en la _vista previa de los productos recomendados_. Solo se permite recomendar productos que coincidan con los filtros de inclusión. No se recomiendan los productos que coinciden con cualquier filtro de exclusión.

Las fichas _Inclusiones_ y _Exclusiones_ enumeran los filtros disponibles de cada tipo. En la lista, cada filtro activo se marca con un punto azul.

- Para mostrar los detalles de cada filtro, haga clic en su nombre.
- Para cambiar el estado del filtro, establezca la opción **Habilitar filtro** en la posición `on` o `off`.

![Editar filtros](assets/edit-filters.png)

La configuración del filtro describe los productos que se van a incluir o excluir en la unidad de recomendación. Por ejemplo, la configuración de inclusión de filtros de _Categoría_ indica al sistema que incluya solo los productos de las categorías seleccionadas.

![Editar filtro de categoría](assets/edit-filter-category.png)
