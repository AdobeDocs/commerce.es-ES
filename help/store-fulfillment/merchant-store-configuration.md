---
title: Configuración de tiendas de comerciantes
description: Configure las fuentes de Inventory management mejoradas como tiendas comerciales.
role: Admin
level: Experienced
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# Configuración de tiendas comerciales (Source)

Esta solución mejora las funciones nativas de Inventory management al ampliar las fuentes de stock con funciones orientadas a las operaciones para los comerciantes.

- Agregar coordenadas geográficas para la ubicación de la tienda
- Designar el origen como [!DNL Store Pickup Location] y especificar las capacidades de envío disponibles (Enviar a tienda, Enviar desde tienda)
- Especifique las opciones de recogida disponibles (en la tienda o en la acera), las instrucciones de recogida personalizadas y otra información para comunicar los detalles de la recogida y las instrucciones a los clientes

Los términos _origen_ y _ubicación de la tienda comercial_ se usan indistintamente. Todos los registros son orígenes de inventario, pero los orígenes también pueden ser ubicaciones de tiendas comerciales, según los valores de configuración.

Administrar la configuración de las tiendas del comerciante desde el administrador: **[!UICONTROL Stores > Inventory > Sources >  Edit Source]**.

>[!NOTE]
>
>Durante el proceso de configuración, puede ser necesario vaciar la caché después de crear fuentes o actualizar las fuentes existentes.

## **General**

<table>
<tbody>
<tr>
<th>Campo</th>
<th>Descripción</th>
<th>Ámbito</th>
<th>Requerido</th>
</tr>
<tr>
<td><strong>[!UICONTROL Latitude]</strong></br><code>Base Attribute: latitude</code></td>
<td>Coordenada latitudinal de la ubicación del almacén comercial. Esta información necesaria se utiliza en la búsqueda de ubicación y en la ubicación de mapas en la experiencia de la tienda. El valor debe coincidir con la dirección exacta del almacén para pasar la validación.</td>
<td>Global</td>
<td>Sí</td>
</tr>
<tr>
<td><strong>[!UICONTROL Longitude]</strong></br><code>Base Attribute: Longitude</code></td>
<td>Coordenada longitudinal de la ubicación del almacén comercial. Esta información necesaria se utiliza en la búsqueda de ubicación y en la ubicación de mapas en la experiencia de la tienda. El valor debe coincidir con la dirección exacta del almacén para pasar la validación.</td>
<td>Global</td>
<td>Sí</td>
</tr>
<tr>
<td><strong>[!UICONTROL Use as Pickup Location]</br></strong><code>Base Attribute: is_pickup_location_active</code></td>
<td>Designar el origen como ubicación de recogida en tienda disponible. Esta configuración determina si el origen se sincroniza y se muestra a los visitantes.</td>
<td>Global</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship to Store]</strong><br><code>Extension Attribute: allow_ship_to_store</code></td>
<td>Configurar las capacidades de envío a tienda en el nivel de origen. Para obtener más información, vea la opción [Configuración general](enable-general.md), <strong>[!UICONTROL Enable Ship To Store]
</tr>
<tr>
<td><strong>[!UICONTROL Latitude]</strong></br><code>Base Attribute: latitude</code></td>
<td>Coordenada latitudinal de la ubicación del almacén comercial. Esta información necesaria se utiliza en la búsqueda de ubicación y en la ubicación de mapas en la experiencia de la tienda. El valor debe coincidir con la dirección exacta del almacén para pasar la validación.</td>
<td>Global</td>
<td>Sí</td>
</tr>
<tr>
<td><strong>[!UICONTROL Longitude]</strong></br><code>Base Attribute: Longitude</code></td>
<td>Coordenada longitudinal de la ubicación del almacén comercial. Esta información necesaria se utiliza en la búsqueda de ubicación y en la ubicación de mapas en la experiencia de la tienda. El valor debe coincidir con la dirección exacta del almacén para pasar la validación.</td>
<td>Global</td>
<td>Sí</td>
</tr>
<tr>
<td><strong>[!UICONTROL Use as Pickup Location]</br></strong><code>Base Attribute: is_pickup_location_active</code></td>
<td>Designar el origen como ubicación de recogida en tienda disponible. Esta configuración determina si el origen se sincroniza y se muestra a los visitantes.</td>
<td>Global</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship to Store]</strong></br> <code>Extension Attribute: [!DNL allow_ship_to_store]</code></td>
<td>Configurar las capacidades de envío a tienda en el nivel de origen. Para obtener más información, vea la opción [Configuración general](enable-general.md), <strong>[!UICONTROL Enable Ship To Store]</strong>.</td>
<td>Global</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong></br><code>Extension Attribute: [!DNL use_as_shipping_source]</code></td>
 <td>Configurar las capacidades de envío desde la tienda en el nivel de origen. Para obtener más información, vea la opción [Configuración general](enable-general.md), [!UICONTROL Enable Ship From Store].</td>
