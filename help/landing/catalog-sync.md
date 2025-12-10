---
title: Sincronización de catálogo
description: Obtenga información sobre cómo exportar datos de productos del servidor  [!DNL Commerce] a [!DNL Commerce Services].
feature: Catalog Management, Data Import/Export, Catalog Service
exl-id: 99f96b93-b036-490c-8c57-40463a0de365
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# Sincronización de catálogo

>[!NOTE]
>
> El tablero de sincronización de catálogos ahora es el tablero de administración de datos. Este tablero remodelado ahora es compatible con [[!DNL Product Recommendations]](../product-recommendations/guide-overview.md) v6.0.0+, [[!DNL Live Search]](../live-search/overview.md) v4.1.0+ y [[!DNL Catalog Service]](../catalog-service/overview.md) v1.17+. Los clientes pueden obtener el tablero de administración de datos actualizando a la última versión de uno de esos servicios. Obtenga más información al respecto en la documentación de [Panel de administración de datos](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html). Este tema actual permanece para los usuarios que aún no se han actualizado y que aún tienen el panel Sincronización de catálogos.

Adobe Commerce utiliza indexadores para compilar datos de catálogo en tablas. El proceso se activa automáticamente por [eventos](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/index-management.html#events-that-trigger-full-reindexing), como un cambio en el precio de un producto o en el nivel de inventario.

El servicio de sincronización de catálogos mueve continuamente los datos de productos de una instancia de [!DNL Adobe Commerce] a la plataforma [!DNL Commerce Services] para mantenerlos actualizados. Por ejemplo, [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) requiere la información actual del catálogo para devolver con precisión las recomendaciones con los nombres, precios y disponibilidad correctos. Use el panel _Sincronización de catálogo_ para observar y administrar el proceso de sincronización o la interfaz de línea de comandos para almacenar en déclencheur una sincronización de catálogo y reindexar los datos de producto para que los consuma [!DNL Commerce Services]. Consulte [Referencia de la interfaz de la línea de comandos](../data-export/data-export-cli-commands.md) en la guía _Exportación de datos SaaS_.

## Acceso al panel de sincronización de catálogos

Para acceder al panel de sincronización de catálogos, seleccione **Sistema** > _Transferencia de datos_ > **Sincronización de catálogos**.

Con el panel **Sincronización de catálogos**, podrá:

- Ver el estado de sincronización (**En curso**, **Correcto**, **Error**)
- Ver el número total de productos sincronizados
- Busque productos sincronizados para ver su estado actual
- Buscar en el catálogo de la tienda por nombre, SKU, etc.
- Ver los detalles del producto sincronizado en JSON para ayudar a diagnosticar una discrepancia de sincronización
- Reinicio del proceso de sincronización

### Última sincronización

Notifica un estado de sincronización de:

- **Correcto** - Muestra la fecha y la hora en que la sincronización se realizó correctamente y el número de productos actualizados
- **Error** - Muestra la fecha y la hora en que se intentó realizar la sincronización
- **En curso**: muestra la fecha y la hora de la última sincronización correcta

El proceso de sincronización del catálogo se ejecuta automáticamente cada hora. Si no ve los productos esperados en la tienda, o si los productos no reflejan los cambios recientes que ha realizado, puede resolver [problemas de sincronización del catálogo](#resolvesync).

### Productos sincronizados

Muestra el número total de productos sincronizados a partir del catálogo [!DNL Commerce]. Después de la sincronización inicial, solo se deben sincronizar los productos modificados.

## Resincronizar {#resync}

Si debe iniciar una resincronización del catálogo antes de que se produzca la sincronización programada por hora, puede forzar una resincronización.

>[!NOTE]
>
> Forzar una resincronización déclencheur una resincronización de todo el catálogo de productos, lo que puede aumentar la carga en los recursos de hardware.

1. En el panel _Sincronización de catálogo_, seleccione **Configuración**.

   Aparecerá la página _Configuración de sincronización de catálogos_.

1. En la sección _Sincronizar datos_, haga clic en [!UICONTROL Resync].

   [!DNL Commerce] sincroniza su catálogo durante la siguiente ventana de sincronización programada. En función del tamaño del catálogo, esta operación puede tardar mucho tiempo.

## Productos de catálogo sincronizados

La tabla **Productos de catálogo sincronizados** muestra la siguiente información.

| Campo | Descripción |
|---|---|
| ID | Identificador único del producto |
| Nombre | Nombre de tienda del producto |
| Tipo | Identifica el tipo de producto, como simple, configurable o descargable |
| Última exportación | Fecha en la que se exportó correctamente el producto del catálogo por última vez |
| Última modificación | Fecha de la última modificación del producto en el catálogo |
| SKU | Muestra la unidad de stock del producto |
| Precio | Precio del producto |
| Visibilidad | Configuración de visibilidad de un producto tal como se define en el catálogo [!DNL Commerce] |

## Resolver problemas de sincronización del catálogo {#resolvesync}

Consulte [Registros y solución de problemas](../data-export/troubleshooting-logging.md#troubleshooting) en la _Guía de exportación de datos SaaS_.
