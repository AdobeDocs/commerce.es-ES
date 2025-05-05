---
title: Configuración de varios sitios web y ámbitos
description: Configure las existencias y los métodos de envío para varios sitios web y ámbitos de almacenamiento.
role: Admin
level: Experienced
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Configuración de varios sitios web y ámbitos

Puede establecer el [Ámbito](https://experienceleague.adobe.com/es/docs/commerce-admin/start/setup/websites-stores-views#scope-settings) para algunos elementos con el fin de admitir varios sitios web, tiendas y vistas de tiendas:

- [Administrar existencias](https://experienceleague.adobe.com/es/docs/commerce-admin/inventory/stocks/stocks-manage) por ámbito

- Administrar [!DNL Delivery Methods] por ámbito

Puede asignar existencias a un sitio web o a un ámbito de tienda. A continuación, actualice las fuentes de la tienda para establecer los métodos de entrega disponibles (envío a domicilio, recogida en la tienda).

Después de actualizar la configuración correctamente, las opciones de recogida de la tienda en la página de detalles del producto (PDP) de la tienda de Adobe Commerce solo se pueden seleccionar para los productos disponibles en una fuente de existencias que permita la recogida en la tienda.

## Administrar configuración de recogida en tienda

Habilite o deshabilite las opciones [!UICONTROL In-Store Pickup] para cada sitio web o ámbito de tienda desde las [configuraciones de métodos de entrega](enable-general.md#delivery-methods) en el administrador.

1. Vaya a **[!UICONTROL Stores > Configuration]**.

1. Seleccione el ámbito (Sitio web para almacenar) que desea configurar.

1. Con el ámbito seleccionado, vaya a **[!UICONTROL Sales > Delivery Methods]**.

1. Deshabilite o habilite el método de entrega **[!UICONTROL In-Store Pickup]**.

También puede administrar si la recogida en la acera o en la tienda está disponible globalmente en esta sección.

Administrar la configuración de [!UICONTROL In-Store Pickup] y [!UICONTROL Delivery Method] por origen de stock. Existen muchas otras configuraciones para disfrutar de una flexibilidad total respecto a la implementación.
