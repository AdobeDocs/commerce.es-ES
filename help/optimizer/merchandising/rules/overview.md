---
title: Reglas de comercialización
description: '[!DNL Adobe Commerce Optimizer] reglas de comercialización combinan lógica con acciones para dar forma a la experiencia de compra.'
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
exl-id: f2a9b5e8-d23d-4855-b424-ca6b40e057df
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Reglas de comercialización

Las reglas de comercialización se refieren a un conjunto de reglas que combinan lógica con acciones para dar forma a la experiencia de búsqueda de un comprador en su tienda. Puede utilizar reglas de comercialización para impulsar, enterrar, fijar u ocultar productos con el fin de calibrar los resultados de búsqueda en tiempo real para lograr los objetivos de su empresa.

Cada regla tiene tres componentes principales:

- Condiciones: las condiciones que almacenan en déclencheur una acción.
- Eventos: las acciones que se realizan cuando se cumplen las condiciones.
- Detalles: nombre de la regla, y marco temporal y descripción opcionales.

Puede combinar varias condiciones y acciones, y programar una regla para que esté activa durante un periodo. También puede establecer una regla predeterminada que se aplique incluso cuando no se haya definido ningún término de búsqueda.

## Requisitos

Una regla de búsqueda simple puede tener una sola condición y un solo evento, mientras que una regla compleja puede tener hasta diez condiciones que almacenen en déclencheur hasta 25 eventos.
Las reglas pueden tener:

- Hasta diez condiciones
- Hasta 25 eventos

El texto de la consulta puede contener:

- Caracteres alfanuméricos (letras y números)
- Caracteres en mayúsculas o minúsculas. Se omiten las mayúsculas.

## Operadores lógicos

Los operadores lógicos `AND` y `OR` unen dos condiciones y devuelven resultados diferentes. Todos los operadores lógicos utilizados en una regla con varias condiciones son los mismos. No es posible usar `AND` y `OR` a la vez en la misma regla.

### Operadores de coincidencia

Los operadores de coincidencia `All` y `Any` determinan el operador lógico que se usa para unir varias condiciones en la regla y se puede usar para cambiar el operador existente.

- `All`: utiliza el operador lógico `AND` para unir varias condiciones. Una regla que usa el operador de coincidencia `All` solo puede tener una condición `Search query is`.
- `Any`: utiliza el operador lógico `OR` para unir varias condiciones.

Al componer una regla compleja, puede resultar útil escribirla con sangría para describir las condiciones, los eventos asociados y los nombres de producto o SKU necesarios para devolver los resultados que desea lograr. A continuación, genere la regla y pruebe el resultado.

## Regla predeterminada

Puede establecer una regla predeterminada que se aplique cuando no se proporciona ningún término de búsqueda o cuando no se puede aplicar ninguna otra regla de búsqueda. Si establece la regla predeterminada en Más compradas, todas las consultas tendrán ese tipo de clasificación de forma predeterminada, a menos que se sustituyan por un término de búsqueda más específico. No se puede establecer ningún término de búsqueda para la regla predeterminada.

## Orden de prioridad con varias reglas

Solo se aplica una regla de búsqueda a un término de búsqueda al mismo tiempo.
Si se encuentran varias reglas aplicables a una frase de búsqueda, se aplican todas estas reglas. Si hay un conflicto entre dos reglas (`rule 1` que aumenta sku1 pero `rule 2` oculta el mismo SKU), entonces la regla aplicada más recientemente (`rule 2`) tiene prioridad.

- Las reglas se ordenan por la marca de tiempo &quot;Última modificación&quot;. La regla modificada más recientemente se aplica primero, y las reglas más antiguas después, en orden de marca de tiempo.
- La condición `query is` tiene prioridad sobre otras condiciones. Si una regla más reciente contiene una condición `query contains`, pero una regla más antigua tiene una condición `query is`, se aplica la regla `query is`.

### Solicitudes de tienda

Si una regla activa que contiene una condición `query is` coincide con la frase de búsqueda, se aplica. Si hay varias reglas coincidentes con una condición `query is`, se aplica la regla activa actualizada más recientemente.
De lo contrario, se aplica la regla activa actualizada más recientemente.

### Previsualizar solicitudes

La solicitud realizada en [!DNL Adobe Commerce Optimizer] funciona de manera ligeramente diferente. Al obtener una vista previa de [!DNL Adobe Commerce Optimizer], se aplican todas las reglas, incluidas las caducadas y programadas.

- Si la regla que se está previsualizando tiene una condición `query is`, se aplica.
- Si la regla que se está previsualizando no tiene una condición `query is` y se encuentra una regla coincidente activa posterior con una condición `query is`, se aplica la regla `query is`.
- Si la regla que se está previsualizando no tiene una condición `query is` y no se encuentra ninguna otra regla con una condición `query is`, se aplica la regla que se está previsualizando.
