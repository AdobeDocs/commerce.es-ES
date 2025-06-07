---
title: Ampliación y personalización de los datos de exportación de fuentes de SaaS
description: Obtenga información sobre cómo ampliar y personalizar los datos de la fuente  [!DNL SaaS Data Export] .
role: Admin, Developer
exl-id: 694bd281-12c5-415c-a251-b4251e2edea7
source-git-commit: ac6c690f87e3df2ac4997d80453028829be8e657
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# Ampliación y personalización de los datos de exportación de fuentes de SaaS

La extensión [!DNL Commerce Data Export] proporciona una forma de exportar datos desde la aplicación [!DNL Commerce] a servicios de Commerce como Live Search, Servicio de catálogo y Recomendaciones de productos. Si es necesario, puede ampliar y personalizar los datos de fuente para incluir datos de atributo adicionales o modificar los datos recopilados.

Después de agregar los datos de atributo, se puede obtener acceso a ellos desde el [campo de atributos](https://developer.adobe.com/commerce/services/graphql/catalog-service/products/#productviewattribute-type) en el esquema de GraphQL para el servicio de tienda.

>[!NOTE]
>
>Añadir o modificar datos de fuente puede afectar al rendimiento y a la lógica de procesamiento en el backend de Commerce. Pruebe el código personalizado antes de combinarlo en producción. En lugar de agregar datos al back-end, utilice API Mesh para ampliar el esquema GraphQL del servicio de catálogo. Para obtener detalles de configuración, consulte [Servicio de catálogo y malla de API](../catalog-service/mesh.md).

## Ampliar los datos de atributos del sistema en la fuente de productos

La fuente de productos incluye atributos de sistema predeterminados que son necesarios para el procesamiento del producto o que suelen utilizar los consumidores. Puede incluir atributos del sistema adicionales en la fuente de productos añadiéndolos a la fuente.

Para completar esta tarea, actualice el módulo `magento/catalog-data-exporter` para agregar los atributos de sistema adicionales al [archivo de configuración de inyección de dependencia](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`).

Agregue los atributos a la consulta de atributos del producto (`Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery`).

**Ejemplo**

```xml
    <type name="Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery">
        <arguments>
            <argument name="systemAttributes" xsi:type="array">
                <item name="news_from_date" xsi:type="string">news_from_date</item>
                ...
                <item name="some_system_attribute_code">some_system_attribute_code</item>
            </argument>
        </arguments>
    </type>
```

## Añadir atributos de producto a Adobe Commerce

Los desarrolladores pueden agregar atributos de producto a los que se puede tener acceso desde el [campo de atributos de producto](https://developer.adobe.com/commerce/services/graphql/catalog-service/products/#output-fields) mediante uno de los métodos siguientes:

- Agregue el atributo a Adobe Commerce para incluirlo en los datos de fuente `products` exportados a los servicios de tienda de Commerce.
- Añada el atributo de forma dinámica durante el proceso de sincronización de fuentes mediante un complemento.

### Añadir el atributo a Adobe Commerce

Puede añadir un atributo de producto desde el administrador de Commerce o, mediante programación, utilizar un módulo PHP personalizado para definir el atributo y actualizar Adobe Commerce. Añadir el atributo desde el administrador de Commerce es el método más sencillo, ya que puede añadir el atributo y todos los metadatos necesarios a la vez. El nuevo atributo y sus propiedades de metadatos se exportan automáticamente a los servicios SaaS durante la siguiente sincronización programada.

#### Cree el atributo de producto desde el administrador

1. Desde Commerce Admin, cree el atributo desde la página de configuración de atributos del producto ([!UICONTROL Stores] > *[!UICONTROL Attributes]* > [!UICONTROL Product]).

1. Agregue el atributo a un conjunto de atributos según sea necesario.

Consulte [Crear atributos de producto](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create) en la *Guía de administración de Adobe Commerce*.

#### Crear el atributo de producto mediante programación

Agregue un atributo product mediante programación creando un parche de datos que implemente `DataPatchInterface` e instancie una copia de la clase `EavSetup Factory` dentro del constructor para configurar las opciones del atributo.

Al definir las opciones de atributo, todos los parámetros de atributo excepto `type`, `label` y `input` son opcionales. Defina los siguientes parámetros adicionales y cualquier otro que difiera de la configuración predeterminada.

- **`user_defined`=`1`**: exporta el atributo a los servicios de tienda durante la sincronización de datos
- **`used_in_product_listing`=`1`**: permite acceder al atributo desde la consulta de base de datos de listado de productos

Para obtener información sobre cómo crear parches de datos, consulte [Desarrollo de parches de datos y esquemas](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/) en la *Guía para desarrolladores de PHP*.

### Añadir el atributo de producto de forma dinámica

Para obtener más información sobre cómo crear atributos de producto de forma dinámica sin introducir nuevos atributos EAV, consulte [Agregar atributo de forma dinámica](add-attribute-dynamically.md).
