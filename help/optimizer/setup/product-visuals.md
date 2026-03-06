---
title: Imágenes del producto con AEM Assets
description: Aprenda a utilizar AEM Assets para imágenes de productos en  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
role: Admin, Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
source-git-commit: c7c21df464685783b5fae1c99d60ca91e0c334d2
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---


# Imágenes del producto con AEM Assets

Product Visuals permite que [!DNL Adobe Commerce Optimizer] comerciantes administren imágenes de productos a través de Adobe Experience Manager (AEM) Assets. Esta integración proporciona un flujo de trabajo perfecto para sincronizar imágenes de productos de alta calidad de los AEM Assets al catálogo [!DNL Commerce Optimizer] mediante capas de catálogo.

## Ventajas principales

* **Administración centralizada de recursos**: administre todas las imágenes de productos en AEM Assets, la solución de administración de recursos digitales de nivel empresarial.
* **Sincronización automática**: las imágenes de productos se sincronizan automáticamente cuando los recursos se aprueban o actualizan en los AEM Assets.
* **Entrega de Dynamic Media**: Aproveche Dynamic Media con las capacidades de OpenAPI para ofrecer imágenes optimizadas.
* **Capas de catálogo**: las imágenes de producto se aplican como una capa de catálogo, lo que permite superponer las imágenes de los AEM Assets en el catálogo base.

## Cómo funciona

La integración tiene dos flujos principales:

* **De AEM Assets**: cuando se aprueba, rechaza o elimina un recurso, el evento fluye a través de la canalización de Adobe al servicio de integración de Assets. El servicio hace coincidir recursos con productos mediante una estrategia de coincidencia de `match-by-SKU` o personalizada y, a continuación, envía las asignaciones de `product-asset` a [!DNL Commerce Optimizer], donde se almacenan como capas de producto.

* **Desde ACO**: Cuando se actualiza un producto en [!DNL Commerce Optimizer], el evento fluye a través de la canalización de Adobe hasta el servicio de integración de Assets. El servicio sincroniza cualquier asignación de recursos coincidente con ACO.

Las imágenes actualizadas están disponibles a través de las API de tienda (servicio de catálogo, Live Search, recomendaciones de productos).

### Configuración de Source y capas

Las imágenes de los AEM Assets se incorporan como una capa de catálogo con la siguiente configuración de origen:

> Ejemplo de configuración de origen

```json
{
  "source": {
    "locale": "en-US",
    "layer": "AEM-Assets"
  }
}
```

Esta configuración garantiza que las imágenes de los AEM Assets se apliquen como una superposición en el catálogo de productos base.

## Requisitos previos

Antes de habilitar los elementos visuales del producto, asegúrese de cumplir los [requisitos previos de Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md#prerequisites).

## Configurar

Para habilitar la integración, [cree un vale de soporte técnico](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) con los detalles de [!DNL Commerce Optimizer] y los AEM Assets. El Soporte de Adobe configura la integración y registra su inquilino con el Servicio de integración de Assets.

Consulte [Configuración de AEM Assets para Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md) para obtener información sobre la incorporación.

### Configuración de metadatos de AEM Assets

Para habilitar la coincidencia automática de productos, configure los recursos en AEM Assets con metadatos de Commerce.

Consulte [Configuración de AEM Assets](../../aem-assets-integration/get-started/configure-aco.md#configure-aem-assets) para ver los campos y pasos de metadatos requeridos.

## Uso de elementos visuales del producto

Una vez configurada la integración, administre las imágenes de producto con los AEM Assets.

### Añadir imágenes a los productos

1. Cargue imágenes en el repositorio de AEM Assets.

1. Añada metadatos de Commerce al recurso. Consulte [Aplicar metadatos a recursos](../../aem-assets-integration/get-started/configure-aco.md#step-3-apply-metadata-to-assets).

1. Apruebe el recurso para su envío. El recurso debe estar en estado **aprobado** para sincronizar el déclencheur.

1. La imagen se sincroniza automáticamente con [!DNL Commerce Optimizer].

### Aplicación de la capa AEM-Assets

Para mostrar imágenes de AEM Assets en tu tienda, [asigna la capa `AEM-Assets` a tu vista de catálogo](catalog-layer.md#assign-the-aem-assets-layer-to-a-catalog-view).

## Más parecido a esto

* [Capas de catálogo](catalog-layer.md)
* [Vistas de catálogo](catalog-view.md)
* [Guía de integración de AEM Assets](../../aem-assets-integration/overview.md)
