---
title: '[!DNL Product Recommendations] Workspace'
description: Obtenga información sobre cómo configurar, administrar y supervisar el rendimiento de recomendaciones de productos.
exl-id: eaf1f0b2-9d9d-4069-8269-06f30166f788
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 0%

---

# [!DNL Product Recommendations] Workspace

El espacio de trabajo [!DNL Product Recommendations] muestra una lista de recomendaciones configuradas anteriormente con métricas que le ayudan a realizar un seguimiento del éxito de cada recomendación. La lista se puede configurar para calcular las métricas del último día, semana o mes. Puede utilizar las métricas para crear perspectivas procesables en función de la frecuencia con la que se ve o se hace clic en una unidad de recomendación, o para analizar el rendimiento de sus recomendaciones.

>[!INFO]
>
>Una unidad de recomendación es un widget que contiene el producto recomendado _items_.

![espacio de trabajo de Recommendations](assets/workspace.png)
_Workspace de Recommendations_

## Recopilación de datos

Para asegurarse de que cada área funcional del espacio de trabajo contiene los datos correctos, debe configurar la recopilación de datos en función de la implementación de tienda seleccionada:

1. Luma: la recopilación de datos está disponible de forma predeterminada.
1. Sin encabezado: la recopilación de datos debe configurarse manualmente, según la implementación de la tienda.

Si utiliza una tienda sin encabezado, consulte la siguiente documentación para obtener más información sobre los eventos necesarios que debe agregar:

- [Eventos requeridos](events.md) para el panel de recomendaciones de productos.
- [Recopilador de eventos de tienda](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/) que debe agregarse como requisito previo.
- [Ejemplos](https://github.com/adobe/commerce-events/tree/main/examples) de la estructura de eventos.

## Establecer el ámbito

Inicialmente, el [ámbito](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html) de toda la configuración de recomendaciones está establecido en `Default Store View`. Si la instalación de Commerce incluye varias vistas de tienda, establece **Scope** en la [vista de tienda](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) donde se aplican las recomendaciones.

## Definir intervalo de fechas de métricas

1. Haga clic en el control **Calendario** ![Selector de calendario](assets/icon-calendar.png).

1. Elija una de las siguientes opciones:

   - Últimas 24 horas
   - Últimos 7 días
   - Últimos 30 días

   Los valores calculados en las columnas de métricas cambian para reflejar el intervalo de fechas actual.

   >[!NOTE]
   >
   >Las métricas de Recomendación de producto están optimizadas para las tiendas de Luma. Si la tienda no está basada en Luma, el modo en que las métricas rastrean los datos depende de cómo [implemente la colección de eventos](events.md).

## Mostrar u ocultar columnas

1. En la esquina superior izquierda, haga clic en **Mostrar u ocultar** ![Columnas del selector de columnas](assets/icon-show-hide-columns.png).

   Las columnas visibles tienen una marca de verificación azul.

1. En el menú, realice una de las acciones siguientes:

   - Para mostrar una columna oculta, haga clic en cualquier nombre de columna sin marca de verificación.
   - Para ocultar una columna visible, haga clic en cualquier nombre de columna con una marca de verificación.

   La tabla se actualiza para incluir solo las columnas seleccionadas.

   ![espacio de trabajo de Recommendations](assets/workspace-select-columns.png)
   _Mostrar/ocultar columnas_

## Configuración

La configuración determina el espacio de datos SaaS que proporciona los datos de comportamiento de recomendación.

- Para cambiar la ubicación en la que se originan los datos de comportamiento de recomendación, elija un espacio de datos de SaaS diferente.

- Para configurar un nuevo espacio de datos SaaS, haga clic en **Editar configuración**. Para obtener más información, consulte [Configuración](settings.md).

![Configuración de recomendaciones](assets/settings.png)
_Configuración de recomendaciones_

## Ver detalles

1. En la tabla, haga clic en la recomendación que desee examinar.

   ![espacio de trabajo de Recommendations](assets/recommendation-detail.png)
   _Detalle de tasa de conversión de página de inicio_

1. Para cambiar el estado de la recomendación, haga clic en **Activar** o **Desactivar**.

## Editar recomendación

En la página de detalles de la recomendación, haga clic en **Editar**. Para obtener más información, ve a [Editar recomendaciones](edit.md).

## Crear recomendación

En la página de detalles de la recomendación, haga clic en **Crear**. Para obtener más información, ve a [Crear recomendaciones](create.md).

## Controles de Workspace

| Control | Descripción |
|---|---|
| ![Selector de calendario](assets/icon-calendar.png) | Determina el intervalo de tiempo que se utiliza para los cálculos de métricas. Opciones: 24 horas / 7 días / 30 días |
| ![Selector de columna](assets/icon-show-hide-columns.png) | Determina las columnas que aparecen en la tabla [!DNL Product Recommendations]. |
| Configuración | Determina el espacio de datos SaaS donde se recuperan los datos de comportamiento de recomendación y también habilita el tipo de recomendación de similitud visual. |
| Crear recomendación | Abre la página [Crear nueva recomendación](create.md). |

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
