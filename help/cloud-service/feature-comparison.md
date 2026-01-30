---
title: Comparación de SaaS y PaaS de Adobe Commerce
description: Compare los modelos de SaaS de Adobe Commerce con los de PaaS para determinar el mejor enfoque de implementación para sus necesidades comerciales.
feature: App Builder, GraphQL, Integration, Saas
role: Developer, Admin, Leader
level: Intermediate
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
source-git-commit: 5e4481dfd7259a07bda58a1e945b086e9f1c1805
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# Comparación de características

Adobe Commerce ofrece tres modelos de implementación:

- [!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."} [as a Cloud Service de Adobe Commerce](overview.md) (SaaS)
- [!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."} [Adobe Commerce en la nube](https://experienceleague.adobe.com/es/docs/commerce-on-cloud/user-guide/overview) (PaaS)
- [Adobe Commerce](https://experienceleague.adobe.com/es/docs/commerce-operations/installation-guide/overview) (local)

Esta comparación se centra en las diferencias entre los modelos de software como servicio (SaaS) y plataforma como servicio (PaaS). Estos modelos proporcionan diferentes niveles de personalización, extensibilidad y control sobre la implementación de Commerce.

>[!NOTE]
>
>El modelo local comparte capacidades similares con el modelo PaaS, por lo que esta comparación también se aplica al considerar SaaS en comparación con las implementaciones locales.

## Funciones de administración de tiendas

La [IU de administración de Commerce](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/guide-overview) es la interfaz principal para acceder a las funciones y administrar las operaciones de la tienda back-end, el inventario, los precios, las promociones y las interacciones con los clientes. Sin embargo, [!DNL Adobe Commerce as a Cloud Service] ofrece soluciones únicas que reemplazan algunas de las características conocidas disponibles en [!DNL Adobe Commerce on Cloud] y en los proyectos locales.

En la tabla siguiente se describen las características y las soluciones de reemplazo disponibles en [!DNL Adobe Commerce as a Cloud Service]:

<table>
    <thead>
        <tr>
            <th>Función</th>
            <th>Modelo PaaS [!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y proyectos locales."}</th>
            <th>Modelo SaaS [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Administración de recursos digitales</td>
            <td><a href="https://experienceleague.adobe.com/es/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">Galería de medios</a></td>
            <td><a href="../aem-assets-integration/overview.md">Visuales del producto</a></td>
        </tr>
        <tr>
            <td>Gestión de contenido</td>
            <td><a href="https://experienceleague.adobe.com/es/docs/commerce-admin/content-design/guide-overview">Sistema de administración de contenido (CMS)</a>, <a href="https://experienceleague.adobe.com/es/docs/commerce-admin/page-builder/guide-overview">Generador de páginas</a>, <a href="https://experienceleague.adobe.com/es/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">reescribe URL</a></td>
            <td><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/?lang=es">Storefront Builder</a></td>
        </tr>
        <tr>
            <td>Comercialización en catálogo</td>
            <td><a href="https://experienceleague.adobe.com/es/docs/commerce-admin/content-design/staging/content-staging">Ensayo de contenido</a>, <a href="https://experienceleague.adobe.com/es/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">Visual Merchandiser</a></td>
            <td><a href="../catalog-service/overview.md">Servicio de catálogo</a></td>
        </tr>
        <tr>
            <td>Pagos</td>
            <td><a href="https://experienceleague.adobe.com/es/docs/commerce-admin/stores-sales/payments/payments">Soluciones de pago</a></td>
            <td><a href="../payment-services/guide-overview.md">Servicios de pago</a></td>
        </tr>
        <tr>
            <td>Funcionalidad B2B</td>
            <td>Funciones B2B completas disponibles tras la instalación</td>
            <td>Preinstalado con las características principales B2B<sup>1</sup></td>
        </tr>
        <tr>
            <td>Experimentación</td>
            <td>Complemento para determinados niveles</td>
            <td>Pruebas A/B nativas para optimizar la participación y la conversión</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                Las <sup>1</sup> características principales de <a href="https://experienceleague.adobe.com/es/docs/commerce-admin/b2b/guide-overview">B2B</a>, como la administración de la empresa y las cotizaciones, están disponibles de forma predeterminada en SaaS. Sin embargo, las personalizaciones específicas del sector pueden requerir consideraciones de implementación adicionales.
            </td>
        </tr>
    </tfoot>
</table>

## Extensibilidad y funciones de plataforma

En la tabla siguiente se comparan las funciones de plataforma y las funciones de extensibilidad para ayudarle a comprender las diferencias y decidir el modelo que mejor se adapta a los requisitos de su empresa antes de iniciar una implementación.

<table>
    <thead>
        <tr>
            <th>Función</th>
            <th>Modelo PaaS [!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y proyectos locales."}</th>
            <th>Modelo SaaS [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Funcionalidades de Platform</strong></td>
        </tr>
        <tr>
            <td>Actualizaciones de funciones y seguridad</td>
            <td>Requiere actualización manual y aplicación de parches. Seis versiones de parches y una versión menor por año.</td>
            <td>Actualizado automáticamente por Adobe mediante un modelo SaaS sin versiones</td>
        </tr>
        <tr>
            <td>Infraestructura de alojamiento</td>
            <td>De un solo inquilino</td>
            <td>De varios inquilinos</td>
        </tr>
        <tr>
            <td>Rendimiento y escalabilidad</td>
            <td>Escalado automático horizontal para arquitectura a escala. Escalado automático vertical para el nivel web que se está implementando en el acceso anticipado para todos los comerciantes, incluida la arquitectura sin escalado.</td>
            <td>Aplicación nativa en la nube de varios inquilinos con escalado automático completo en toda la pila</td>
        </tr>
        <tr>
            <td>Observabilidad</td>
            <td>[!DNL New Relic] acceso para que los clientes supervisen y administren el entorno</td>
            <td>Gestionado por Adobe. Los clientes pueden usar [!DNL OpenTelemetry] para [!DNL App Builder] aplicaciones y paneles de RUM para la tienda. No se incluye la licencia [!DNL New Relic]. Los clientes pueden configurar [!DNL API Mesh] y [!DNL App Builder] para enviar datos a su propia cuenta de [!DNL New Relic].</td>
        </tr>
        <tr>
            <td>CDN</td>
            <td>[!DNL Fastly] incluido</td>
            <td>CDN de Edge totalmente administrado junto con Commerce Storefront. También se admite BYO-CDN.</td>
        </tr>
        <tr>
            <td>Seguridad y cumplimiento</td>
            <td>SOC2, PCI, certificaciones ISO por proveedor de alojamiento, HIPAA</td>
            <td>SOC2, PCI, ISO, RGPD. HIPAA actualmente no disponible.</td>
        </tr>
        <tr>
            <td>Recuperación ante desastres y SLA</td>
            <td>99,99% infraestructura, 99,9% aplicación (Managed Services)</td>
            <td>99,9% (infraestructura y aplicación), RPO/RTO más rápido</td>
        </tr>
        <tr>
            <td>Regiones de alojamiento</td>
            <td>Azure (24 ubicaciones), AWS (22 ubicaciones), GCP (8 ubicaciones, no estándar)</td>
            <td>Disponible globalmente. Para obtener información sobre los entornos de producción de su región, póngase en contacto con su representante de servicio de atención al cliente. Ubicaciones adicionales desplegadas según la demanda.</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Personalización de administración de Commerce</strong></td>
        </tr>
        <tr>
            <td>Extensibilidad de Admin Console</td>
            <td>Personalización y temas PHP, extensibilidad de App Builder (recomendado)</td>
            <td>Extensibilidad de App Builder</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Extensibilidad</strong></td>
        </tr>
        <tr>
            <td>Modelo de extensibilidad</td>
            <td>En proceso (personalización PHP) y fuera de proceso (recomendado: API, eventos, App Builder)</td>
            <td>Solo fuera de proceso (API, eventos, App Builder)</td>
        </tr>
        <tr>
            <td>API web ampliables</td>
            <td>Extensibilidad nativa de REST/GraphQL y malla de API con solucionadores personalizados</td>
            <td>Malla de API con solucionadores personalizados</td>
        </tr>
        <tr>
            <td>Extensibilidad del modelo de datos</td>
            <td>Personalización completa del modelo de datos</td>
            <td>Atributos personalizados para entidades principales y B2B<sup>1</sup></td>
        </tr>
        <tr>
            <td>Tecnologías</td>
            <td>CSS, CLI, HTML, JS, PHP, XML</td>
            <td>CSS, CLI, HTML, JS, nodo</td>
        </tr>
        <tr>
            <td>App Marketplace</td>
            <td>[[!DNL Magento Marketplace]](https://marketplace.magento.com/) (extensiones PHP) y [[!DNL Exchange Marketplace]](https://commercemarketplace.adobe.com) para [!DNL App Builder] aplicaciones (recomendado)</td>
            <td>[!DNL App Builder] aplicaciones de [[!DNL Exchange Marketplace]](https://commercemarketplace.adobe.com)</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Datos y almacenamiento</strong></td>
        </tr>
        <tr>
            <td>Personalizaciones del índice de búsqueda</td>
            <td>Personalización de búsqueda nativa</td>
            <td>Requiere soluciones de terceros</td>
        </tr>
        <tr>
            <td>Tipos de correo electrónico personalizados</td>
            <td>Personalización completa del correo electrónico</td>
            <td>Solo plantillas de correo electrónico estándar</td>
        </tr>
        <tr>
            <td>Almacenamiento de datos personalizado</td>
            <td>DB, archivo, caché, cola</td>
            <td>La biblioteca de estado de App Builder (solo archivo)<sup>2 - <a href="https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/database">Almacenamiento de la base de datos para App Builder</a> se encuentra actualmente en acceso anticipado.</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> La extensibilidad del modelo de datos en SaaS admite <a href="https://developer.adobe.com/commerce/webapi/graphql/schema/attributes/mutations/">la ampliación de entidades principales</a> más allá del producto y el cliente, incluidas las entidades B2B. Sin embargo, los modelos de datos específicos del sector (por ejemplo, los atributos específicos de los distribuidores) podrían requerir consideraciones arquitectónicas adicionales.
                <br><br>
                <sup>2</sup> Adobe está trabajando activamente en la integración de Document DB para abordar las necesidades de almacenamiento persistentes para SaaS. En la actualidad, las implementaciones que requieren almacenamiento de datos a largo plazo pueden necesitar aprovisionar y mantener una infraestructura adicional.
            </td>
        </tr>
    </tfoot>
</table>

>[!NOTE]
>
>Cuando se considere la posibilidad de migrar a SaaS, Adobe recomienda lo siguiente:
>
>- Mueva la funcionalidad adecuada a la extensibilidad fuera de proceso siempre que sea posible.
>- Reduzca la superficie que requiere transición.
>- Considere [!DNL API Mesh] para ampliar la funcionalidad de la API.
>- Monitorice la evolución continua de la plataforma de Adobe y las nuevas versiones de capacidades.
>- Evaluar los requisitos del modelo de datos específico del sector con respecto a las opciones de extensibilidad disponibles.
>- Considere la posibilidad de adoptar [servicios de comercialización ofrecidos por vistas del catálogo y directivas](../optimizer/setup/catalog-view.md).
