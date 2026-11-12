---
title: Libros de precios
description: Obtenga información sobre cómo administrar libros de precios en [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y a [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
exl-id: a1849830-3d0e-4df9-ab73-380659c3f9dc
TQID: https://experienceleague.adobe.com/-vL79MMePcUdhE-gPwjFJZStZUtNLKAUxpePm4Fvmfk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: cde6d0c92f4c169588164c22c948d1b287873bdd
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%
---
# Libros de precios

Los libros de precios definen los precios de los productos para un origen de catálogo en todos los niveles y mercados de clientes. Admiten un modelo jerárquico, que permite hasta tres niveles de libros de precios secundarios anidados en cada libro de precios base. Cada libro de precios puede hacer referencia a un libro de precios principal, formando una estructura de árbol para las fuentes del catálogo de precios.

![Jerarquía de libros de precios](../assets/price-book-hier.png)

El libro de precios base define la moneda para sí mismo y para todos sus libros de precios secundarios. Los libros de precios secundarios heredan esta divisa y no pueden anularla.

## Conceptos clave

| Término | Descripción |
| ------ | ------------- |
| **Libro de precios** | Agrupación lógica que define los precios para un origen de catálogo; por ejemplo, una región específica o nivel de cliente y se utiliza para administrar los precios de los productos. |
| **Reserva de precios de reserva** | El libro de precios más alto de una jerarquía. No tiene principal y es el libro de precios *solamente* que define la moneda para sí mismo y para todos sus libros de precios descendientes.<br/><br/>Si no se define ningún libro principal durante la creación del libro de precios (a través de la API), se crea un nuevo libro de precios de reserva. |
| **Libro de precios principal** | Un libro de precios de nivel superior del que un libro de precios para niños puede heredar los precios si no se establecen explícitamente en el niño. |
| **Profundidad de jerarquía** | No se aplica un máximo de tres niveles (Alternativa -> Secundario -> Nieto)<br/><br/>en el momento de la ingesta. |
| **Moneda** | Definido solo para el libro de precios de reserva. Heredado de todos los libros de precios secundarios.<br/><br/>Si no se especifica la divisa durante la creación del libro de precios de reserva (a través de la API), el valor predeterminado de la divisa será USD. |
| **Precio del producto** | El precio específico asignado a un producto (SKU) dentro de un libro de precios en particular. |
| **Descuentos** | Los descuentos se definen en el precio del producto. No heredado. |

## Implementación del libro de precios

La implementación de la guía de precios varía según la implementación de Commerce.

* En instancias de Adobe Commerce Optimizer con back-ends de Commerce de terceros, los libros de precios se crean mediante la API de REST de ingesta de datos. Puede asignarlos y administrarlos desde el espacio de trabajo de vista de catálogo en Commerce Optimizer Studio.

* En Adobe Commerce as a Cloud Service con el modelo de datos de catálogo maquetable (CCDM), los libros de precios se asignan a partir de los datos de catálogo y de precios de Adobe Commerce. Puede ver los libros de precios asignados a cada vista de catálogo desde el administrador de Commerce.

* En Adobe Commerce, en implementaciones locales o de infraestructura en la nube con Adobe Commerce Optimizer Connector, los libros de precios también se asignan a partir de los datos de precios y el catálogo de Adobe Commerce. Puede ver los libros de precios asignados a cada vista de catálogo desde el espacio de trabajo Vista de catálogo en la instancia de Commerce Optimizer conectada.

## Añadir libros de precios

Agrega libros de precios a [!DNL Adobe Commerce Optimizer] mediante la API de libro de precios. Consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/services/reference/rest/) para aprender a crear, actualizar y eliminar libros de precios para [!DNL Adobe Commerce Optimizer].

## Ver libros de precios

Después de ingerir libros de precios en [!DNL Adobe Commerce Optimizer], puede ver la lista de libros de precios y sus identificadores correspondientes en la página **Vista de catálogo**.

>[!NOTE]
>
>Una vista de catálogo privado (una con [!UICONTROL Catalog Protection] habilitado) sólo puede hacer referencia a un libro de precios. Ver [Restricción del libro de precios en las vistas del catálogo privado](private-catalog-view.md#price-book-restriction-on-private-catalog-views).

1. Vaya a _Configuración de la tienda_ y haga clic en **[!UICONTROL Catalog views]**.

1. Haga clic en **[!UICONTROL Create catalog view]**. &#x200B;

   En los detalles de configuración de la vista del catálogo, seleccione uno de los libros de precios disponibles.

   ![Nombres e ID del libro de precios](../assets/price-book-name-ids.png)

## Configurar disponibilidad del libro de precios

Especifique los datos de precios disponibles para cada vista del catálogo configurando la disponibilidad del libro de precios para cada vista.

1. En el área de trabajo **Vista de catálogo**, seleccione la vista de catálogo que desee configurar.

1. En la sección [!UICONTROL Price Books], seleccione las opciones de la libreta de precios para configurar los precios disponibles en las tiendas respaldadas por la vista de catálogo.

1. Haga clic en **[!UICONTROL Save]** para aplicar los cambios a la vista del catálogo.
