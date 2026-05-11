---
title: Agregar atributos de clase de impuestos, juego de atributos e inventario
description: Obtenga información sobre cómo ampliar los datos de fuente de productos para incluir atributos de clasificación de impuestos, juego de atributos y configuración avanzada de inventario
role: Admin, Developer
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/
TQID: https://experienceleague.adobe.com/AWc-yAn-TyiBXQONoF2ZG9SFjj2u92CKbKvAY8mEVEE
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b5f00040-57a0-4a6d-a39e-383b1936c2c9id: c1256247-af4b-46d8-9dca-0c654ecfa157id: c18ed297-2187-4aec-affb-9d9654eca6fcid: dac87252-6066-4d6e-a9d2-f6d84c323de7id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: c1579802-ddd4-4214-8a91-97b2066abe11id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 812
ht-degree: 0%

---

# Agregar atributos de clase de impuestos, juego de atributos e inventario

El módulo Atributos de producto adicionales de Adobe Commerce amplía las fuentes de datos del producto. Incluye atributos de producto adicionales de las configuraciones de producto de Adobe Commerce:

* [Clasificación fiscal](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/taxes/tax-class)
* [Conjunto de atributos](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-sets)
* [Inventario](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/product-options#advanced-product-options)

Una vez instalado, el módulo funciona automáticamente. Registra y exporta los atributos adicionales durante la sincronización de productos. No se requiere ninguna configuración adicional.

## Ventajas principales

* **Mejora automática**: Enriquece las fuentes de productos con la clase de impuestos, el conjunto de atributos y los atributos de inventario
* **Integración perfecta**: proporciona contexto esencial para los sistemas y servicios externos
* **Configuración cero**: funciona inmediatamente después de la instalación
* **Actualizaciones en tiempo real**: se sincroniza automáticamente con los cambios del producto

## Funciones y atributos exportados

El módulo agrega tres atributos adicionales a las fuentes de datos de productos existentes:

* `ac_tax_class`
* `ac_attribute_set`
* `ac_inventory`

### &#x200B;1. Información de clase de impuestos (`ac_tax_class`)

**Propósito**: Proporciona información de clasificación de impuestos para cada producto

**Formato de datos**: Valor de cadena que contiene el nombre de la clase de impuestos

**Ejemplo de salida**:

```json
{
  "attributes": [
    {
      "code": "ac_tax_class",
      "values": ["Taxable Goods"]
    }
  ]
}
```

**Casos de uso**:

Al exportar datos de clase de impuestos a los servicios de catálogo de Commerce, estos datos están disponibles para las aplicaciones compatibles con lo siguiente:

* Informes de cumplimiento fiscal
* Integración con servicios de cálculo de impuestos externos
* Categorización de productos para sistemas de contabilidad

### &#x200B;2. Información del conjunto de atributos (`ac_attribute_set`)

**Propósito**: Identifica qué conjunto de atributos está asignado a cada producto

**Formato de datos**: Valor de cadena que contiene el nombre del conjunto de atributos

**Ejemplo de salida**:

```json
{
  "attributes": [
    {
      "code": "ac_attribute_set",
      "values": [
        "Default"
      ]
    }
  ]
}
```

**Casos de uso**:

Al exportar datos de conjuntos de atributos a los servicios de catálogo de Commerce, se habilitan funciones avanzadas de administración de productos en sistemas externos. Estas funciones incluyen:

* Identificación de plantilla de producto
* Gestión y organización del catálogo
* Integración de sistemas de terceros que requiere un contexto de conjunto de atributos

### &#x200B;3. Datos de inventario avanzados (`ac_inventory`)

**Propósito**: proporciona la configuración de administración de inventario para cada producto

**Formato de datos**: cadena con codificación JSON que contiene la configuración del inventario

**Campos incluidos**:

* `manageStock` (booleano): Si la administración de existencias está habilitada
* `cartMinQty` (flotante): Cantidad mínima permitida en el carro de compras
* `cartMaxQty` (flotante): Cantidad máxima permitida en el carro de compras
* `backorders` (cadena): directiva de pedidos pendientes. El valor es uno de los siguientes:
   * `"no"`: no se permiten pedidos pendientes
   * `"allow"`: permitir cantidad inferior a 0
   * `"allow_notify"`: permitir cantidad inferior a 0 y notificar al cliente
* `enableQtyIncrements` (booleano): Si los incrementos de cantidad están habilitados
* `qtyIncrements` (flotante): valor de incremento de cantidad requerido

**Ejemplo de salida**:

```json
{
  "attributes": [
    {
      "code": "ac_inventory",
      "values": [
        "{\"manageStock\":true,\"cartMinQty\":2,\"cartMaxQty\":42,\"backorders\":\"no\",\"enableQtyIncrements\":false,\"qtyIncrements\":2}"
      ]
    }
  ]
}
```

**Casos de uso**:

Al exportar datos de inventario a los servicios de catálogo de Commerce, se habilitan funciones avanzadas de administración de inventario en sistemas externos. Estas funciones incluyen:

* Integración del sistema de Inventory management
* Reglas de validación del carro de compras
* Optimización del proceso de realización de pedidos
* Personalización de la experiencia del cliente

## Mejora de la fuente de exportación de datos

El módulo Atributos de producto adicionales mejora las fuentes de productos existentes. Integra los nuevos datos de atributos automáticamente.

* **Fuente de productos** (`products`): mejorada con los tres atributos adicionales

   * Agrega los atributos `ac_tax_class`, `ac_attribute_set` y `ac_inventory` a cada registro de producto
   * Mantiene los datos del producto original sin cambios
   * Mantiene la compatibilidad con versiones anteriores de los consumidores de fuentes de datos existentes

* **Fuente de atributos del producto** (`productAttributes`): mejorado con metadatos de atributos para los nuevos atributos

   * Registra automáticamente los metadatos de los tres atributos nuevos en la fuente `productAttributes`
   * Proporciona detalles de configuración de atributos (tipos de datos, configuración de visibilidad, etc.)
   * Ayuda a los sistemas externos a comprender el nuevo esquema de atributos

## Instalación de la extensión

**Requisitos**

* PHP 8.1, 8.2, 8.3 u 8.4
* Adobe Commerce 2.4.4+
* [Extensión de exportación de datos de Adobe Commerce](manage-extension.md#update-a-module-to-a-specific-version), versión 103.4.11 o posterior
* Acceso a [repo.magento.com](https://repo.magento.com)

  Para generar claves y obtener los derechos necesarios, consulta [Obtener tus claves de autenticación](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys). Para instalaciones en la nube, consulte la [Guía de Commerce en infraestructura en la nube](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/authentication-keys).
* Acceso a la línea de comandos del servidor de aplicaciones de Adobe Commerce.

### Pasos de instalación

Agregar el módulo `adobe-commerce/module-extra-product-attributes` mediante Composer:

```shell
composer require adobe-commerce/module-extra-product-attributes
```

Para ver los pasos detallados de la instalación, consulte las siguientes guías:

* [Instalar la extensión en Adobe Commerce en la infraestructura de la nube](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
* [Instalación de la extensión de Adobe Commerce local](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

## Sincronización de datos de producto

Después de la reimplementación, la instancia de Adobe Commerce exporta los datos adicionales automáticamente durante la sincronización de productos. También puede utilizar los comandos CLI `resync` para sincronizar inmediatamente.

```shell
# Resync the products feed (includes the new attributes)
bin/magento saas:resync --feed=products
```

```shell
# Resync the product attributes feed (includes new attribute metadata)
bin/magento saas:resync --feed=productAttributes
```

## Resolución de problemas

A **productos les faltan atributos adicionales:**

* Compruebe que el módulo está correctamente instalado y habilitado
* Ejecute los comandos de resincronización para actualizar los datos del producto
* Comprobar que los productos tengan asignaciones válidas de clases de impuestos y juegos de atributos

**Los datos de inventario parecen incorrectos:**

* Compruebe que la configuración del inventario sea correcta en el Administrador
* Comprobar invalidaciones de inventario específicas del sitio web
* Compruebe que el [módulo de Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/guide-overview) funciona correctamente

Para obtener más información, consulte la [Guía de Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/guide-overview) en la *Documentación de Adobe Commerce Merchant*.

**Problemas de rendimiento:**

* Monitorización del rendimiento del proceso de exportación después de la instalación
* Considere la posibilidad de programar resincronizaciones durante períodos de poco tráfico

### Registro y depuración

Los registros del módulo exportan errores y advertencias al sistema de registro estándar de Commerce. Si tiene problemas durante la sincronización de productos, compruebe los registros de exportación de datos.

Para obtener más información, vea [Revisar registros y solucionar problemas](troubleshooting-logging.md).