<td>Global</td>
<td>No</td>
</tr>
<tr>
<td>Global</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong><code></br><code>Extension Attribute: [!DNL use_as_shipping_source]</code></td>
<td>Configurar las capacidades de envío desde la tienda en el nivel de origen. Para obtener más información, vea la opción [Configuración general](enable-general.md), [!UICONTROL Enable Ship From Store].</td>
<td>Global</td>
<td>No</td>
</tr>
</tbody>
</table>



| **Campo** | **Descripción** | **Ámbito** | **Requerido** |
|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Latitude]**</br>`Base Attribute: latitude` | Coordenada latitudinal de la ubicación del almacén comercial. Esta información necesaria se utiliza en la búsqueda de ubicación y en la ubicación de mapas en la experiencia de la tienda. El valor debe coincidir con la dirección exacta del almacén para pasar la validación. | Global | Sí |
| **[!UICONTROL Longitude]**</br>`Base Attribute: Longitude` | Coordenada longitudinal de la ubicación del almacén comercial. Esta información necesaria se utiliza en la búsqueda de ubicación y en la ubicación de mapas en la experiencia de la tienda. El valor debe coincidir con la dirección exacta del almacén para pasar la validación. | Global | Sí |
| **[!UICONTROL Use as Pickup Location]**</br>`Base Attribute:[!DNL is_pickup_location_active]` | Designar el origen como ubicación de recogida en tienda disponible. Esta configuración determina si el origen se sincroniza y se muestra a los visitantes. | Global | No |
| **[!UICONTROL Enable Ship to Store]**</br>`Extension Attribute: [!DNL allow_ship_to_store]` | Configurar las capacidades de envío a tienda en el nivel de origen. Para obtener más información, vea la opción [Configuración general](enable-general.md), **[!UICONTROL Enable Ship To Store]**. | Global | No |
| **[!UICONTROL Enable Ship From Store]**</br>`Extension Attribute: [!DNL use_as_shipping_source]` | Configurar las capacidades de envío desde la tienda en el nivel de origen. Para obtener más información, vea la opción [Configuración general](enable-general.md), [!UICONTROL Enable Ship From Store] | Global | No |

{style="table-layout:auto"}

## Configuración de ubicación de recogida

| **Campo** | **Descripción** | **Ámbito** | **Requerido** |
|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Allow In-Store Pickup]**</br>`Extension Attribute: [!DNL store_pickup_enabled]` | Una de las dos opciones de recogida. [!DNL In-Store Pickup] hace referencia a la capacidad de permitir que un cliente ingrese la ubicación de la tienda comercial para recuperar su pedido. </br></br>Cuando está habilitada, esta opción podría presentarse al cliente durante el cierre de compra. </br></br>Esta opción también invalida la configuración global de [!UICONTROL Enable In-store Pickup] que se configuró en [!UICONTROL Delivery Method] para [!UICONTROL In-store Pickup] | Global | No |
| **Instrucciones de recogida en tienda**</br>`Extension Attribute: store_pickup_instructions` | Un mensaje personalizable entregado al cliente en la notificación por correo electrónico **Pedido listo para recoger en tienda**. | Global | No |
| **Permitir Lado De La Curva**</br>`Extension Attribute: curbside_enabled` | Una de las dos opciones de recogida. La entrega en la acera permite al cliente estacionar su vehículo en un lugar designado en la ubicación de la tienda del comerciante. En esta situación, un dependiente entrega el pedido al cliente. </br></br>Cuando está habilitada, esta opción se puede presentar al cliente durante el cierre de compra. Además, es posible que se pida al cliente que describa su vehículo y el lugar de estacionamiento durante el proceso de check-in. </br></br>Esta opción también invalida la configuración global de **Habilitar la recogida en la zona de la acera** que se configuró en el **método de entrega** para **recogida en la tienda** | Global | No |
| **[!UICONTROL Curbside Instructions]**</br>`Extension Attribute: curbside_instructions` | Un mensaje personalizable entregado al cliente en la notificación por correo electrónico [!UICONTROL Order Ready For Pickup in Store]. | Global | No |
| **[!UICONTROL Estimated Pickup Lead Time]**</br>`Extension Attribute: pickup_lead_time` | La cantidad de minutos necesarios antes de recibir un pedido, recogerlo y prepararlo para su recogida. </br></br>Esta información se usa para mostrar las horas estimadas para la recogida de pedidos a los clientes en el sitio web.</br></br> Al establecer esta opción, se anula la configuración global de **Tiempo de espera estimado para la recogida** configurada para el **Método de entrega** en la configuración de **Recogida en la tienda**. | Global | No |
| **[!UICONTROL Estimated Pickup Time Label]**</br>`Extension Attribute: pickup_time_label` | Etiqueta que muestra el número de minutos hasta que un pedido está listo para ser recogido.</br></br> Al personalizar esta etiqueta, puede usar el código %1 para insertar su **Plazo estimado de recogida**.</br></br> Al establecer esta opción, se anula la configuración global de [!UICONTROL Estimated Pickup Time Label] configurada para [!UICONTROL Delivery Method] en [!UICONTROL In-store Pickup]. | Global | No |

