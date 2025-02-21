---
title: Desarrollo del administrador de recomendaciones de productos
description: Descripción general de la arquitectura de recomendaciones de productos y las funciones de desarrollo.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Desarrollo del administrador de recomendaciones de productos

Las recomendaciones de productos son una potente herramienta de marketing que puede utilizar para aumentar las conversiones, aumentar los ingresos y estimular la participación del comprador. Las recomendaciones de productos aparecen en la tienda en forma de unidades como &quot;Los clientes que vieron este producto también vieron&quot;, &quot;Los clientes que compraron este producto también compraron&quot;, &quot;Recomendado para ti&quot;, etc. Las recomendaciones de productos de Adobe Commerce están equipadas con la tecnología [Adobe Sensei](https://www.adobe.com/sensei.html), que usa inteligencia artificial y algoritmos de aprendizaje automático para realizar un análisis profundo de los datos agregados del comprador. Estos datos, cuando se combinan con su catálogo de Commerce, generan experiencias muy atractivas, relevantes y personalizadas para el comprador.

>[!NOTE]
>
>Si su tienda está implementada con PWA Studio, consulte la [documentación de PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Si usa tecnología de front-end personalizada, como React o Vue JS, consulte la guía del usuario para aprender a integrar Product Recommendations en un entorno [sin encabezado](headless.md). Las instancias sin encabezado deben implementar eventos para potenciar el espacio de trabajo de recomendaciones de productos.

## Información general de arquitectura

En un nivel superior, Commerce Product Recommendations se implementa como SaaS. El lado de Commerce incluye la tienda, que contiene el recopilador de eventos y la plantilla de diseño Recommendations, y el back-end, que incluye los servicios de datos, el módulo de exportación de SaaS y la IU de administración. Los servicios de inteligencia de Adobe Sensei se aprovechan del lado del SaaS.

![Diagrama de arquitectura de recomendaciones de productos](assets/arch-diag-sensei.svg)

Una vez instalados y configurados los módulos de recomendación, la tienda empezará a recopilar datos de comportamiento. Adobe Sensei procesa estos datos de comportamiento junto con los datos del catálogo y calcula las asociaciones de productos que aprovecha el servicio de Recommendations. En este punto, el comerciante puede crear, administrar e implementar unidades de recomendación de productos en su tienda directamente desde la IU de administración.

## Pasos siguientes

Lea los temas siguientes para empezar a usar Product Recommendations:

- [Implementación de recomendaciones de productos](implementation-workflow.md)

- [Instalación y configuración de Recommendations de productos](install-configure.md)

- [Crear recomendaciones de productos](create.md)
