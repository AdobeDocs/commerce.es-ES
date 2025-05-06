---
title: Incorporación
description: Conozca los requisitos y las plataformas compatibles en  [!DNL Product Recommendations].
exl-id: 7b8a1117-b6d5-4e5d-bb97-09f76a024cbd
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Incorporación

El proceso de incorporación de [!DNL Product Recommendations] requiere acceso a la línea de comandos del servidor y consta de los siguientes pasos. Si no está familiarizado con el trabajo desde la línea de comandos, pida ayuda a un desarrollador o integrador de sistemas.

- [Flujo de trabajo de implementación](implementation-workflow.md)
- [Instalar y configurar](install-configure.md)
- [Configuración](settings.md)
- [Verificar](verify.md)
- [Entorno de ensayo](staging-environment.md)

## Requisitos

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2
- Compositor 2

### Plataformas compatibles

- Adobe Commerce on premise (EE) : 2.4.4+
- Adobe Commerce en la nube (ECE) : 2.4.4+

## Extremo

[!DNL Product Recommendations] se comunica a través del extremo en `https://catalog-service.adobe.io/graphql`.

### Compatibilidad con Page Builder

[!DNL Product Recommendations] se puede agregar a una página como tipo de contenido de Page Builder. Para agregar compatibilidad con Page Builder a Product Recommendations, consulte [Instalar y configurar](install-configure.md).

Consulte [[!DNL Page Builder] Integración](page-builder.md) para obtener instrucciones sobre cómo agregar [!DNL Product Recommendations] al contenido de [!DNL Page Builder].

### Indexación de precios de SaaS

Los clientes de Product Recommendations pueden usar la [indexación de precios SaaS](../price-index/price-indexing.md), que ofrece cambios de precios más rápidos, actualizaciones y tiempo de sincronización.

### Compatibilidad con B2B {#b2bsupport}

Las tiendas B2B a menudo requieren una lógica compleja que dicta la visibilidad del producto y los precios para cada comprador o grupo de clientes. [!DNL Product Recommendations] ahora [admite](release-notes.md) esta funcionalidad al cumplir [permisos de categoría](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html?lang=es), [catálogos compartidos](https://experienceleague.adobe.com/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html?lang=es) y [precios específicos de grupos de clientes](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=es). Por ejemplo, si ha ocultado ciertas categorías del segmento de clientes minoristas, a un comprador de ese segmento no se le mostrarían recomendaciones para productos de esas categorías. Además, al definir un catálogo compartido para grupos de clientes y empresas específicos, esos compradores ven recomendaciones solo para los productos a los que pueden acceder. Todos los productos recomendados reflejan el precio correcto específico del grupo de clientes en función del grupo de clientes de cada comprador.

>[!NOTE]
>
>Los comerciantes pueden personalizar y ampliar widgets o elementos de tienda mediante la API de tienda [Servicio de catálogo](../catalog-service/overview.md), pero cualquier personalización está fuera del ámbito para el equipo de soporte de Adobe.
