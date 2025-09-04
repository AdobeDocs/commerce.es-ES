---
title: '[!DNL Manage the Data Export extension]'
description: Obtenga información sobre cómo actualizar la extensión  [!DNL Data Export] y quitar o deshabilitar los servicios de exportación de datos que no son necesarios.
role: Admin, Developer
exl-id: 94702995-d272-47b9-9560-198eee3250a6
source-git-commit: c7a08cabe07ec94e31e9f4c27448ee0862e62cf2
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Administración de la extensión de exportación de datos SaaS

La extensión [!DNL data export] para los servicios SaaS es una colección de módulos que permiten la recopilación y sincronización de datos entre Adobe Commerce y los servicios de Commerce conectados.

Se incluyen módulos específicos en los metapaquetes para las extensiones de servicios de Adobe Commerce, como
como [Live Search](/help/live-search/overview.md), [Product Recommendations](/help/product-recommendations/overview.md) y [Servicio de catálogo](/help/catalog-service/overview.md). Si utiliza estos servicios, no se requiere ninguna instalación independiente para habilitar la extensión de exportación de datos.

## Eliminación o desactivación de las funciones de exportación de datos de Commerce

Si no necesita uno de los módulos de exportación de datos de comercio instalados, use el comando `magento:module:disable` CLI para deshabilitarlo.

Por ejemplo, existe una [API de categorías](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) que usa internamente los datos de fuentes de permisos de categorías. Si no utiliza esta API, puede deshabilitar la exportación de datos para la fuente de permisos para categorías.

```shell script
bin/magento module:disable Magento_CategoryPermissionDataExporter Magento_SaaSCategoryPermissions
```

### Actualización de un módulo a una versión específica

Puede actualizar cualquiera de los módulos de exportación de datos de comercio instalados mediante Composer. Por ejemplo, puede actualizar un módulo a una versión especificada y también actualizar las dependencias necesarias.

1. Inicie sesión en el servidor de aplicaciones de Commerce.

1. Desde la línea de comandos, actualice el módulo mediante Composer:

   ```bash
   composer require magento/commerce-data-export:103.4.11 --with-all-dependencies
   ```

Si la instancia de Commerce está implementada en la infraestructura de Cloud, actualice la extensión desde el directorio del proyecto de Cloud. Consulte [Actualizar una extensión](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension) en la _Guía de infraestructura de Adobe Commerce en la nube_.
