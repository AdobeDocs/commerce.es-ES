---
title: Filtros de recomendación
description: Aprenda a utilizar filtros para controlar qué productos aparecen en  [!DNL Adobe Commerce Optimizer] recomendaciones.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 746c016f149fb49b9c483968a8a5f40196b163ed
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Filtrar productos

[!DNL Adobe Commerce Optimizer] aplica automáticamente filtros predeterminados no configurables a las unidades de recomendación. Si tiene varias unidades de recomendación implementadas en una página, [!DNL Adobe Commerce Optimizer] filtra los productos que se repiten en las unidades. Solo se usa la primera referencia a un producto repetido, para dejar espacio a otros productos que se recomienden. [!DNL Adobe Commerce Optimizer] también filtra los productos comprados anteriormente y los que están en el carro de compras.

Cuando [crea](create.md) una unidad de recomendación, puede definir filtros que controlen qué productos se pueden mostrar en las recomendaciones. Estos filtros se basan en un conjunto de condiciones de inclusión o exclusión que usted defina. En las recomendaciones solo aparecen los productos que cumplen todas las condiciones de inclusión. No se recomiendan los productos que coinciden con cualquiera de las condiciones de exclusión.

Puede configurar varios filtros y habilitar solo los que desee seleccionando la opción en cada página de filtro. Esto le permite crear borradores de filtros para su uso futuro. El número de filtros habilitados se muestra en cada pestaña.

## Condiciones

Las condiciones pueden ser estáticas o dinámicas.

- Una condición estática utiliza atributos de producto existentes para determinar qué productos pueden aparecer en la unidad. Por ejemplo, puede especificar que solo aparezcan en la unidad los productos en existencias con un precio mayor que 25 $.

- Una condición dinámica elimina el contexto actual de un comprador, como la categoría o el producto que se está viendo en ese momento. Por ejemplo, al crear una recomendación de producto para implementarla en páginas de detalles de producto, puede crear una condición para recomendar solo productos que se encuentren dentro de un rango de precios relativo del producto que se está viendo en ese momento.

### Operadores lógicos

Los operadores lógicos `AND` y `OR` se utilizan para unir varias condiciones. Si utiliza filtros de inclusión y exclusión, las inclusiones se evalúan primero para determinar todos los productos posibles que se pueden recomendar y, a continuación, se eliminan de la lista los productos que coinciden con cualquier filtro de exclusión.

- `AND` - Une dos condiciones de filtrado de inclusión
- `OR` - Une dos condiciones de filtrado de exclusión

## Tipos de filtros

![Filtros](../../assets/rec-conditions.png)

### Product

Los filtros de producto especifican qué productos específicos son aptos o no para mostrarse en las recomendaciones. No puede seleccionar productos que estén desactivados o no sean visibles individualmente porque dichos productos nunca pueden aparecer en las recomendaciones.

>[!NOTE]
>
>Los productos secundarios de un producto configurable no se muestran en una unidad de recomendación porque tienen la visibilidad de _No visible individualmente_.

### Precio

Un filtro basado en el precio del producto utiliza el precio final para realizar la comparación. El precio final incluye cualquier descuento o precio especial disponible para compradores anónimos.

<!--### Attribute

You can filter products based on attribute criteria, including attribute values. Selected values use OR logic to either include or exclude products when any of the specified values are found.-->
