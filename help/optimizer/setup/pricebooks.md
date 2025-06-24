---
title: Libros de precios
description: Aprenda a administrar libros de precios en  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 553490762ef10e43ccce1654acec59aeb83bb5f9
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Libros de precios

Este artículo describe cómo definir y asignar libros de precios a vistas de catálogo con controles adecuados de control de datos.

Consulte la [documentación para desarrolladores](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/api-reference/#tag/Price-Books) para obtener información sobre cómo ingerir información del libro de precios de un sistema de terceros en [!DNL Adobe Commerce Optimizer] mediante la API de libro de precios.

Con los libros de precios puede definir las fuentes del catálogo de precios para administrar los precios de los productos en diferentes niveles de clientes y mercados. Los libros de precios admiten un modelo jerárquico, que permite hasta tres niveles de libros de precios secundarios anidados en cada libro de precios base. Cada libro de precios puede hacer referencia a un libro de precios principal, formando una estructura de árbol para las fuentes del catálogo de precios.

El libro de precios base define la moneda para sí mismo y para todos sus libros de precios secundarios. Los libros de precios secundarios heredan esta divisa y no pueden anularla.

## Conceptos clave

| Término | Descripción |
|------|-------------|
| **Libro de precios** | Agrupación lógica que define el origen del catálogo de precios; por ejemplo, una región específica o nivel de cliente y que se utiliza para administrar los precios de los productos. |
| **Reserva de precios de reserva** | El libro de precios más alto de una jerarquía. No tiene principal y es el libro de precios *solamente* que define la moneda para sí mismo y para todos sus libros de precios descendientes.<br/><br/>Si no se define ningún libro principal durante la creación del libro de precios (a través de la API), se crea un nuevo libro de precios de reserva. |
| **Libro de precios principal** | Un libro de precios de nivel superior del que un libro de precios para niños puede heredar los precios si no están establecidos explícitamente en el niño. |
| **Profundidad de jerarquía** | No se aplica un máximo de 3 niveles (reserva → hijo → nieto)<br/><br/>en el momento de la ingesta. |
| **Moneda** | Definido solo en el libro de precios de reserva. Heredado por todos los niños, libros de precios.<br/><br/>Si no se especifica la divisa durante la creación del libro de precios de reserva (a través de la API), el valor predeterminado de la divisa es USD. |
| **Precio del producto** | El precio específico asignado a un producto (SKU) dentro de un libro de precios en particular. |
| **Descuentos** | Los descuentos se definen en Precio del producto. No heredado. |
