---
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 27%
---

# Eliminar extensiones en conflicto

Si tiene instaladas cualquiera de las siguientes extensiones, desinstálelas antes de instalar [!DNL Adobe Commerce Optimizer Connector for B2B]:

* [!DNL Adobe Commerce Live Search] (`magento/live-search`)
* [!DNL Adobe Commerce Product Recommendations] (`magento/product-recommendations`)
* [!DNL Adobe Commerce Catalog Service] (`magento/catalog-service`, `magento/catalog-service-installer`)
* **[!UICONTROL Data Management Dashboard]** (`magento-catalog-sync-admin`)

Los datos asociados con estas extensiones siguen estando disponibles en la base de datos de Commerce. Sin embargo, no se exporta a [!DNL Commerce Optimizer] cuando el conector está habilitado. Para implementar las funcionalidades de búsqueda y comercialización de Adobe Commerce proporcionadas por estas extensiones después de habilitar el conector, configúrelas desde la [[!DNL Commerce Optimizer] IU del administrador](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour).

>[!IMPORTANT]
>
>Si no se quitan estas extensiones antes de habilitar el conector, se producirán pantallas de configuración dañadas, datos duplicados en [!DNL Commerce Optimizer] y errores de autenticación 401 o 403.