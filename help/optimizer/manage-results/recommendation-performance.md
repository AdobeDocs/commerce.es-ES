---
title: Rendimiento de Recommendations
description: La página de rendimiento de Recommendations proporciona a insight información sobre el rendimiento de las recomendaciones de productos.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
exl-id: 1b77e2ea-412b-4c78-9d38-390bd8fda87e
source-git-commit: 9cb231055df45bbfcff3303c6e1c257c883cb852
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---

# Rendimiento de Recommendations

La página Rendimiento de las Recomendaciones muestra una lista de recomendaciones configuradas junto con métricas clave para ayudarle a evaluar su eficacia. Puede configurar la vista para que muestre las métricas del día, la semana o el mes pasados. Estas perspectivas muestran la frecuencia con la que se visualiza o se hace clic en cada unidad de recomendación, lo que le ayuda a evaluar el rendimiento e identificar oportunidades para la optimización.

>[!INFO]
>
>Una unidad de recomendación es un widget que contiene el producto recomendado _items_.

![Rendimiento de recomendaciones](../assets/rec-performance.png){zoomable="yes"}

## Ver un informe

1. Elija la **vista de catálogo**, como *Todas las vistas* donde se aplican las recomendaciones.

   Obtenga más información acerca de [vistas de catálogo](#select-catalog-view) en Recommendations.

1. Haga clic en **[!UICONTROL Date Range]** y seleccione uno de los siguientes intervalos:

   ![Intervalo de fechas de Recommendations](../assets/rec-perf-date-range.png)

   La tabla de recomendación se actualiza para mostrar las métricas de ese intervalo de fechas y la vista de catálogo.

## Personalizar tabla

1. En la esquina superior izquierda, haga clic en el icono ![Selector de columna](../assets/icon-show-hide-columns.png) para personalizar la tabla.

   Las columnas visibles tienen una marca de verificación.

1. En el menú, realice una de las acciones siguientes:

   - Para mostrar una columna oculta, haga clic en cualquier nombre de columna sin marca de verificación.
   - Para ocultar una columna visible, haga clic en cualquier nombre de columna con una marca de verificación.

   La tabla se actualiza para incluir solo las columnas seleccionadas.

## Ver detalles

1. En la tabla, haga clic en el icono (![Selector de más](../assets/btn-more.png)) que aparece junto a la recomendación que desea examinar.

1. Para cambiar el estado de la recomendación, haga clic en **Activar** o **Desactivar**.

## Crear o administrar recomendaciones

Aprenda a [crear una nueva recomendación o a administrar una existente](../merchandising/recommendations/create.md).

## Controles de Workspace

| Control | Descripción |
|---|---|
| ![Intervalo de fecha](../assets/rec-perf-date-range.png) | Determina el intervalo de tiempo que se utiliza para los cálculos de métricas. |
| ![Selector de columna](../assets/icon-show-hide-columns.png) | Determina las columnas que aparecen en la tabla Recommendations. |
| Crear recomendación | Abre la página [Crear nueva recomendación](../merchandising/recommendations/create.md). |
| [Vista de catálogo](#select-catalog-view) | Seleccione la vista de catálogo para filtrar la tabla y mostrar solo las recomendaciones que se aplican a la vista de catálogo seleccionada. Esta selección también se usa como vista de catálogo cuando [crea](../merchandising/recommendations/create.md) una nueva recomendación. Las opciones son *Todas las vistas* o una [vista de catálogo](../setup/catalog-view.md) específica. |

## Descripciones de columna

| Columna | Descripción |
|---|---|
| Nombre | El nombre de la recomendación. |
| Página | Página en la que aparece la recomendación. |
| Tipo | El tipo de recomendación. |
| Estado | El estado de la recomendación. Opciones: Inactivo/Activo/Borrador |
| Creado | La fecha en la que se creó la recomendación. |
| Última edición | Fecha en la que se editó la recomendación por última vez. |
| Impresiones | El número de veces que se carga y procesa una unidad de recomendación en una página. En la página se representa una unidad de recomendación que está por debajo del pliegue de la ventanilla del explorador, aunque el comprador no la vea. En este caso, la unidad procesada se cuenta como una impresión, pero una vista solo se cuenta si el comprador desplaza la unidad a la vista. |
| vImpresiones | (Impresiones visibles) El número de unidades de recomendación que registran al menos una vista. Por ejemplo, si la unidad de recomendación tiene dos líneas, cada una con dos productos, y el comprador no ve los dos últimos productos, pero los dos primeros sí, la actividad seguirá contando como una impresión. |
| Vistas | El número de unidades de recomendación que aparecen en la ventanilla móvil del explorador del comprador. Si el comprador desplaza la página hacia arriba o hacia abajo varias veces, el evento se activa varias veces, cada vez que se puede ver la unidad. |
| Clics | La suma del número de veces que un comprador hace clic en un artículo de la unidad de recomendación y el número de veces que el comprador hace clic en el botón **Agregar al carro** de la unidad de recomendación |
| Ingresos | Ingresos impulsados por la recomendación para el intervalo de tiempo actual. |
| Ingresos Lt | (Ingresos de por vida) Ingresos de por vida impulsados por una recomendación. |
| Visibilidad | Porcentaje de unidades de recomendación que se registran para la vista. |
| CTR | (Tasa de pulsaciones) El porcentaje de impresiones unitarias de la recomendación que registra un clic. CTR cuenta todas las impresiones, incluso si la unidad no entra en la vista del comprador. Si no se ve la unidad de recomendación, es poco probable que se haga clic en ella. Sin embargo, las impresiones invisibles se contabilizan en la puntuación de CTR y reducen el porcentaje de CTR general. |
| vCTR | (Tasa de clics visibles) mide los clics basados únicamente en impresiones visibles (recomendaciones que aparecieron en la parte visible de la pantalla del comprador), lo que proporciona una medición más precisa de la participación del comprador. |

## Seleccionar vista de catálogo

>[!IMPORTANT]
>
>Esta función se encuentra actualmente en fase beta.

El selector **[!UICONTROL Catalog view]** de la página **Recommendations** hace dos cosas:

1. **Filtra la tabla**: muestra solo las recomendaciones (y sus métricas) que se aplican a la vista de catálogo seleccionada.
1. **Establece el ámbito de las nuevas recomendaciones**: al [crear](../merchandising/recommendations/create.md) una recomendación, la vista de catálogo seleccionada se usa como ámbito de la unidad. Las opciones son *Todas las vistas* o una [vista de catálogo](../setup/catalog-view.md) específica.

   - **Todas las vistas**: la recomendación se aplica a todas las vistas del catálogo (la disponibilidad del producto sigue filtrándose por vista).
   - **Vista de catálogo**: la recomendación solo se aplica a la vista de catálogo seleccionada (por ejemplo, una tienda, un idioma o una marca).

Si especifica una vista de catálogo para cada recomendación, puede:

- Configure las recomendaciones para todas las vistas de catálogo (globales) o para una vista de catálogo.
- Previsualizar y filtrar productos por vista de catálogo en la página de recomendaciones [crear](../merchandising/recommendations/create.md).
- Mostrar solo los productos disponibles en cada tienda.
- Ver las métricas y el comportamiento de la tienda por vista de catálogo.

### Filtros de productos en la vista de catálogo

La disponibilidad del producto se aplica por vista de catálogo incluso para las unidades de recomendación en la selección de **Todas las vistas**. Esto funciona además de los [filtros de inclusión o exclusión](../merchandising/recommendations/filters.md) que establezca en la unidad de recomendación.

**Ejemplo: Recomendación con filtros de inclusión en la selección Todas las vistas**

- La recomendación de **Todas las vistas** incluye SKU: SKU_ABC, SKU_CDE, SKU_XYZ.
- **Vista de catálogo: Kingsbluff** no puede vender SKU_ABC o SKU_CDE. **Mostrado:** SKU_XYZ más cualquier otro SKU válido para Kingsbluff.
- **Vista de catálogo: Arkbridge** no puede vender ninguna de las SKU incluidas. **Mostrado:** solo SKU permitidas por Arkbridge. Si no hay ninguna disponible, la unidad de recomendación no aparece en esa tienda.
