---
title: Transferencia de Inventory management Source
description: Configure las existencias para  [!DNL Store Fulfillment solution] con Adobe Commerce Inventory management. Configure un nuevo inventario de stock y transfiéralo fuera del inventario predeterminado para que pueda asignarlo a orígenes configurados para habilitar las capacidades de recogida de tienda requeridas por la solución Store Fulfillment.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Transferencia de Inventory management Source

La solución [!DNL Store Fulfillment] utiliza Adobe Commerce Inventory management nativo. De manera predeterminada, la configuración [!DNL Commerce] asigna todo el inventario web a las existencias predeterminadas, que no pueden tener fuentes adicionales asignadas. Dado que a un sitio web solo se le puede asignar un único inventario de stock, un comerciante debe configurar un nuevo inventario de stock y, opcionalmente, transferir su inventario de origen predeterminado a un origen que esté asignado al ámbito adecuado. A continuación, el origen se puede asignar al nuevo stock.

>[!IMPORTANT]
>
>Los comerciantes deben mantener el origen predeterminado para todos los productos incluidos en los tipos de producto de grupo y paquete. Estos productos necesitan una cantidad de inventario que cumpla el umbral de cantidad mínima para los artículos en stock e incluyan un estado de stock de [!UICONTROL In Stock].

Estos cambios de configuración le ayudan a lograr tres cosas:

1. [Transfiera el inventario al origen](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/quantities/inventory-transfer) para mover el inventario del stock/origen predeterminado al nuevo stock/origen.

1. [Asignar fuentes en lote](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/quantities/bulk-assignment) para agregar las nuevas fuentes para todos sus productos.

1. [Complete actualizaciones masivas de los atributos de producto](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/bulk-product-attribute-update) para agregar los atributos `Allow Store Pickup` y `Allow Home Delivery` a los productos existentes. Cuando se instala la solución, los atributos tienen los valores óptimos de *default*. Sin embargo, estos atributos no se aplican a los productos existentes hasta que complete el proceso de actualización masiva.

El inventario se deduce del origen seleccionado (ubicación de tienda minorista o almacén de comercio electrónico). Las fuentes utilizadas como almacenes de comercio electrónico deben asignarse a las mismas existencias que la ubicación de recogida de la tienda y priorizarse antes que las ubicaciones de venta minorista. Para obtener más información, vea [Priorizar orígenes para un archivo de Stock](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/stocks/stocks-prioritize-sources).

Para obtener más información sobre la administración del inventario, los inventarios de stock y los orígenes, consulte la documentación del usuario de Adobe Commerce:

- [Administrar inventario](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction)

- [Administración de cantidades de inventario](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/quantities/quantities-manage)

- [Administrar existencias](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/stocks/stocks-manage)

- [Administrar orígenes](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/sources/sources-manage)

- [Priorización de orígenes para un recurso](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/stocks/stocks-prioritize-sources)

- [Actualizaciones masivas para los atributos del producto](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/bulk-product-attribute-update)


>[!IMPORTANT]
>
>Cambiar la configuración para las fuentes de inventario y stock también puede tener un impacto descendente en los sistemas integrados. Asegúrese de comprender cómo afectan los cambios en la configuración de inventario a estos sistemas.
