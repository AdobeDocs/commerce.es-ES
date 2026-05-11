---
title: Faceting Workspace
description: Aprenda a utilizar el espacio de trabajo de  [!DNL Live Search] faceting.
exl-id: 7108e41b-44a7-4943-b20f-6ee544d099e9
TQID: https://experienceleague.adobe.com/LsVM4inUqk2EozfVN--FH1Ukggt8A8QBIQXW-SmnxZs
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 229
ht-degree: 0%

---

# Faceting Workspace

El área de trabajo *Faceting* enumera todas las facetas que están disponibles actualmente y proporciona acceso a las herramientas que necesita para configurar y administrar facetas. Las facetas ancladas aparecen primero en la lista de facetas existentes, seguidas de las facetas dinámicas. La lista se puede filtrar para mostrar todas las facetas o solo aquellas que estén ancladas o sean dinámicas.

![Espacio de trabajo de facetas](assets/faceting-workspace.png)

## Establecer el ámbito

Si la instalación de Adobe Commerce incluye varias vistas de tienda, establece **Scope** en la [vista de tienda](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) donde se aplique la configuración de faceta.

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
