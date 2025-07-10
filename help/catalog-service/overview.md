---
title: '[!DNL Catalog Service]'
description: 'Acelere su tienda Adobe Commerce con [!DNL Catalog Service] : una API de GraphQL de alto rendimiento que reduce los tiempos de carga de las páginas de productos, las páginas de categorías y los resultados de búsqueda.'
role: Admin, Developer
recommendations: noCatalog
exl-id: 525e3ff0-efa6-48c7-9111-d0b00f42957a
source-git-commit: e582bff6ee8ee7c4213f04bdab984efa94333fb6
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 0%

---

# [!DNL Catalog Service] para Adobe Commerce

La extensión [!DNL Catalog Service] para Adobe Commerce mejora los tiempos de carga de las tiendas al proporcionar datos de catálogo optimizados de solo lectura a través de una API de GraphQL dedicada. Este servicio está diseñado específicamente para mejorar las experiencias de página relacionadas con el producto, lo que resulta en cargas de página más rápidas y tasas de conversión mejoradas.

Los datos del modelo de vista enriquecido proporcionados por [!DNL Catalog Service] incluyen detalles del producto, atributos, inventario y precios, lo que permite procesar rápidamente las experiencias de tienda relacionadas con el producto, como:

- Páginas de detalles del producto
- Páginas de lista y categoría de productos
- Páginas de resultados de búsqueda
- Carruseles de productos
- Páginas de comparación de productos
- Cualquier otra página que procese datos de producto, como páginas de carro de compras, pedidos y listas de deseos


## Ventajas y características principales

- **Cargas de página más rápidas**: Consultas optimizadas para una recuperación de datos del catálogo hasta 10 veces más rápida en comparación con el sistema principal de GraphQL
- **Tasas de conversión mejoradas**: Los tiempos de carga más rápidos conducen a una mejor experiencia de usuario
- **Tipos de productos simplificados**: el esquema unificado basado en tipos de productos simples y complejos reduce la complejidad para los desarrolladores
- **Precisión de precio mejorada**: Compatibilidad con valores de 16 dígitos con 4 decimales
- **Arquitectura disociada**: un sistema GraphQL independiente para los datos del catálogo garantiza un alto rendimiento sin afectar a las operaciones principales de Commerce
- **Sincronización de datos en tiempo real**: El servicio de catálogo se mantiene sincronizado con la aplicación de Adobe Commerce a través de la extensión de exportación de datos SaaS, lo que garantiza que las consultas devuelvan los datos de catálogo más actuales
- **Panel de administración de datos**: supervise y administre las operaciones de sincronización de datos desde la interfaz de administración de Adobe Commerce
- **Integración de API Mesh**: opcionalmente se integra con [API Mesh para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/) para combinar los sistemas de Adobe Commerce GraphQL con otras API internas y de terceros para extender el esquema GraphQL del servicio de catálogo y agregar datos o funcionalidad personalizados


## Descripción general de arquitectura

