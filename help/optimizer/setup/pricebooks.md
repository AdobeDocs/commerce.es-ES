---
title: Libros de precios
description: Aprenda a administrar libros de precios en  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
exl-id: a1849830-3d0e-4df9-ab73-380659c3f9dc
source-git-commit: 513ed97442bfffe74d64f4eb0484cfa8f25b5ecc
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Libros de precios

Los libros de precios permiten definir los precios de los productos para un origen de catálogo en diferentes niveles de clientes y mercados. Los libros de precios admiten un modelo jerárquico, que permite hasta tres niveles de libros de precios secundarios anidados en cada libro de precios base. Cada libro de precios puede hacer referencia a un libro de precios principal, formando una estructura de árbol para las fuentes del catálogo de precios.

El libro de precios base define la moneda para sí mismo y para todos sus libros de precios secundarios. Los libros de precios secundarios heredan esta divisa y no pueden anularla.

Consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/services/reference/rest/) para obtener información sobre cómo crear, actualizar y eliminar libros de precios [!DNL Adobe Commerce Optimizer] mediante la API de libros de precios.

## Conceptos clave

| Término | Descripción |
|------|-------------|
| **Libro de precios** | Agrupación lógica que define los precios para un origen de catálogo; por ejemplo, una región específica o nivel de cliente y se utiliza para administrar los precios de los productos. |
| **Reserva de precios de reserva** | El libro de precios más alto de una jerarquía. No tiene principal y es el libro de precios *solamente* que define la moneda para sí mismo y para todos sus libros de precios descendientes.<br/><br/>Si no se define ningún libro principal durante la creación del libro de precios (a través de la API), se crea un nuevo libro de precios de reserva. |
| **Libro de precios principal** | Un libro de precios de nivel superior del que un libro de precios para niños puede heredar los precios si no se establecen explícitamente en el niño. |
| **Profundidad de jerarquía** | No se aplica un máximo de tres niveles (Alternativa -> Secundario -> Nieto)<br/><br/>en el momento de la ingesta. |
| **Moneda** | Definido solo para el libro de precios de reserva. Heredado de todos los libros de precios secundarios.<br/><br/>Si no se especifica la divisa durante la creación del libro de precios de reserva (a través de la API), el valor predeterminado de la divisa es USD. |
| **Precio del producto** | El precio específico asignado a un producto (SKU) dentro de un libro de precios en particular. |
| **Descuentos** | Los descuentos se definen en el precio del producto. No heredado. |
