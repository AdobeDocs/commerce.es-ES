---
title: Introducción a  [!DNL Product Recommendations]
description: '[!DNL Product Recommendations] es una potente herramienta de marketing que puede usar para aumentar las conversiones, aumentar los ingresos y estimular la participación del comprador.'
recommendations: noCatalog
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# Introducción a [!DNL Product Recommendations]

Las recomendaciones de productos son una potente herramienta de marketing que puede utilizar para aumentar las conversiones, aumentar los ingresos y estimular la participación del comprador. Las recomendaciones de productos de Adobe Commerce están equipadas con [Adobe AI](https://business.adobe.com/es/ai.html), que usa inteligencia artificial y algoritmos de aprendizaje automático para realizar un análisis profundo de los datos agregados de visitantes. Estos datos, cuando se combinan con su catálogo de Adobe Commerce, resultan en una experiencia muy atractiva, relevante y personalizada.

Las recomendaciones de productos aparecen en la tienda como unidades con etiquetas como, por ejemplo, &quot;Los clientes que vieron este producto también vieron&quot;. Puede crear, administrar e implementar recomendaciones en las vistas de su tienda directamente desde el administrador de Adobe Commerce.

Si su tienda está implementada con PWA Studio, consulte la [documentación de PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Si usas una tecnología de front-end personalizada como React o Vue JS, aprende a [integrar](headless.md) [!DNL Product Recommendations] en tu tienda sin encabezado.

>[!NOTE]
>
>Existen muchas maneras de desarrollar una implementación sin encabezado o personalizada. En esta guía se describe una forma de hacerlo, utilizando PWA Studio. No cubre todos los escenarios o eventualidades.

## Privacidad

La recopilación de datos a los efectos de [!DNL Product Recommendations] no incluye información de identificación personal (PII). Además, todos los identificadores de usuario, como los ID de cookie y las direcciones IP, se anonimizan estrictamente. Para obtener más información, consulte la [Política de privacidad de Adobe](https://www.adobe.com/privacy/policy.html).

[!DNL Product Recommendations] usuarios pueden consultar [Panel de administración de datos](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=es) para obtener más datos sobre la sincronización de datos.

## Recomendaciones de productos frente a relaciones de productos

Dadas las complejidades cambiantes de las compras en línea, lo que mejor funciona para su tienda a menudo es una combinación de múltiples tecnologías clave. El uso de [!DNL Product Recommendations] y [relaciones de producto](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html?lang=es) le proporciona más flexibilidad al promocionar productos. Puede aprovechar [!DNL Product Recommendations] con la tecnología de Adobe AI para automatizar de forma inteligente sus recomendaciones a escala. Entonces, puede aprovechar [reglas de productos relacionadas](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html?lang=es) cuando tenga que intervenir manualmente y asegurarse de que se hace una recomendación específica a un segmento de destinatario o cuando se deban cumplir ciertos objetivos comerciales.

Las recomendaciones de productos le permiten:

- Elija entre nueve tipos de recomendaciones inteligentes distintos en función de las siguientes áreas: basado en compradores, basado en artículos, basado en popularidad, en tendencias y basado en similitudes
- Utilice datos de comportamiento para personalizar las recomendaciones en el recorrido de la tienda del comprador
- Mida las métricas clave relevantes para cada recomendación para ayudarle a comprender el impacto de sus recomendaciones

## Demostración de [!DNL Product Recommendations]

Vea este vídeo para obtener más información sobre [!DNL Product Recommendations]:

>[!VIDEO](https://video.tv.adobe.com/v/3449961?captions=spa&quality=12)

## Política de retención de datos del catálogo

Si no envía una consulta para los datos del catálogo en el entorno de prueba durante 90 días consecutivos, los datos del catálogo se establecen en modo de hibernación y no se devuelve ningún dato para ninguna consulta. Esta directiva no afecta a los datos de catálogo del entorno de producción.

Para reactivar los datos del catálogo en su entorno de prueba, [envíe una solicitud de soporte técnico](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page) con el título: &quot;Reactivar [!DNL Product Recommendations]&quot; e incluya los identificadores de entorno. Los datos del catálogo en el entorno de prueba deben restaurarse en un par de horas.
