---
title: Comparación de SaaS y PaaS de Adobe Commerce
description: Compare los modelos de SaaS de Adobe Commerce con los de PaaS para determinar el mejor enfoque de implementación para sus necesidades comerciales.
role: Architect
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
source-git-commit: 0eb74c1e70ac2c7073f8f9387baec4f6d3e90a86
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Comparación de características

Adobe Commerce ofrece tres modelos de implementación:

- [!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."} [as a Cloud Service de Adobe Commerce](overview.md) (SaaS)
- [!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."} [Adobe Commerce en la nube](https://experienceleague.adobe.com/es/docs/commerce-on-cloud/user-guide/overview) (PaaS)
- [Adobe Commerce](https://experienceleague.adobe.com/es/docs/commerce-operations/installation-guide/overview) (local)

Esta comparación se centra en las diferencias entre los modelos de software como servicio (SaaS) y plataforma como servicio (PaaS), que proporcionan diferentes niveles de personalización, extensibilidad y control sobre la implementación comercial.

>[!NOTE]
>
>El modelo local comparte capacidades similares con el modelo PaaS, por lo que esta comparación también se aplica al considerar SaaS en comparación con las implementaciones locales.

## Funciones de administración de tiendas

La [IU de administración de Commerce](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/guide-overview) es la interfaz principal para acceder a las funciones y administrar las operaciones de la tienda back-end, el inventario, los precios, las promociones y las interacciones con los clientes. Sin embargo, [!DNL Adobe Commerce as a Cloud Service] ofrece soluciones únicas que reemplazan algunas de las características conocidas disponibles en Adobe Commerce en proyectos en la nube y locales.

En la tabla siguiente se describen las características y las soluciones de reemplazo disponibles en [!DNL Adobe Commerce as a Cloud Service]:

<table>
    <thead>
        <tr>
            <th>Modelo PaaS [!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y proyectos locales."}</th>
            <th>Modelo SaaS [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."}</th>
            <th>Detalles</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="https://experienceleague.adobe.com/es/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">Administración de recursos digitales</a></td>
            <td><a href="../product-visuals/overview.md">Visuales del producto</a></td>
            <td>Un sistema sólido de administración de activos digitales (DAM) que se integra con Adobe Experience Manager para administrar contenido con medios enriquecidos. Como alternativa, la función predeterminada de administración de recursos y archivos digitales proporciona herramientas básicas de administración de recursos para almacenar y administrar recursos digitales.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/es/docs/commerce-admin/content-design/guide-overview">Sistema de administración de contenido (CMS)</a></td>
            <td rowspan="3"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/?lang=es">Storefront Builder</a></td>
            <td rowspan="3">Un CMS que permite a los usuarios crear y administrar fácilmente el contenido de la tienda mediante la creación de documentos o un editor visual, e incluye capacidades de experimentación nativas.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/es/docs/commerce-admin/page-builder/guide-overview">Page Builder</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/es/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">Reescrituras de URL</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/es/docs/commerce-admin/content-design/staging/content-staging">Ensayo de contenido</a></td>
            <td rowspan="2"><a href="../catalog-service/overview.md">Servicio de catálogo</a></td>
            <td rowspan="2">Un servicio de modelo de vista enriquecido (solo lectura) para administrar datos de catálogo y procesar experiencias de tienda relacionadas con el producto.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/es/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">Visual Merchandiser</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/es/docs/commerce-admin/stores-sales/payments/payments">Pagos</a></td>
            <td><a href="../payment-services/guide-overview.md">Servicios de pago</a></td>
            <td>Un servicio de pago integrado que facilita transacciones seguras y eficientes.</td>
        </tr>
    </tbody>
</table>

## Extensibilidad y funciones de plataforma

La siguiente tabla compara las funcionalidades de la plataforma y las funciones de extensibilidad para ayudarle a comprender las diferencias y tomar una decisión informada sobre qué modelo se adapta mejor a sus necesidades comerciales antes de iniciar una implementación.

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
            <td>Funcionalidad B2B</td>
            <td>Funciones B2B completas disponibles tras la instalación</td>
            <td>Preinstalado con las características principales B2B<sup>1</sup></td>
        </tr>
        <tr>
            <td>Experimentación</td>
            <td>Complemento para determinados niveles</td>
            <td>Pruebas A/B para optimizar la participación y la conversión</td>
        </tr>
        <tr>
            <td>Actualizaciones de funciones y seguridad</td>
            <td>Requiere actualización manual y parches</td>
            <td>Implementado automáticamente</td>
        </tr>
        <tr>
            <td>Infraestructura de alojamiento</td>
            <td>De un solo inquilino</td>
            <td>De varios inquilinos</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Personalización de administración de Commerce</strong></td>
        </tr>
        <tr>
            <td>Pantallas de administración principales ampliables</td>
            <td>Personalización completa del diseño y la funcionalidad</td>
            <td>Filtros preestablecidos, controles de visibilidad</td>
        </tr>
        <tr>
            <td>Pantallas de administración nuevas y ampliables</td>
            <td>Integración de la IU de administración estándar e inyección de aplicaciones externas (SDK de la IU de administración)</td>
            <td>Inyección de aplicación externa (SDK de IU de administración)</td>
        </tr>
        <tr>
            <td>Tema de administrador personalizable</td>
            <td>Marco de temas extensible</td>
            <td>Sin marco de temas</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Extensibilidad</strong></td>
        </tr>
        <tr>
            <td>Modelo de extensibilidad</td>
            <td>En proceso (personalización PHP) y fuera de proceso (API, eventos, App Builder)</td>
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
            <td>Atributos personalizados para entidades principales y B2B<sup>2</sup></td>
        </tr>
        <tr>
            <td>Tecnologías</td>
            <td>CSS, CLI, HTML, JS, PHP, XML</td>
            <td>CSS, CLI, HTML, JS, nodo</td>
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
            <td>Biblioteca de estado de App Builder (solo archivo)<sup>3</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                Las <sup>1</sup> características principales de <a href="https://experienceleague.adobe.com/es/docs/commerce-admin/b2b/guide-overview">B2B</a>, como la administración de la empresa y las cotizaciones, están disponibles de forma predeterminada en SaaS. Sin embargo, las personalizaciones específicas del sector pueden requerir consideraciones de implementación adicionales.
                <br><br>
                <sup>2</sup> La extensibilidad del modelo de datos en SaaS admite <a href="https://developer.adobe.com/commerce/webapi/graphql/schema/attributes/mutations/">la ampliación de entidades principales</a> más allá del producto y el cliente, incluidas las entidades B2B. Sin embargo, los modelos de datos específicos del sector (por ejemplo, los atributos específicos de los distribuidores) podrían requerir consideraciones arquitectónicas adicionales.
                <br><br>
                <sup>3</sup> Adobe está trabajando activamente en la integración de Document DB para abordar las necesidades de almacenamiento persistentes para SaaS. En la actualidad, las implementaciones que requieren almacenamiento de datos a largo plazo pueden necesitar aprovisionar y mantener una infraestructura adicional.
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
>- Considere la API Mesh para ampliar la funcionalidad de la API.
>- Monitorice la evolución continua de la plataforma de Adobe y las nuevas versiones de capacidades.
>- Evaluar los requisitos del modelo de datos específico del sector con respecto a las opciones de extensibilidad disponibles.
>- Considere la posibilidad de adoptar [servicios de comercialización con tecnología de canales y directivas](../optimizer/setup/catalog-view.md).
