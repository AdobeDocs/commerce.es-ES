---
title: Administración de stock de productos
description: Configure las funciones y la mensajería de existencias del comerciante disponibles para los clientes.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Administración de stock de productos

Como comerciante, puede usar las opciones de origen y existencias de Adobe Commerce [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction). Además, puede utilizar la solución Store Fulfillment para controlar otras opciones de disponibilidad de inventario relacionadas con las operaciones de su tienda comercial.

- Opción de envío a domicilio desde tiendas Merchant

- Permitir/disponible para la recogida en tienda

- UPC / SKU / Otros identificadores de producto únicos

- Umbral de falta de stock

- Reducción del inventario de ubicaciones específicas según el pedido

Configurar opciones de Stock de productos del administrador: **[!UICONTROL Catalog > Products > Select Product]**

## **Opciones de productos**

| **Campo** | **Descripción** | **Ámbito** | **Requerido** |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|--------------|
| **Disponible para envío a domicilio** | <p>Establece la disponibilidad de Home Delivery (Ship-from-Store) para el producto. Cuando está activada, cualquier ubicación de tienda de comerciantes asignada con inventario disponible para el producto se considera apta para la opción Entrega a domicilio. Cuando esta opción está desactivada, el producto nunca cumple los requisitos para el envío a domicilio.</p>Normalmente, es suficiente configurar esta opción en el nivel de tienda comercial. Sin embargo, puede haber casos únicos para productos específicos, como los que están sujetos a restricciones de envío federales, que no deberían cumplir los requisitos para Entrega a domicilio.</p> | Sitio web | No |
| **[!UICONTROL Available for Store Pickup]** | <p>Establece la disponibilidad de la recogida en la tienda para el producto. Cuando está activada, cualquier ubicación de tienda de comerciantes asignada con inventario disponible para el producto se considera apta para la opción de recogida de tienda. Cuando está desactivado, el producto nunca es apto para la recogida en tienda.</p><p>Esta opción puede resultar útil para rastrear el inventario de comerciantes en el sistema que no desea vender desde el canal de comercio electrónico.</p> | Sitio web | No |
| **[!UICONTROL UPC / SKU / Custom Scannable Identifier]** | Este atributo debe existir como atributo de producto y está relacionado con la configuración **[!UICONTROL Barcode Source / Barcode Type]**. Este atributo se utiliza para rastrear un código de barras que se puede escanear para sus productos. Este valor puede enviarse cuando se envía un pedido a las tiendas de comerciantes para su picking. Los socios de la tienda pueden usar el valor con la lista de selección para que coincida con los productos en el estante mediante un escáner de código de barras. | Vista de tienda | No |

{style="table-layout:auto"}

## Fuentes del inventario de nivel de producto

| **Campo** | **Descripción** | **Ámbito** | **Requerido** |
|-----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Out of Stock Threshold]** | <p>Defina el umbral de stock para el artículo dentro de cada origen. Cuando las existencias caen por debajo del umbral, se considera que están agotadas en origen.</p><p>Para usar la opción de configuración del almacén global, marque la opción **[!UICONTROL Use Default]**.</p> | Global | No |
| **[!UICONTROL Allow Store Pickup]** | <p>Establece explícitamente si el artículo está disponible para la recogida en la tienda, independientemente de la configuración del inventario o la ubicación de la tienda del comerciante disponible.</p><p>Para usar la configuración de nivel de producto, anule la selección de la opción [!UICONTROL Use Default] y realice la selección. De lo contrario, esta opción se elige en función de la configuración de **[!UICONTROL Allow In-Store Pickup]** que se establece en el origen de existencias.</p> | Global | No |

{style="table-layout:auto"}

