---
title: Límites y límites
description: Conozca los límites y limitaciones de [!DNL Adobe Commerce Optimizer] para asegurarse de que cumple con las necesidades de su empresa.
role: Admin, Developer
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
source-git-commit: 149b87fc822e5d07eed36f3d6a38c80e7b493214
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Límites y límites

>[!NOTE]
>
>Esta documentación describe los límites y limitaciones del desarrollo de acceso anticipado y no refleja todas las funcionalidades destinadas a la disponibilidad general.

A continuación se indican los límites y limitaciones de Adobe Commerce Optimizer.

## Catálogo

- La tasa garantizada de ingesta de catálogos es: 1000 productos/minuto y 5000 precios/minuto
- El número base de actualizaciones de productos por día es de 1 000 000.
- El número total de SKU permitidas en una sola instancia es de 250 000. 
- El número máximo de ámbitos es 50.
- El número de variantes por producto es de 10.000.
- El tamaño del producto no puede superar los 200 kb.

## Precios

- El número máximo de libros de precios es de 1.000.

## Búsqueda y tienda

- El número de productos que puede devolver una sola solicitud de búsqueda es 100.
- El número máximo de atributos filtrables es 200
- El número máximo de atributos en los que se puede buscar es 200
- El número máximo de atributos que se pueden ordenar es 50
- El número máximo de facetas es 100. Todas las facetas deben ser atributos filtrables.
- El número máximo de opciones que devuelve un solo gato de faceta es 100, que se pueden aumentar por solicitud de asistencia.

## Canales y políticas

- El número máximo de canales por inquilino es 1000.
- El número máximo de directivas asignadas a un canal es 10.
- El número máximo de valores de atributo utilizados en una directiva es 100. 

## Descubrimiento de productos y recomendaciones

- Para la detección de productos, no se admite la comercialización basada en atributos ni la configuración de precios.
- Para recomendaciones:

   - [!DNL Adobe Commerce Optimizer] admite el tipo de recomendación _Vistos recientemente_ para acceso anticipado.
   - No se admiten exclusiones o inclusiones de categorías o atributos.
   - No puede obtener una vista previa de las recomendaciones en [!DNL Adobe Commerce Optimizer].
