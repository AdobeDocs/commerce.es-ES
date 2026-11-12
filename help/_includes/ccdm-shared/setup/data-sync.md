---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%
---
La página **Sincronización de datos** muestra una descripción general del estado de sincronización de los datos de producto transferidos desde la fuente de datos (el catálogo de Commerce, el sistema de administración de información de producto (PIM), el sistema de planificación de recursos empresariales (ERP), etc. existentes) a la capa de datos de los servicios de comercialización.

La página **Sincronización de datos** proporciona información valiosa sobre la disponibilidad de datos de productos para tu tienda, lo que garantiza que se puedan mostrar rápidamente a tus compradores.

## Acceso al espacio de trabajo de sincronización de datos

La forma de abrir el área de trabajo *Sincronización de datos* depende del producto que use:

- **Administrador de Adobe Commerce** (Adobe Commerce as a Cloud Service)—Seleccione *Tiendas* > **Sincronización de catálogos**.
- **Adobe Commerce Optimizer Studio**—Seleccione *Configuración de tienda* > **Sincronización de datos**.

![Sincronización de datos](/help/assets/ccdm-shared/setup/data-sync.png)

La página **Sincronización de datos** contiene los siguientes campos:

| Campo | Descripción |
| --- | --- |
| Origen del catálogo | Configuración regional específica para los datos sincronizados. |
| [!DNL Catalog Service] | Muestra la última actualización de sincronización, el total de productos recibidos, un campo de búsqueda y una tabla de productos sincronizados para [!DNL Catalog Service]. |
| Descubrimiento de productos | Muestra la última actualización de sincronización, el total de productos recibidos, un campo de búsqueda y una tabla de los productos sincronizados para la búsqueda. |
| Recommendations | Muestra la última actualización de sincronización, el total de productos recibidos, un campo de búsqueda y una tabla de productos sincronizados para Recommendations. |
| Productos recibidos en las últimas 3 horas | Muestra el número de productos que se han transferido del origen del catálogo a la capa de datos de Servicios de comercialización en las últimas tres horas. Si realiza actualizaciones poco frecuentes en el catálogo, este valor suele ser cero. |
| Total de productos en el catálogo | Refleja el número total de productos de catálogo disponibles en la capa de datos de Servicios de comercialización. |
| Productos sincronizados | Proporciona detalles sobre los productos sincronizados con la capa de datos de Servicios de comercialización. De forma predeterminada, esta tabla está ordenada por Última actualización. Para buscar un producto específico, utilice el campo **[!UICONTROL Search by Name or SKU]**. |

## Lista de productos sincronizados

Para ver los detalles de un producto sincronizado en formato JSON, haga clic en el icono de código ![Vínculo de código](/help/assets/ccdm-shared/setup/data-sync-details.png) en la fila del producto de la tabla Productos sincronizados.

![Detalles del producto sincronizado](/help/assets/ccdm-shared/setup/synced-products.png)

## Resincronizar datos de catálogo

Si no ve productos específicos en la página **Sincronización de datos**, debe iniciar una resincronización desde el sistema de flujo ascendente. Sin embargo, tenga en cuenta que una resincronización puede aumentar la carga en los recursos de hardware. Sin embargo, puede que sea necesario volver a sincronizar el catálogo en los siguientes casos:

- Cuando se realizan cambios significativos en el catálogo de productos, como agregar nuevos productos, actualizar detalles del producto o modificar categorías

- Si notas discrepancias o problemas de rendimiento en la visualización de datos de productos en tus tiendas

>[!IMPORTANT]
>
>El tiempo que se tarda en completar la sincronización varía en función del tamaño del catálogo y el volumen de datos actualizados.

## Compruebe que la sincronización de datos funciona

En el caso de los proyectos que utilizan Adobe Commerce como origen de datos de flujo ascendente, puede supervisar el proceso de exportación de datos e iniciar operaciones de resincronización desde la página Estado de sincronización de fuente de datos. Para obtener más información, consulte [Supervisión del estado de sincronización de fuentes de datos](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status).
