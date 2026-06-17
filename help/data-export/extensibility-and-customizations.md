---
title: Ampliación y personalización de los datos de exportación de fuentes de SaaS
description: Obtenga información sobre cómo ampliar y personalizar los datos de la fuente  [!DNL SaaS Data Export] .
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 694bd281-12c5-415c-a251-b4251e2edea7
TQID: https://experienceleague.adobe.com/T71zNl7WOrqzEsz4H8A8arx--q6w1B0h33CF2Q0VI4A
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 815
ht-degree: 0%

---

# Ampliación y personalización de los datos de exportación de fuentes de SaaS

La extensión [!DNL Commerce Data Export] proporciona una forma de exportar datos desde la aplicación [!DNL Commerce] a servicios de Commerce como Live Search, Servicio de catálogo y Recomendaciones de productos. Si es necesario, puede ampliar y personalizar los datos de fuente para incluir datos de atributo adicionales o modificar los datos recopilados.

Después de agregar los datos de atributo, se puede obtener acceso a ellos desde el [campo de atributos](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type) en el esquema de GraphQL para los servicios de tienda.

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

Los desarrolladores pueden agregar atributos de producto a los que se puede tener acceso desde el [campo de atributos de producto](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#output-fields) mediante uno de los métodos siguientes:

- Agregue el atributo a Adobe Commerce para incluirlo en los datos de fuente `products` exportados a los servicios de tienda de Commerce.
- Añada el atributo de forma dinámica durante el proceso de sincronización de fuentes mediante un complemento.

### Añadir el atributo a Adobe Commerce

Puede añadir un atributo de producto desde el administrador de Commerce o, mediante programación, utilizar un módulo PHP personalizado para definir el atributo y actualizar Adobe Commerce. Añadir el atributo desde el administrador de Commerce es el método más sencillo, ya que puede añadir el atributo y todos los metadatos necesarios a la vez. El nuevo atributo y sus propiedades de metadatos se exportan automáticamente a los servicios SaaS durante la siguiente sincronización programada.

#### Cree el atributo de producto desde el administrador

1. Desde Commerce Admin, cree el atributo desde la página de configuración de atributos del producto ([!UICONTROL Stores] > *[!UICONTROL Attributes]* > [!UICONTROL Product]).

1. Agregue el atributo a un conjunto de atributos según sea necesario.

Consulte [Crear atributos de producto](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create) en la *Guía de administración de Adobe Commerce*.

#### Crear el atributo de producto mediante programación

Agregue un atributo product mediante programación creando un parche de datos que implemente `DataPatchInterface` e instancie una copia de la clase `EavSetup Factory` dentro del constructor para configurar las opciones del atributo.

Al definir las opciones de atributo, todos los parámetros de atributo excepto `type`, `label` y `input` son opcionales. Defina los siguientes parámetros adicionales y cualquier otro que difiera de la configuración predeterminada.

- **`user_defined`=`1`**: exporta el atributo a los servicios de tienda durante la sincronización de datos
- **`used_in_product_listing`=`1`**: permite acceder al atributo desde la consulta de base de datos de listado de productos

Para obtener información sobre cómo crear parches de datos, consulte [Desarrollo de parches de datos y esquemas](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/) en la *Guía para desarrolladores de PHP*.

### Añadir el atributo de producto de forma dinámica

Para obtener más información sobre cómo crear atributos de producto de forma dinámica sin introducir nuevos atributos EAV, consulte [Agregar atributos de producto de forma dinámica](add-attribute-dynamically.md).

## Resumen del esquema de fuentes (`et_schema.xml`) {#feed-schema-overview}

Cada estructura de datos de fuente se declara en `etc/et_schema.xml` mediante un DSL XML simple. El marco de trabajo lee este archivo para determinar qué campos recopilar y a qué clases de proveedor PHP llamar.

```xml
<record name="Product">
  <field name="sku" type="ID" />
  <field name="name" type="String" />
  <field name="attributes" type="Attribute" repeated="true"
         provider="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
    <using field="productId" />
    <using field="storeViewCode" />
  </field>
</record>
```

Elementos clave:

- `<record>`: define la entidad de fuente
- `<field>` - declara un campo de datos; el atributo `provider` señala a una clase PHP que implementa `DataProcessorInterface` que recupera los datos
- `repeated="true"`: el campo es una matriz de objetos
- `<using>`: parámetros de entrada pasados desde el contexto de registro principal al proveedor

>[!IMPORTANT]
>
>Al agregar un nuevo campo a `et_schema.xml` solo se cambia lo que [!DNL Adobe Commerce] recopila localmente. El servicio SaaS de recepción también debe actualizarse para aceptar y procesar el nuevo campo antes de que tenga algún efecto en la tienda.

## Observar datos después del envío {#observe-data-after-submission}

[!DNL SaaS Data Export] distribuye el evento `data_sent_outside` después de cada envío de lotes correcto a un servicio SaaS. Utilice este evento para el registro de auditoría, los déclencheur de webhook o la recopilación de métricas.

**Evento:** `data_sent_outside`

**Datos disponibles:**

| Clave | Descripción |
|---|---|
| `timestamp` | Marca de tiempo Unix del envío |
| `type` | Nombre de fuente (por ejemplo, `products`, `prices`) |
| `data` | La carga útil de fuente enviada |

**Observador de ejemplo:**

```php
<?php
namespace My\Module\Observer;

use Magento\Framework\Event\Observer;
use Magento\Framework\Event\ObserverInterface;

class DataSentOutsideObserver implements ObserverInterface
{
    public function execute(Observer $observer): void
    {
        $feedName = $observer->getData('type');
        $timestamp = $observer->getData('timestamp');
        $data = $observer->getData('data');

        // Custom logic: audit logging, webhook, metrics
    }
}
```

Registrar al observador en `etc/events.xml`:

```xml
<event name="data_sent_outside">
    <observer name="my_module_data_sent_outside"
              instance="My\Module\Observer\DataSentOutsideObserver" />
</event>
```

Para obtener información general sobre eventos y observadores, consulte [Eventos y observadores](https://developer.adobe.com/commerce/php/development/components/events-and-observers){target="_blank"} en la documentación para desarrolladores de Adobe Commerce.

## Filtrado de datos antes del envío

Utilice el punto de extensión `Magento\SaaSCommon\Model\DataFilter` para redactar campos confidenciales u omitir entidades específicas antes de que se envíen datos al servicio SaaS. Esto resulta útil para los requisitos de cumplimiento, como RGPD o PCI, en los que determinados campos no deben salir de la instancia de Commerce.

Implemente la interfaz y conéctela a través de una preferencia de ID en `etc/di.xml`:

```xml
<preference for="Magento\SaaSCommon\Model\DataFilter"
            type="My\Module\Model\MyDataFilter" />
```

>[!NOTE]
>
>El filtrado se aplica después de la recopilación de datos. Si se establece `PERSIST_EXPORTED_FEED=1`, la tabla de fuentes almacena la carga útil sin filtrar antes de que se produzca el filtrado.

>[!MORELIKETHIS]
>
> - [Agregar atributo de producto dinámicamente](add-attribute-dynamically.md)
> - [Agregar metadatos de inventario, conjunto de atributos y clase de impuestos](add-tax-attribute-set-inventory-attributes.md)
> - [Funcionamiento de la sincronización](sync-overview.md)
