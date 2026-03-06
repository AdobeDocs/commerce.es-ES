---
title: Workspace de reglas de comercialización
description: Obtenga información sobre el espacio de trabajo Reglas de comercialización.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
exl-id: 3deac529-731d-44b9-87f3-3c9cb36e28e7
source-git-commit: 9cb231055df45bbfcff3303c6e1c257c883cb852
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 0%

---

# Workspace de reglas de comercialización

El área de trabajo *Reglas de comercialización* enumera la selección actual de reglas y su estado, y proporciona acceso a las herramientas que necesita para crear y administrar reglas. Puede asignar el ámbito de las reglas a todas las [vistas de catálogo](../../setup/catalog-view.md) (globales) o a una sola vista de catálogo. Consulte [Seleccionar vista de catálogo](#select-catalog-view) para ver cómo filtrar por vista de catálogo y crear reglas por vista de catálogo. Desde el espacio de trabajo puede:

- Buscar reglas
- Ver detalles de la regla
- Activar/desactivar reglas
- Eliminar reglas
- Acceso al editor de reglas

![Workspace de reglas de comercialización](../../assets/rules-workspace.png)

## Mostrar u ocultar columnas

1. En la esquina superior derecha, haga clic en **Mostrar/ocultar** ![Selector de columna](../../assets/btn-show-hide-columns.png) columnas.

1. En el menú, realice una de las acciones siguientes:

   - Para mostrar una columna oculta, haga clic en cualquier nombre de columna sin marca de verificación.
   - Para ocultar una columna visible, haga clic en cualquier nombre de columna con una marca de verificación.

## Filtrado de reglas por estado

1. Si la tienda tiene muchas reglas, puede filtrarlas por estado para acortar la lista. De forma predeterminada, la lista Reglas muestra todas las reglas.

1. Para enumerar sólo las reglas con una configuración de estado específica, establezca **Estado** en uno de los siguientes:

   - Todo
   - Activo
   - Inactivo
   - Programado
   - Borrador

   También puede filtrar por **Condiciones**, **Fecha de inicio**, **Fecha de finalización** y **Última actualización**.

## Ver detalles

El panel de detalles muestra el nombre de la regla, el estado, las condiciones y los eventos, la fecha de inicio y finalización, la descripción y la fecha de la última edición. Las reglas se pueden habilitar, editar y eliminar desde el panel de detalles.

1. En el área de trabajo *Reglas de comercialización*, busque la regla en la cuadrícula que desee ver y haga clic en el icono (![Selector de más](../../assets/btn-more.png)).

   Puede realizar cualquiera de las siguientes acciones desde el menú:

   - Editar regla
   - Eliminar regla
   - Activar/Desactivar regla

## Descripciones de columna

| Columna | Descripción |
|--- |--- |
| Nombre | Nombre de la regla. |
| Última actualización | La fecha en la que se actualizó la regla por última vez. |
| Fecha de inicio | La fecha de inicio de una regla programada. |
| Fecha de finalización | La fecha de finalización de una regla programada. |
| Estado | El estado codificado por colores indica el estado actual de la regla. Utilice el control Estado situado encima de la cuadrícula para filtrar las reglas por estado. Valores:<br />Todos los estados: muestra todas las reglas independientemente del estado.<br />Activo (azul): solo muestra las reglas activas.<br />Programado (naranja): solo muestra las reglas programadas.<br />Inactivo (gris): solo muestra las reglas inactivas. |

## Controles

| Control | Descripción |
|--- |--- |
| Añadir regla | Abre el [editor de reglas](add.md). |
| Vista de catálogo | Filtra la tabla a las reglas que se aplican a la vista de catálogo seleccionada. También establece el ámbito cuando [crea una regla](add.md). Opciones: *Todas las vistas* o una [vista de catálogo](../../setup/catalog-view.md) específica. Ver [Seleccionar vista de catálogo](#select-catalog-view). |
| Estado | Filtra la lista de reglas por estado. Opciones: Todo, Activo, Inactivo, Programado |
| ![Selector de columna](../../assets/btn-show-hide-columns.png) | Especifica las columnas visibles en la cuadrícula. Opciones: Última actualización, Fecha de inicio, Fecha de finalización, Estado |
| Buscar | Busca una regla por nombre completo o coincidencia parcial. |
| ![Selector de más](../../assets/btn-more.png) | Muestra un menú de más acciones que se pueden aplicar a la regla seleccionada. Opciones: Editar, Ver detalles, Eliminar |

## Detalles de regla

| Campo | Descripción |
|--- |--- |
| Estado | El estado actual de la regla. |
| Condiciones | La consulta de búsqueda que describe las condiciones asociadas con la regla. |
| Fecha de inicio | La fecha en la que la regla entra en vigor, si está programada. |
| Fecha de finalización | La fecha en la que caduca la regla, si está programada. |
| Descripción | Breve descripción de la regla. |
| Última actualización | La fecha y la hora de la última actualización de la regla. |
| Habilitado | Control que cambia el estado de la regla. Opciones: Habilitado / Deshabilitado |

## Seleccionar vista de catálogo

>[!IMPORTANT]
>
>Esta función se encuentra actualmente en fase beta.

El selector **[!UICONTROL Catalog view]** de la página Reglas de comercialización hace dos cosas:

1. **Filtra la tabla**: muestra solo las reglas (y sus detalles) que se aplican a la vista de catálogo seleccionada.
1. **Establece el ámbito de las nuevas reglas**: cuando [crea una regla](add.md), la vista de catálogo seleccionada se usa como ámbito de la regla. Las opciones son *Todas las vistas* o una [vista de catálogo](../../setup/catalog-view.md) específica.

   - **Todas las vistas** - La regla se aplica a todas las vistas del catálogo. El comportamiento de búsqueda y clasificación es el mismo en todas las tiendas que usan el catálogo.
   - **Vista de catálogo**: la regla se aplica solamente a la vista de catálogo seleccionada (por ejemplo, una tienda, región, concesionario o marca). Utilícelo cuando las distintas vistas de catálogo necesiten lógicas de comercialización diferentes.

Para obtener más información sobre cómo crear una regla y establecer su ámbito, consulte [Crear y administrar reglas](add.md).

### ¿Por qué crear una regla por vista de catálogo?

Cree reglas por vista de catálogo cuando diferentes tiendas, regiones o marcas necesiten un comportamiento diferente de búsqueda y clasificación. Ejemplos:

- **Redes de distribuidores o distribuidores**: cada distribuidor tiene su propia vista de catálogo; quiere diferentes productos anclados, ampliados o enterrados por distribuidor.
- **Varias regiones**: vistas de catálogo por separado para la UE, EE. UU. u otras regiones con reglas de comercialización específicas de la región.
- **Varias marcas**: cada marca tiene su propia vista de catálogo y usted desea reglas específicas de la marca (por ejemplo, diferentes productos promocionados o de clasificación predeterminada por cada marca).

Los datos de comportamiento que alimentan la [clasificación inteligente](add.md#intelligent-ranking) (como los más vistos, los más comprados y las tendencias) se calculan por vista de catálogo de forma predeterminada. Por lo tanto, las reglas que utilizan la clasificación inteligente reflejan el comportamiento del comprador en la vista de catálogo. Cuando su cuenta tiene un gran número de vistas de catálogo, el sistema puede acumular datos de comportamiento globalmente para mantener el rendimiento; en ese caso, la clasificación puede verse más afectada por las vistas de catálogo de alto tráfico, y la relevancia para las vistas de poco tráfico puede reducirse. Consulte [Límites y límites](../../boundaries-limits.md) para conocer los límites actuales.

### Configuración de una regla por vista de catálogo

1. En el área de trabajo *Reglas de comercialización*, use la lista desplegable **[!UICONTROL Catalog view]** para seleccionar la vista de catálogo donde se debe aplicar la regla.
1. Haga clic en **[!UICONTROL Create rule]**.

   La regla que cree se aplicará a la vista de catálogo seleccionada.
1. Genere la regla en el [editor de reglas](add.md).

   En el editor, defina las condiciones, los eventos y los detalles. La regla solo se aplica a los resultados de búsqueda en esa vista de catálogo.

Una vez creada una regla, no se puede cambiar la vista de catálogo (ámbito). Para aplicar una lógica similar a otra vista de catálogo, cree una nueva regla y seleccione esa vista de catálogo antes de crear.