[!DNL Catalog Service] usa [GraphQL](https://graphql.org/) para solicitar y recibir datos de catálogo, incluidos productos, atributos de productos, inventario y precios. GraphQL es un lenguaje de consulta que un cliente de front-end utiliza para comunicarse con la interfaz de programación de aplicaciones (API) definida en un back-end como Adobe Commerce. GraphQL es un método de comunicación popular porque es ligero y permite al integrador de sistemas especificar el contenido y el orden de cada respuesta.

Adobe Commerce proporciona dos sistemas GraphQL con diferentes propósitos:

### Sistema Core GraphQL

- **Propósito**: API con todas las funciones para todas las operaciones de Commerce
- **Capacidades**: Consultas (lectura) y mutaciones (escritura) para productos, clientes, carrito, cierre de compra y más
- **Limitación**: las consultas de productos no están optimizadas para la velocidad
- **Caso de uso**: operaciones generales de Commerce y operaciones de escritura

### Sistema GraphQL de servicio de catálogo

- **Propósito**: solo consultas de catálogo de productos de alto rendimiento
- **Capacidades**: consultas de solo lectura para productos, atributos, inventario y precios
- **Ventaja**: considerablemente más rápido que el sistema principal para los datos de productos
- **Caso de uso**: Experiencias de productos en tiendas donde la velocidad es crítica

La extensión de exportación de datos SaaS entrega los datos disponibles para el servicio de catálogo. Esta extensión sincroniza los datos entre la aplicación de Commerce y los servicios de Commerce conectados para garantizar que las consultas a los servicios de los extremos de la API de GraphQL devuelvan los datos de catálogo más actuales. Para obtener información acerca de la administración y solución de problemas de las operaciones de exportación de datos SaaS, consulte la [Guía de exportación de datos SaaS](../data-export/overview.md).

Los clientes de [!DNL Catalog Service] pueden usar el [indexador de precios SaaS](../price-index/price-indexing.md), que ofrece actualizaciones de precios y tiempo de sincronización más rápidos.

## Detalles de arquitectura

El diagrama siguiente ilustra las diferencias de arquitectura entre el sistema principal de GraphQL y el sistema GraphQL de servicio de catálogo, y muestra cómo funcionan juntos para optimizar el rendimiento de la tienda:

![Diagrama de arquitectura de catálogo](assets/catalog-service-architecture.png)

### Cómo funcionan los sistemas

**Sistema Core GraphQL (Enfoque Tradicional):**
La aplicación web progresiva (PWA) envía solicitudes directamente a la aplicación de Commerce, que procesa cada solicitud a través de varios subsistemas antes de devolver una respuesta. Este recorrido de ida y vuelta de varios pasos puede causar tiempos de carga de página lentos, lo que potencialmente conduce a tasas de conversión más bajas.

**Servicio de catálogo (enfoque optimizado):**
El servicio de catálogo actúa como una puerta de enlace de Storefront Services que accede a una base de datos dedicada y optimizada que contiene detalles del producto, atributos, variantes, precios y categorías. El servicio mantiene la sincronización con Adobe Commerce mediante la indexación automatizada, lo que evita el ciclo tradicional de solicitud y respuesta para reducir la latencia de forma notable.

Los sistemas GraphQL principales y de servicio no se comunican directamente entre sí. Puede acceder a cada sistema desde una dirección URL diferente y las llamadas requieren información de encabezado diferente. Los dos sistemas GraphQL están diseñados para utilizarse juntos. El sistema de GraphQL [!DNL Catalog Service] aumenta el sistema principal para que las experiencias de tienda de productos sean más rápidas.

Opcionalmente, puede implementar [API Mesh para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/) para integrar los dos sistemas de Adobe Commerce GraphQL con API privadas y de terceros y otras interfaces de software mediante Adobe Developer. La malla se puede configurar para garantizar que las llamadas enrutadas a cada extremo contengan la información de autorización correcta en los encabezados.

## Detalles arquitectónicos

En las secciones siguientes se describen algunas de las diferencias entre los dos sistemas de GraphQL.

### Administración de esquemas

Dado que el servicio de catálogo funciona como un servicio, los integradores no necesitan preocuparse por la versión subyacente de Commerce. La sintaxis de las consultas es la misma para todas las versiones. Además, el esquema es coherente para todos los comerciantes. Esta coherencia facilita la definición de prácticas recomendadas y aumenta significativamente la reutilización de los widgets de tienda.

### Simplificación de los tipos de productos

El esquema reduce la diversidad de tipos de productos a dos casos de uso:

- **Productos simples**: el servicio de catálogo asigna los tipos de producto Adobe Commerce simples, virtuales, descargables y de tarjeta regalo a `simpleProductViews`. Este tipo tiene:
   - Un precio y cantidad únicos y fijos
   - Precio normal (antes de descuentos) y precio final (después de descuentos)
   - Compatibilidad con atributos del producto, como color, tamaño y otras características

- **Productos complejos**: el servicio de catálogo asigna los tipos de productos configurables, agrupados y agrupados de Adobe Commerce a `complexProductViews`. Los productos complejos son colecciones de varios productos simples que se pueden configurar o agrupar.
   - Cada componente de producto simple puede tener su propio precio.
   - Los compradores pueden especificar cantidades para productos de componentes individuales.
   - Las opciones de producto (como tamaño, color y material) están unificadas y funcionan de la misma manera independientemente del tipo de producto. Cada selección de opciones apunta a un producto simple específico con sus propios atributos y precios. El producto final permanece sin definir hasta que el comprador selecciona todas las opciones requeridas.

#### Atributos de vista de producto

Tanto los productos simples como los complejos tienen atributos definidos por el cliente que se pueden mostrar en la tienda. Estos atributos se devuelven como [ProductViewAttributes](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type). En Adobe Commerce, los atributos disponibles se definen cuando se crea el producto. Puede agregar atributos adicionales desde el backend de Adobe Commerce o mediante programación. Consulte [Ampliar y personalizar datos de fuentes de exportación de datos SaaS](../data-export/extensibility-and-customizations.md).

>[!TIP]
>
>En lugar de agregar tipos de datos al servidor de Commerce, puede usar [API Mesh con el servicio de catálogo](mesh.md) para ampliar el esquema de GraphQL del servicio de catálogo y agregar datos o configurar los datos de catálogo existentes para habilitar la nueva funcionalidad.

### Precios

Los productos simples representan la unidad de venta base que tiene un precio. [!DNL Catalog Service] calcula el precio normal antes de los descuentos, así como el precio final después de los descuentos. Los cálculos de precios pueden incluir impuestos de productos fijos. Excluyen las promociones personalizadas.

Un producto complejo no tiene un precio establecido. En su lugar, el servicio de catálogo devuelve los precios de las simples vinculadas. Por ejemplo, un comerciante puede asignar inicialmente los mismos precios a todas las variantes de un producto configurable. Si ciertos tamaños o colores son impopulares, el comerciante puede reducir los precios de esas variantes. Por lo tanto, el precio del producto complejo (configurable) al principio muestra un rango de precios, que refleja el precio de las variantes estándar y las impopulares. Una vez que el comprador ha seleccionado un valor para todas las opciones disponibles, la tienda muestra un solo precio.

El servicio de catálogo garantiza actualizaciones y cálculos de precios precisos al admitir precios con valores grandes (hasta 16 dígitos) y alta precisión decimal (hasta 4 decimales).

>[!NOTE]
>
> Los clientes de Commerce con [!DNL Catalog Service] pueden aprovechar las actualizaciones de precios más rápidas y el tiempo de sincronización en sus sitios web con el [indexador de precios SaaS](../price-index/price-indexing.md).

## Implementación

El proceso de implementación implica:

1. [!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."} **[Instale y configure el Servicio de catálogo](installation.md)**: instale y configure la extensión del Servicio de catálogo y configure la conexión SaaS mediante [!DNL Commerce Services Connector].
2. **Actualizar código de tienda**: integra las consultas GraphQL del servicio de catálogo en tu front-end.
3. **Consultas de ruta**: todas las consultas del servicio de catálogo pasan a través de la puerta de enlace de GraphQL (URL proporcionada durante la incorporación)
4. **Supervisar y solucionar problemas de sincronización de datos**: compruebe el rendimiento mejorado y supervise los resultados


