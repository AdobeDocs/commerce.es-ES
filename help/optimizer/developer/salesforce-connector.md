---
title: Conector de Salesforce Commerce
description: Obtenga información acerca de [!DNL Commerce Optimizer SFCC Connector] que proporciona un punto de partida para integrar Salesforce Commerce B2C con [!DNL Adobe Commerce Optimizer] para sincronizar los datos del catálogo e implementar y personalizar el conector para admitir operaciones empresariales.
role: Admin, Developer
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 0%

---

# Conector de Salesforce Commerce para Adobe Commerce Optimizer

Basado en la tecnología Adobe App Builder, [!DNL Commerce Optimizer Salesforce Commerce Connector] permite la transferencia y administración sin problemas de los datos del catálogo de Salesforce Commerce Cloud B2C a [!DNL Adobe Commerce Optimizer]. Combina ambas plataformas y mantiene la información del producto, los precios y las actualizaciones sincronizados, sin necesidad de volver a plataformas.

De forma predeterminada, el conector ofrece funciones fiables de sincronización de datos y la flexibilidad para personalizar los flujos de trabajo según las necesidades de su empresa.

Para ver una serie completa de tutoriales de vídeo, consulte [Más información acerca del kit de iniciación en la nube de Salesforce Commerce](https://experienceleague.adobe.com/es/docs/commerce-learn/tutorials/adobe-commerce-optimizer/sfcc-starter-kit/overview).

## Funcionalidades clave

* **Sincronización de datos de catálogo:** inserte datos de productos (incluidas variantes, libros de precios y estructuras) de Salesforce Commerce B2C en Adobe Commerce Optimizer para mantener actualizados los escaparates y las aplicaciones basadas en la experiencia.
* **Sincronización de precios:** Importe y administre datos de precios directamente desde Salesforce Commerce B2C.
* **Admite varios tipos de datos:** Sincroniza productos, precios y estructuras de catálogo para reflejar configuraciones de comercialización complejas.

* **Flujos de trabajo de sincronización flexibles**
   * **Sincronizaciones programadas:** Automatice las actualizaciones mediante la programación de trabajos cron, no se requiere ningún esfuerzo manual.
   * **Actualizaciones a petición:** déclencheur al instante actualizaciones a nivel de SKU para cambios urgentes, correcciones o lanzamientos de productos.

* **Compilado para extensibilidad**
   * Utiliza los extremos personalizados de la [API B2C de Salesforce Commerce](https://developer.salesforce.com/docs/commerce/commerce-api/guide/get-started.html) (SCAPI) para ofrecer compatibilidad y fácil adaptación a casos de uso únicos o avanzados.
   * Escala con su empresa: inicie con la sincronización de catálogos y precios y, a continuación, amplíe los flujos de trabajo para admitir integraciones o lógica empresarial adicionales.
   * Configure y evolucione flujos de trabajo sin reconstruir integraciones principales.

>[!NOTE]
>
>El conector está diseñado específicamente para Salesforce Commerce Cloud B2C. No admite productos B2B o D2C de Salesforce, que se basan en diferentes pilas de tecnología.

## ¿Quién se beneficia de Salesforce Connector?

[!DNL Salesforce Commerce Connector] es ideal para:

* **Clientes existentes de Salesforce Commerce Cloud B2C** que mejoran las capacidades de la tienda
* **Organizaciones de varias marcas** que requieren funciones avanzadas de comercialización y personalización en varias tiendas
* **Empresas que buscan mejoras de rendimiento** a través de Edge Delivery Services de Adobe para experiencias de tienda más rápidas
* **Compañías con estructuras de precios complejas** que sincronizan libros de precios sofisticados y precios específicos de la configuración regional
* **Clientes de AEM** que administran catálogos de productos desde Salesforce Commerce B2C mientras usan Adobe Commerce Storefront con Edge Delivery Services
* **Minoristas con requisitos de varias configuraciones regionales** que sincronizan la información de productos localizados en mercados e idiomas

## Casos de uso

El conector admite varios casos de uso clave:

### Ingesta de datos de catálogo y visualización de tiendas

Este caso de uso principal muestra el flujo de datos completo de Salesforce Commerce B2C a la tienda de Adobe Commerce:

1. **Ingesta inicial al catálogo:** Cargue en lote todo el catálogo comercial de Salesforce, incluidos productos simples con variantes, libros de precios e información de precios.
1. **Actualizaciones delta automatizadas:** Sincronice automáticamente las actualizaciones de productos de la interfaz de usuario de administración del catálogo de Salesforce Commerce con [!DNL Commerce Optimizer].
1. **Integración de tienda:** Muestra datos de catálogo sincronizados en tu tienda de Adobe Commerce Edge Delivery Service mediante las API de tienda [!DNL Commerce Optimizer].
1. **Actualizaciones en tiempo real:** Consulta la información actualizada del producto (nombres, precios, descripciones) inmediatamente en tu tienda después de hacer cambios en Salesforce.

### Administración de productos en varias configuraciones regionales

Aproveche las funciones de localización B2C de Salesforce Commerce:

* Sincronizar versiones localizadas de campos de texto de productos (nombres, descripciones) de Salesforce Commerce B2C para diferentes configuraciones regionales.
* Asignar conceptos de configuración regional de Salesforce 1:1 con configuraciones regionales de [!DNL Commerce Optimizer].
* Admitir varios ciclos de ingesta de productos para diferentes localizaciones.
* Mantener la coherencia en los catálogos de productos globales.

## Arquitectura y componentes

[!DNL SFCC Connector] proporciona una capa de integración sólida entre una instancia B2C de Salesforce Commerce y [!DNL Commerce Optimizer]. El conector funciona a través de una serie de acciones de sincronización que transfieren los datos del catálogo, los libros de precios y la información del producto.

1. **Extracción de datos**: realice la autenticación con su instancia B2C de Salesforce Commerce y extraiga los datos del catálogo mediante las API de SCAPI personalizadas.
1. **Transformación de datos**: transforme los datos del producto para que coincidan con los requisitos del esquema y el modelo de datos [!DNL Commerce Optimizer].
1. **Ingesta de datos**: transmita de forma segura datos transformados a [!DNL Commerce Optimizer] mediante ACO TypeScript SDK.
1. **Integración de tienda**: los datos sincronizados están disponibles a través de las API [!DNL Commerce Optimizer] para las experiencias de tienda.

El diagrama siguiente ilustra el flujo de datos de alto nivel para la integración:

![Arquitectura del conector Commerce de Salesforce](../assets/sfcc_starter_kit.png){zoomable="yes"}

### Componentes clave

[!DNL Commerce Optimizer SFCC Connector] consta de varios componentes clave:

* **Aplicación ACO SFCC Starter Kit App Builder**: proporciona funciones sin servidor que administran la sincronización de datos entre SFCC y Adobe Commerce Optimizer.
* **Cartucho SFCC personalizado**: cartucho requerido que amplía la instancia de Salesforce Commerce Cloud con las API necesarias para la extracción de datos.
* **IU de administración**: interfaz web para supervisar el estado de sincronización y administrar las operaciones del conector.

### Proceso de sincronización

El conector admite varios modos de sincronización.

| Modo de sincronización | Descripción |
|-----------|-------------|
| **Sincronización completa del sitio** | Realiza una sincronización completa de todos los productos, libros de precios y precios para el sitio y las configuraciones regionales de Salesforce Commerce Cloud. Esto incluye <ul><li>metadatos y atributos del producto</li><li>estructura y categorías del catálogo</li><li>libros de precios</li><li>información de precios</li><li>datos de producto de varias configuraciones regionales</li></ul> |
| **Sincronización Delta** | Recupera y sincroniza solo los cambios realizados en los datos de precios y productos de Salesforce desde la última sincronización, lo que garantiza actualizaciones eficientes y oportunas.<br>La sincronización delta se ejecuta automáticamente de forma programada (valor predeterminado: por hora) para mantener la actualización de los datos. |
| **Opciones de sincronización de destino** | Proporciona funciones de sincronización granulares: <ul><li>**Sincronización del libro de precios** sincroniza solo la información del libro de precios</li><li>**Sincronización de metadatos** actualiza definiciones de atributos y metadatos de productos</li><li>**Sincronización específica de productos** sincroniza productos individuales por SKU</li></ul> |

## Consideraciones importantes

Al planificar la implementación, tenga en cuenta estos factores clave:

### Asignación de datos y atributos

* **Atributos que permiten búsqueda:** Salesforce Commerce B2C establece atributos que permiten búsqueda a través de la interfaz de usuario, que la API no expone. Use [[!DNL Catalog Data Ingestion metadata APIs]](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#metadata) para configurar manualmente estos atributos en los que se puede buscar en Adobe Commerce Optimizer.
* **Asignación de atributos:** Planifique la asignación de atributos de productos B2C de Salesforce Commerce a metadatos [!DNL Commerce Optimizer] en función de los requisitos de su empresa.
* **Campos predeterminados en los que se pueden realizar búsquedas:** El conector permite buscar automáticamente los atributos principales (`name`, `description`, `ID`) de forma predeterminada.

### Ámbito de sincronización

* **Selección de sitios:** Salesforce Commerce B2C tiene un concepto de sitios a los que se adjuntan catálogos. Durante la sincronización completa, seleccione qué sitio de Salesforce sincronizar.
* **Administración de configuración regional:** Cada configuración regional de Salesforce Commerce genera un ciclo de ingesta de productos independiente en [!DNL Commerce Optimizer].
* **Volumen de datos:** Tenga en cuenta el tamaño del catálogo y la frecuencia de sincronización al planificar la implementación.

## Monitorización y administración

Una vez instalado y configurado, [!DNL Commerce Optimizer SFCC Connector] proporciona funciones completas de supervisión y administración desde [!DNL SFCC to ACO Sync Panel]:

![IU de administración del conector Salesforce Commerce](../assets/sfcc_management_ui.png){width="700" zoomable="yes"}

La dirección URL de esta interfaz se proporciona después de implementar [!DNL Commerce Optimizer SFCC Connector Starter Kit] en el proyecto de App Builder.

Las funciones principales incluyen:

* **Seguimiento del estado de sincronización:** Supervise el estado y las marcas de tiempo de todas las operaciones de sincronización.
* **Validación de conectividad:** Probar conexiones a Salesforce Commerce Cloud y Adobe Commerce Optimizer.
* **Validación de datos del producto:** Compruebe que los datos sincronizados del producto aparezcan correctamente en la tienda.
* **Registro de errores y solución de problemas:** Se puede acceder a los registros de errores para la solución de problemas a través de la CLI de App Builder.
* **Administración de estado:** Rastree el progreso de sincronización y evite conflictos con la administración de estado integrada.

## Código Source y recursos de desarrollo

[!DNL Commerce Optimizer SFCC Connector] es de código abierto y está disponible para la personalización. Los repositorios clave incluyen:

* **[Kit de inicio ACO SFCC](https://github.com/adobe-commerce/aco-sfcc-starter-kit)**: aplicación y documentación del conector principal.
* **[Cartuchos ACO SFCC](https://github.com/adobe-commerce/aco-sfcc-cartridges)**: Se requiere un cartucho SFCC para la integración de API.
* **[SDK TypeScript de ACO](https://github.com/adobe-commerce/aco-ts-sdk)**: integración de SDK para Adobe Commerce Optimizer.

Estos repositorios proporcionan código fuente completo, documentación detallada y ejemplos para implementar y personalizar el conector.

## Pasos siguientes

¿Está listo para integrar sus datos de Salesforce Commerce Cloud con Adobe Commerce Optimizer? Comience por revisar la guía de implementación detallada en el [repositorio del Starter Kit de ACO SFC](https://github.com/adobe-commerce/aco-sfcc-starter-kit) y asegúrese de que cuenta con los requisitos previos necesarios.
