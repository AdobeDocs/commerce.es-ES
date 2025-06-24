---
title: Workspace de reglas de comercialización
description: Obtenga información sobre el espacio de trabajo Reglas de comercialización.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 33a0903986cf581ece48616dad877db9516d9350
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---

# Workspace de reglas de comercialización

El área de trabajo *Reglas de comercialización* enumera la selección actual de reglas y su estado, y proporciona acceso a las herramientas que necesita para crear y administrar reglas. Desde el espacio de trabajo puede:

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
