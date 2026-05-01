---
title: ¿Qué son las recomendaciones de productos?
description: Obtenga información acerca de Recomendaciones de productos en Adobe Commerce. Descubra las unidades de tienda impulsadas por IA, la privacidad, las rutas de administración y de tienda y la retención de datos clave.
recommendations: noCatalog
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
source-git-commit: 6bfc2c0ed53b44fb30a142dc87f87dca8a601a33
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 0%

---

# ¿Qué son [!DNL Product Recommendations]?

[!DNL Product Recommendations] te ayuda a mostrar recomendaciones de productos personalizadas en tiendas Adobe Commerce usando [Adobe AI](https://business.adobe.com/es/ai.html) y aprendizaje automático en el comportamiento agregado del comprador y tu catálogo. Esta descripción general abarca las restricciones de servicio (incluida la HIPAA), los datos y la privacidad, donde aparecen las unidades de recomendación, las rutas de implementación de tienda, cómo las recomendaciones complementan las relaciones de producto y la retención de datos de catálogo.

>[!IMPORTANT]
>
>**[!DNL Product Recommendations]no es un servicio compatible con HIPAA.** No habilite ni utilice [!DNL Product Recommendations] en ninguna implementación de Adobe Commerce que utilice la oferta compatible con HIPAA o que procese información médica protegida (PHI) de otro modo. [!DNL Product Recommendations] forma parte de los servicios SaaS de Commerce que están clasificados actualmente como no preparados para HIPAA.
>
>Para obtener detalles sobre qué funciones de Adobe Commerce están preparadas para HIPAA y qué servicios no se deben usar con PHI, consulte [Preparación para HIPAA en Adobe Commerce](https://experienceleague.adobe.com/es/docs/commerce-admin/start/compliance/hipaa-ready-service/overview) y [Operaciones](https://experienceleague.adobe.com/es/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services).

## Administración de datos y privacidad

La recopilación de datos de [!DNL Product Recommendations] no incluye información de identificación personal (PII). Todos los identificadores de usuario, como los ID de cookie y las direcciones IP, se anonimizan estrictamente. Para obtener más información, consulte la [Política de privacidad de Adobe](https://www.adobe.com/privacy/policy.html).

Para obtener más información acerca de la sincronización de datos, consulte [Panel de administración de datos](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=es).

## Dónde aparecen las recomendaciones

Las recomendaciones aparecen en la tienda como unidades con etiquetas como, por ejemplo, &quot;Los clientes que vieron este producto también vieron&quot;. Puede crear, administrar e implementar recomendaciones en las vistas de su tienda desde el administrador de Adobe Commerce. Si su proyecto de Commerce usa el [Conector de Adobe Commerce Optimizer](https://experienceleague.adobe.com/es/docs/commerce/aco-optimizer-connector/overview), usted crea, administra e implementa las recomendaciones a través de [Adobe Commerce Optimizer](../optimizer/overview.md).

## Implementaciones de tienda

Elija la documentación que coincida con su tienda:

- **PWA Studio** — [Documentación de PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)
- **front-end personalizado (por ejemplo, React o Vue.js)** — [Integrar [!DNL Product Recommendations]](headless.md) en una tienda sin encabezado
- **Commerce Edge Delivery Services (EDS)** — [Documentación de Adobe Commerce Storefront para EDS](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=es)

>[!NOTE]
>
>Las configuraciones sin encabezado y personalizadas varían según la pila. Esta área del producto documenta una ruta de PWA Studio y un patrón general de integración sin encabezado; no cubre todos los escenarios de terceros o personalizados.

## Recomendaciones de productos frente a relaciones de productos

Dadas las complejidades cambiantes de las compras en línea, lo que mejor funciona para su tienda a menudo es una combinación de múltiples tecnologías clave. El uso de [!DNL Product Recommendations] y [relaciones de producto](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html?lang=es) le proporciona más flexibilidad al promocionar productos. Puede aprovechar [!DNL Product Recommendations] con tecnología de Adobe AI para automatizar de manera inteligente sus recomendaciones a escala. Entonces, puede aprovechar [reglas de productos relacionadas](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html?lang=es) cuando tenga que intervenir manualmente y asegurarse de que se hace una recomendación específica a un segmento de destinatario o cuando se deban cumplir ciertos objetivos comerciales.

Las recomendaciones de productos le permiten:

- Elija entre nueve tipos de recomendaciones inteligentes distintos en función de las siguientes áreas: basado en compradores, basado en artículos, basado en popularidad, en tendencias y basado en similitudes
- Utilice datos de comportamiento para personalizar las recomendaciones en el recorrido de la tienda del comprador
- Mida las métricas clave relevantes para cada recomendación para ayudarle a comprender el impacto de sus recomendaciones

## Demostración de recomendaciones de productos

Vea este vídeo para obtener más información sobre [!DNL Product Recommendations]:

>[!VIDEO](https://video.tv.adobe.com/v/3449961?captions=spa&quality=12)

## Política de retención de datos del catálogo

El servicio [!DNL Product Recommendations] depende de los datos del catálogo que permanecen sincronizados con su entorno de Adobe Commerce. Los catálogos o entornos inactivos que dejan de consultar esos datos pueden entrar en hibernación, lo que afecta a lo que devuelve el servicio hasta que se reactiva.

Si no envía una consulta para los datos del catálogo en su entorno **testing** durante 90 días consecutivos, los datos del catálogo se establecerán en modo de hibernación y no se devolverá ningún dato para ninguna consulta. Los datos del catálogo en su entorno **production** no se ven afectados por la regla de 90 días.

Si su entorno tiene un **catálogo vacío** 45 días después de crearse, los datos del catálogo se establecen en modo de hibernación y no se devuelven datos para ninguna consulta. Esto se aplica tanto a los entornos de producción como de prueba.

### Reactivar datos de catálogo

Para restaurar los datos del catálogo después de la hibernación, [envíe una solicitud de soporte técnico](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page) con el título &quot;Reactivar [!DNL Product Recommendations]&quot; e incluya los identificadores de entorno. Los datos del catálogo deben restaurarse en un par de horas.
