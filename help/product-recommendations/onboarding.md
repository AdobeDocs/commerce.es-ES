---
title: Incorporación
description: Conozca los requisitos y las plataformas compatibles en  [!DNL Product Recommendations].
exl-id: 7b8a1117-b6d5-4e5d-bb97-09f76a024cbd
TQID: https://experienceleague.adobe.com/FLrOFe-Lwe7i3dOwCISflVGEv2MIkXmmE-NqTvpaY-0
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 0802d0e53a1ed6701318647b7bf78435082ad5f3
workflow-type: tm+mt
source-wordcount: 477
ht-degree: 0%

---

# Incorporación

>[!IMPORTANT]
>
>**Recomendaciones de productos no es un servicio compatible con HIPAA.** No habilite ni utilice Recomendaciones de productos en ninguna implementación de Adobe Commerce que utilice la oferta compatible con HIPAA o que procese de otro modo información médica protegida (PHI). Product Recommendations forma parte de los servicios SaaS de Commerce que actualmente están clasificados como no preparados para HIPAA.
>
>Para obtener detalles sobre qué funciones de Adobe Commerce están preparadas para HIPAA y qué servicios no se deben usar con PHI, consulte [Preparación para HIPAA en Adobe Commerce](https://experienceleague.adobe.com/es/docs/commerce-admin/start/compliance/hipaa-ready-service/overview) y [Operaciones](https://experienceleague.adobe.com/es/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services).

El proceso de incorporación de [!DNL Product Recommendations] requiere acceso a la línea de comandos del servidor y consta de los siguientes pasos. Si no está familiarizado con el trabajo desde la línea de comandos, pida ayuda a un desarrollador o integrador de sistemas.

- [Flujo de trabajo de implementación](implementation-workflow.md)
- [Instalar y configurar](install-configure.md)
- [Configuración](settings.md)
- [Verificar](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify)
- [Entorno de ensayo](staging-environment.md)

## Requisitos

[Adobe Commerce](https://business.adobe.com/es/products/magento/magento-commerce.html) 2.4.4+. Para obtener más información, consulte [Requisitos del sistema](https://experienceleague.adobe.com/es/docs/commerce-operations/installation-guide/system-requirements){target="_blank"}.

### Plataformas compatibles

- Adobe Commerce on premise (EE) : 2.4.4+
- Adobe Commerce en la nube (ECE) : 2.4.4+

Para ver los requisitos detallados, consulte [Requisitos del sistema](https://experienceleague.adobe.com/es/docs/commerce-operations/installation-guide/system-requirements).

## Extremo

[!DNL Product Recommendations] se comunica a través del extremo en `https://catalog-service.adobe.io/graphql`.

### Compatibilidad con Page Builder

[!DNL Product Recommendations] se puede agregar a una página como tipo de contenido de Page Builder. Para agregar compatibilidad con Page Builder a Product Recommendations, consulte [Instalar y configurar](install-configure.md).

Consulte [[!DNL Page Builder] Integración](page-builder.md) para obtener instrucciones sobre cómo agregar [!DNL Product Recommendations] al contenido de [!DNL Page Builder].

### Optimización de imagen rápida

[!DNL Product Recommendations] admite un módulo [Fastly Image Optimization](install-configure.md#fastlysupport) opcional que aplica parámetros de Fastly Image Optimization a [!DNL Product Recommendations] direcciones URL de imagen. Para agregar esta compatibilidad, consulte [Instalar y configurar](install-configure.md#fastlysupport).

### Indexación de precios de SaaS

Los clientes de Product Recommendations pueden usar la [indexación de precios SaaS](../price-index/price-indexing.md), que ofrece cambios de precios más rápidos, actualizaciones y tiempo de sincronización.

### Compatibilidad con B2B {#b2bsupport}

Las tiendas B2B a menudo requieren una lógica compleja que dicta la visibilidad del producto y los precios para cada comprador o grupo de clientes. [!DNL Product Recommendations] ahora [admite](release-notes.md) esta funcionalidad al cumplir [permisos de categoría](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/categories/category-permissions), [catálogos compartidos](https://experienceleague.adobe.com/es/docs/commerce-admin/b2b/shared-catalogs/catalog-shared) y [precios específicos de grupos de clientes](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/products/pricing/pricing-advanced). Por ejemplo, si ha ocultado determinadas categorías del segmento de clientes minoristas, a un comprador de ese segmento no se le muestran recomendaciones para productos de esas categorías. Además, al definir un catálogo compartido para grupos de clientes y empresas específicos, esos compradores ven recomendaciones solo para los productos a los que pueden acceder. Todos los productos recomendados reflejan el precio correcto específico del grupo de clientes en función del grupo de clientes de cada comprador.

>[!NOTE]
>
>Los comerciantes pueden personalizar y ampliar widgets o elementos de tienda mediante la API de tienda [Servicio de catálogo](../catalog-service/overview.md), pero cualquier personalización está fuera del ámbito para el equipo de soporte de Adobe.
