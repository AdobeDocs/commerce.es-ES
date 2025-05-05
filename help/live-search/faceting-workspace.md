---
title: Faceting Workspace
description: Aprenda a utilizar el espacio de trabajo de  [!DNL Live Search] faceting.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Faceting Workspace

El área de trabajo *Faceting* enumera todas las facetas que están disponibles actualmente y proporciona acceso a las herramientas que necesita para configurar y administrar facetas. Las facetas ancladas aparecen primero en la lista de facetas existentes, seguidas de las facetas dinámicas. La lista se puede filtrar para mostrar todas las facetas o solo aquellas que estén ancladas o sean dinámicas.

![Espacio de trabajo de facetas](assets/faceting-workspace.png)

## Establecer el ámbito

Si la instalación de Adobe Commerce incluye varias vistas de tienda, establece **Scope** en la [vista de tienda](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=es#scope-settings) donde se aplique la configuración de faceta.

## Filtrado de la lista

1. Haga clic en el control **Filtrar por**.
1. Elija una de las siguientes opciones:

   * Todos los filtros
   * Anclado
   * Dinámico

## Añadir una faceta

1. Haga clic en **Agregar facetas**.
1. Consulte [Agregar facetas](facets-add.md) para obtener instrucciones detalladas.

## Descripciones de columna

| Columna | Descripción |
|--- |--- |
| (primera columna) | Enumera facetas fijas y dinámicas mediante la [etiqueta](facets-type.md) que es visible para el comprador. |
| Tipo de orden | El [orden](facets-type.md) de valores de faceta. Las facetas se ordenan alfabéticamente en todas las [!DNL Commerce] tiendas. Para implementaciones de [headless], las facetas se pueden ordenar alfabéticamente o por recuento. Opciones: Alfabético, Recuento (solo sin encabezado) |
| Valor máximo | El número de valores de faceta disponibles en la tienda como filtros, con un máximo de 10. |

## Controles

| Control | Descripción |
|--- |--- |
| Añadir facetas | Abre el [editor de facetas](facets-add.md). |
| Filtrar por | Determina el [tipo de facetas](facets-type.md) que aparecen en la lista. Opciones: Todo, Anclado, Dinámico |
