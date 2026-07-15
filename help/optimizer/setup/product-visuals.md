---
title: Imágenes del producto con AEM Assets
description: Aprenda a utilizar AEM Assets para imágenes de productos en  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
role: Admin, Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
source-git-commit: 264658bee09a22cfd55828c6960153cc1239d3fb
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# Imágenes del producto con AEM Assets

Product Visuals permite que [!DNL Adobe Commerce Optimizer] comerciantes administren imágenes de productos a través de Adobe Experience Manager (AEM) Assets. Esta integración proporciona un flujo de trabajo perfecto para sincronizar imágenes de productos de alta calidad de los AEM Assets al catálogo [!DNL Commerce Optimizer] mediante capas de catálogo.

>[!NOTE]
>
>**Product Visuals** es el nombre del paquete proporcionado con [!DNL Adobe Commerce as a Cloud Service] y [!DNL Adobe Commerce Optimizer]. Combina [Dynamic Media con funciones OpenAPI](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview) y [Prime para AEM Assets](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-prime).
>
>Los clientes con una licencia de AEM Assets diferente (por ejemplo, **AEM Assets Ultimate**) pueden usar la misma integración; solo la versión de AEM afecta a los pasos de incorporación, no al tipo de licencia.

## Ventajas principales

* **Administración centralizada de recursos**: administre todas las imágenes de productos en AEM Assets, la solución de administración de recursos digitales de nivel empresarial.
* **Sincronización automática**: las imágenes de productos se sincronizan automáticamente cuando los recursos se aprueban o actualizan en los AEM Assets.
* **Entrega de Dynamic Media**: Aproveche Dynamic Media con las capacidades de OpenAPI para ofrecer imágenes optimizadas.
* **Capas de catálogo**: las imágenes de producto se aplican como una capa de catálogo, lo que permite superponer las imágenes de los AEM Assets en el catálogo base.

## Cómo funciona

La integración tiene dos flujos de eventos independientes. Ambos usan [Adobe I/O Events](https://developer.adobe.com/events/docs/) para transferir eventos al servicio de integración de Assets, pero cada dirección usa su propio proveedor de eventos:

* **De AEM Assets al servicio de integración de Assets**: cuando se aprueba, rechaza o elimina un recurso, el evento se envía al servicio de integración de Assets. El servicio hace coincidir recursos con productos mediante una estrategia de coincidencia `match-by-SKU` o personalizada y, a continuación, envía las asignaciones `product-asset` a [!DNL Commerce Optimizer], donde se almacenan como capas de producto.

* **De [!DNL Commerce Optimizer] al servicio de integración de Assets**: cuando se actualiza un producto en [!DNL Commerce Optimizer], el evento se entrega al servicio de integración de Assets. El servicio sincroniza todas las asignaciones de recursos coincidentes con [!DNL Commerce Optimizer].

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

Para habilitar la integración, [cree un vale de soporte técnico](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/help-and-support/create-a-support-ticket) con los detalles de [!DNL Commerce Optimizer] y los AEM Assets. El Soporte de Adobe configura la integración y registra su inquilino con el Servicio de integración de Assets.

Consulte [Configuración de AEM Assets para Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md) para obtener información sobre la incorporación.

### Configuración de metadatos de AEM Assets

Para habilitar la coincidencia automática de productos, configure los recursos en AEM Assets con metadatos de Commerce.

Consulte [Configuración de AEM Assets](../../aem-assets-integration/get-started/configure-aco.md#configure-aem-assets-first) para ver los campos y pasos de metadatos requeridos.

## Limitaciones

Antes de usar los elementos visuales del producto, revise las [limitaciones de integración](../../aem-assets-integration/get-started/configure-aco.md#limitations): las restricciones relacionadas con la capa que afectan a la forma en que los datos de los AEM Assets se combinan con el catálogo base.

Para las asignaciones de capacidad y uso (almacenamiento de recursos, operaciones de Dynamic Media, licencias de usuario), consulte [Límites visuales del producto](../boundaries-limits.md#product-visuals-limits) en la guía _Límites y límites_.

## Uso de elementos visuales del producto

Una vez configurada la integración, administre las imágenes de producto con los AEM Assets.

### Añadir imágenes a los productos

1. Cargue imágenes en el repositorio de AEM Assets.

1. Añada metadatos de Commerce al recurso.

   Ver [Coincidencia automática predeterminada](../../aem-assets-integration/synchronize/default-match.md) y [Coincidencia automática personalizada](../../aem-assets-integration/synchronize/custom-match.md).

1. Apruebe el recurso para su envío. El recurso debe estar en estado **aprobado** para sincronizar el déclencheur.

1. La imagen se sincroniza automáticamente con [!DNL Commerce Optimizer].

### Aplicación de la capa AEM-Assets

Para mostrar imágenes de AEM Assets en tu tienda, [asigna la capa `AEM-Assets` a tu vista de catálogo](catalog-layer.md#assign-the-aem-assets-layer-to-a-catalog-view).

## Más parecido a esto

* [Capas de catálogo](catalog-layer.md)
* [Vistas de catálogo](catalog-view.md)
* [Guía de integración de AEM Assets](../../aem-assets-integration/overview.md)