### **Horas de apertura**

| **Campo** | **Descripción** | **Ámbito** | **Requerido** |
|------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Location Timezone]**</br>`Extension Attribute: timezone` | Zona horaria de la ubicación de la tienda del comerciante. Para cada día, establezca las horas de apertura y cierre.</br></br>Esta configuración se usa para optimizar los tiempos de recogida estimados y en los informes del servicio de cumplimiento. | Global | Sí |
| **[!UICONTROL Opening Hours]**</br>`Internal Attribute: inventory_source_opening_hours_dynamic_rows` | El horario de funcionamiento de la ubicación del almacén comercial. </br></br>Esta información se puede usar para optimizar los tiempos de recolección estimados y en los informes de servicio de cumplimiento. | Global | Sí |

### Configuración de las opciones de la interfaz de Check-in Experience



| **Campo** | **Descripción** | **Ámbito** | **Requerido** |
|---------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Use Parking Spots]**</br>`Extension Attribute: parking_spots_enabled` | Especifique si la ubicación de la tienda del comerciante tiene lugares de estacionamiento designados para la recogida en la acera. </br></br>Si está activada, puede configurar las plazas de estacionamiento disponibles. | Global | No |
| **[!UICONTROL Is Parking Spot a Mandatory Field?]**</br>`Extension Attribute: parking_spot_mandatory` | Especifique si se requiere la identificación del lugar de estacionamiento para los clientes durante la experiencia de compra.</br></br>Si está habilitado, se le pedirá al cliente que especifique su lugar de estacionamiento al llegar. Si está desactivado, el cliente puede omitir esta entrada. | Global | No |
| **[!UICONTROL Parking Spots List]**</br> `Internal Attribute: inventory_source_parking_spot_dynamic_rows` | Las plazas de aparcamiento disponibles en esta tienda comercial para la recogida en la acera. Utilice la interfaz proporcionada para asignar un nombre a cada lugar.</br></br> No necesita nombrar todos los lugares de estacionamiento, solo los lugares designados para la acera. Por ejemplo, puede tener filas A-G de estacionamiento disponibles, pero solo los primeros 8 lugares de la fila A están designados para la recogida en la acera. En este escenario, puede definir 8 posiciones; por ejemplo: A1, A2, A3, etc. | Global | No |
| **[!UICONTROL Allow "Other" Parking Spot Field]**</br>`Extension Attribute: custom_parking_spot_enabled` | Cuando está habilitado, este ajuste permite al cliente describir su lugar de estacionamiento durante el check-in. | Global | No |
| **[!UICONTROL Use Car Color]**</br>`Extension Attribute: use_car_color` | Especifique si se admitirá la recopilación del color del vehículo del cliente durante el registro de entrada. </br></br> Las selecciones disponibles para [!UICONTROL Car Color] están configuradas en la configuración del sistema de administración [para la experiencia de protección](check-in-experience-setup.md). | Global | No |
| **[!UICONTROL Is Car Color a Mandatory Field?]**</br>`Extension Attribute: car_color_mandatory` | Especifique si es necesaria la identificación del color del vehículo para los clientes durante el registro de entrada.</br></br>Si está habilitado, se le pedirá al cliente que especifique el color de su vehículo a su llegada. Si está desactivado, el cliente puede omitir esta entrada. | Global | No |
| **[!UICONTROL Use Car Make]** </br>`Extension Attribute: use_car_make` | Especifique si desea apoyar la recogida del fabricante del vehículo del cliente durante el registro de entrada.</br></br> Las selecciones disponibles para [!UICONTROL Car Make] están configuradas en la configuración del sistema de administración [para la experiencia de protección](check-in-experience-setup.md). | Global | No |
| **[!UICONTROL Is Car Make a Mandatory Field?]**</br>`Extension Attribute: car_make_mandatory` | Especifique si se requiere la identificación del fabricante del vehículo para los clientes durante el registro de entrada.</br></br>Si está habilitado, se le pedirá al cliente que especifique la marca de su vehículo a la llegada. Si está desactivado, el cliente puede omitir esta entrada. | Global | No |
| **[!UICONTROL Use Additional Information]**</br> `Extension Attribute: use_additional_information` | Especifique si se admitirá la recopilación de información adicional del cliente durante el registro de entrada. | Global | No |
| **[!UICONTROL Is Additional Information a Mandatory Field?]**</br>`Extension Attribute: additional_information_mandatory` | Especifique si se requiere información adicional para los clientes durante el registro de entrada. </br></br>Si está habilitado, se le pedirá al cliente que especifique información adicional a su llegada. Si está desactivado, el cliente puede omitir esta entrada. | Global | No |
