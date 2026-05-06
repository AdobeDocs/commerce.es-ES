---
title: Límites y límites de integración
description: Conozca los límites de ámbito de los catálogos de terceros, la cobertura de corrección automática, la rastrea de requisitos previos, las consideraciones de escala empresarial y las restricciones de acceso beta restringidas para LLM Optimizer con Commerce.
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Límites y límites de integración

>[!IMPORTANT]
>
>El acceso a esta integración está restringido. Póngase en contacto con el administrador de cuentas técnico para obtener más información.

Utilice este tema para establecer expectativas sobre lo que la integración de [!DNL Adobe Commerce] y [!DNL Adobe LLM Optimizer] puede automatizar, dónde usted sigue siendo responsable y qué restricciones siguen evolucionando.

## Limitaciones del catálogo de terceros {#third-party-catalog}

Si el catálogo **no** se encuentra en [!DNL Adobe Commerce]:

- LLM Optimizer aún puede identificar problemas y sugerir mejoras utilizando datos de catálogo duplicados o importados, según la configuración.
- **La corrección automática directa** en la plataforma de comercio del comerciante no es lo mismo que escribir en el catálogo de origen del comerciante. Es posible que necesite un catálogo espejo, una exportación/importación o una automatización de socios para aplicar los cambios.

Para los catálogos alojados en Commerce, las actualizaciones de nombre y descripción aprobadas se dirigen al sistema de registro de Commerce. Ver [Usar LLM Optimizer con Adobe Commerce](get-started/use-llmo-with-commerce.md).

## Escala y límites técnicos {#scale-limits}

Los catálogos grandes y los recuentos altos de URL pueden sobrecargar los patrones de rastrea, análisis e implementación de Edge.

## Rastrear y legibilidad de bots {#crawling}

Las perspectivas significativas del catálogo y el PDP suponen que los **bots relevantes para LLM pueden acceder** a las URL que le interesan y que las páginas están estructuradas de modo que el análisis automatizado sea fiable. Las reglas, la autenticación, el bloqueo geográfico y la personalización avanzada de los robots pueden reducir la cobertura.

## Temas relacionados

- [Resumen de integración](overview.md)
- [Conectar Adobe Commerce a LLM Optimizer](get-started/connect-to-llmo.md)
- [Uso de LLM Optimizer con Adobe Commerce](get-started/use-llmo-with-commerce.md)
