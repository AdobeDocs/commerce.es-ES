---
title: Límites y fronteras
description: Conozca los límites y los límites para [!DNL Adobe Commerce Optimizer] asegurarse de que satisface las necesidades de su negocio.
role: Admin, Developer
source-git-commit: 45a43fe2ada206515c512a04aa6e9072e08844cc
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Límites y límites

>[!NOTE]
>
>Esta documentación describe los límites y límites para el desarrollo del acceso anticipado y no refleja todos los funcionalidad destinados a la disponibilidad general.

A continuación se indican los límites y los límites de Adobe Systems Commerce Optimizer.

## Catálogo

- La tasa garantizada de ingesta de catálogo es: 1000 productos/minuto y 5000 precios/minuto
- El número base de actualizaciones de productos al día es 1.000.000.
- El número total de SKU permitidos en una sola instancia es de 250 000. 
- El número máximo de ámbitos es 50.
- El número de variantes por producto es de 10.000.
- El tamaño del producto no puede superar los 200 kb.

## Precios

- El número máximo de libros de precios es de 30.000. El número de nivel básico de los libros de precios no puede exceder de 100 y debe seguir la regla donde (el número de libros de precios) x (el número de canales) debe ser inferior o igual a 100.
- El precio garantizado fuente la tasa de ingestión es de 5000 registros por minuto.
- Un único registro de precios no puede tener más de 10 descuentos.
- El número base de actualizaciones de precios por día es 5,000,000.

## Search y escaparate

- El número de productos que un único búsqueda solicitud puede devolver es 100.
- El número máximo de atributos filtrables es 200
- El número máximo de atributos en los que se pueden realizar búsquedas es 200
- El número máximo de atributos que se pueden ordenar es 50
- El número máximo de facetas es 100. Todas las facetas deben ser atributos filtrables.
- El número máximo de opciones que devuelve un gato de una sola faceta es 100, que se puede aumentar por solicitud de soporte.

## Canales y políticas

- El número máximo de canales por inquilino es de 1000.
- El número máximo de directivas asignadas a una canal es 10.
- El número máximo de valores de atributo utilizados en una directiva es 100. 

## Descubrimiento de productos y recomendaciones

- Para la detección de productos, no se admite la configuración de precios y comercialización basada en atributos.
- Para recomendaciones:

   - ACO admite el tipo de _recomendación vistos_ recientemente para EA
   - No se admiten inclusiones o exclusiones de categoría o atributos.
   - No puede previsualización recomendaciones en [!DNL Adobe Commerce Optimizer].
