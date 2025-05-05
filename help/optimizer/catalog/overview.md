---
title: Descripción general del catálogo
description: Descubra cómo definir sus canales y políticas.
hide: true
recommendations: noCatalog
source-git-commit: d716dd9d75beb642bfad30271b6ecd3490ee7328
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 0%

---

# Descripción general del catálogo

>[!NOTE]
>
>Esta documentación describe un producto en desarrollo de acceso anticipado y no refleja todos los funcionalidad destinados a la disponibilidad general.

Un catálogo de productos es esencial para en línea experiencias de compra, ya que permite a los clientes examinar, búsqueda y realizar compras. Para la eficiencia operativa, un catálogo de productos debe reflejar fielmente la estructura empresarial del compañía. Las empresas a menudo necesitan vender productos a precios variables según el mercado geográfico, el canal de distribución, el segmento del cliente y otras variables. Para acomodar esto, una plataforma de comercio electrónico debe oferta un modelo de datos de catálogo flexible que permita a las empresas producir variaciones de su catálogo adaptadas a estos escenarios. Adobe Systems aborda estas necesidades ofreciendo servicios de comercialización impulsados por canales y políticas. Los servicios de comercialización proporcionan bloques de creación que los comerciantes pueden utilizar para crear y administrar catálogos a escala. Esto permite a las empresas configurar catálogos que se alinean con su estructura empresarial y estrategias de mercado.

A un alto nivel, con los Servicios de Merchandising puedes:

- Utilice un único catálogo base para todas las necesidades empresariales. Escale su catálogo rápidamente a través de nuevas marcas, mercados, unidades de negocio, canales de mercado y segmentos de clientes sin necesidad de una rearquitectura completa. Esto elimina la duplicación de datos y configura su plataforma de comercio electrónico para una alta eficiencia operativa.
- Desbloquee la sindicación de catálogos y ofrezca la contenido correcta diseñando su catálogo de productos para reflejar su negocio, incluidos productos, clientes, precios y distribución.
- Ingiera y actualice rápidamente los datos del catálogo y entregue rápidamente las actualizaciones a la tienda para sus promociones y necesidades campaña.
- Logre puntajes de faro perfectos con componentes de IU listos para usar y ultrarrápidos con tecnología de Edge Delivery Services para una navegación y recomendaciones de productos sin problemas.
- Adopte una arquitectura componible moderna utilizando la arquitectura de extensibilidad de Adobe Systems ([aplicación Builder](https://experienceleague.adobe.com/es/playlists/commerce-get-started-app-builder-development)) para importar datos de productos y potenciar escaparates de comercio sin cabeza utilizando la malla API de [Adobe Systems](https://experienceleague.adobe.com/es/playlists/commerce-get-started-app-builder-and-api-mesh).

>[!INFO]
>
>Para obtener más información sobre las API disponibles en Servicios de comercialización equipados con canales y políticas, consulte la documentación[&#128279;](https://developer-stage.adobe.com/commerce/services/composable-catalog) para desarrolladores.

## Arquitectura

Los servicios de comercialización basados en canales y políticas son un modelo de datos de catálogo flexible y altamente escalable que desbloquea casos de uso de varias marcas, unidades empresariales y varios idiomas con facilidad. Este modelo reemplaza el uso de los ámbitos de producto clásicos de Adobe Commerce (sitio web, tienda, vista de tienda) con los nuevos ámbitos de producto de Servicios de comercialización (canal, directiva y configuración regional).

El diagrama siguiente proporciona una vista de alto nivel del marco de comercialización.

![[!DNL Merchandising Services] arquitectura](../assets/merchandising-svcs-architecture.png)

En la parte superior de este diagrama, los datos de catálogo (PIM, ERP, etc.) se incorporan al marco de servicios de comercialización. Estos datos de catálogo contienen SKU. Cada SKU contiene detalles de ámbito (configuración regional) y atributos de producto, que se asignan a los nuevos ámbitos de producto de los servicios de comercialización (canales, directivas y configuración regional).

Cuando todos estos datos se incorporan al marco de trabajo de comercialización, el resultado es un nuevo catálogo base unificado que está disponible en la canalización de datos del servicio de catálogo. En la siguiente parte del diagrama, verá varios canales. Cada canal representa una unidad empresarial. Por ejemplo, *comercio minorista de Texas*, *comercio minorista de Texas de temporada*, etc. Como puede ver, en el diagrama, las configuraciones regionales, las directivas y los libros de precios se pueden compartir en todos los canales&#x200B;

Por último, el diagrama muestra cómo se pueden mostrar estos datos de catálogo distintos en varias ubicaciones, como una tienda Edge Delivery Services, un mercado, un canal de publicidad, una microtienda personalizada, etc.

Para obtener información sobre cómo introducir los datos del catálogo en comercialización mediante la API de ingesta de datos del catálogo y cómo configurar las configuraciones regionales, las directivas y los libros de precios mediante la API de reglas y la administración del catálogo, consulte [documentación para desarrolladores](https://developer-stage.adobe.com/commerce/services/composable-catalog/).

Para obtener más información sobre los conceptos que componen los servicios de comercialización, consulte las siguientes secciones.

## Administración del catálogo de productos

La administración del catálogo de productos abarca dos aspectos distintos: datos y contexto del producto. Servicios de Comercialización respeta la separación de estas funciones, ofreciendo una gestión independiente para cada uno.

- **Datos del** producto: ¿Qué producto se vende y a qué precio?
- **Contexto** del producto: ¿Quién vende a quién y dónde?

![[!DNL Merchandising Services] Aspectos](../assets/merchandising-svcs-parts.png)

### Datos del producto

Los datos del producto incluyen los siguientes tipos:

- **Productos**: SKU individuales o colecciones de SKU que representan bienes físicos o servicios intangibles con atributos que representan el producto, incluidos la descripción, el peso, el tamaño, las dimensiones, etc. Los atributos también especifican los ámbitos de canal y directiva de un SKU. Los productos se pueden agrupar en varios tipos de productos, como simple, configurable, paquete, paquete de paquetes, suscripciones, etc.
- **Metadatos**: los metadatos de atributos del producto definen y administran cómo se muestran los atributos del producto en la tienda en las listas de productos, las páginas de detalles, los resultados de búsqueda, etc. Los metadatos también definen cómo se utilizan los atributos de producto en las búsquedas (clasificación, filtrado, ponderaciones de búsqueda, etc.).
- **Libros de precios y precios** - Determina los precios de venta de los productos. En los Servicios de Comercialización, un unidad de almacén de producto y un precio están desacoplados, por lo tanto, usted está facultado para definir múltiples libros de precios para un solo unidad de almacén. Al desacoplar los precios de la unidad de almacén, puede desbloquear precios específicos de ámbito en diferentes niveles de clientes, unidades de negocio y geografías. Puede definir precios regulares y con descuento y administrar todo esto a escala.
- **&#x200B;**&#x200B;Assets: artefactos asociados con productos, como imágenes, videos, archivos PDF u otros tipos de archivos (hoja de ruta futura).

### Gestión del contexto del producto

La gestión del contexto del producto cubre los siguientes aspectos:

- **Canal**: el canal de distribución define la ruta por la que una empresa quiere vender productos. Un canal es la abstracción de nivel superior que encapsula configuraciones regionales y directivas.
   - Ejemplo: Distribuidores para la industria del automóvil. Filiales para conglomerados multimarca. Ubicación de fabricación para proveedores.
- **Directiva**: filtro de acceso a datos que te permite entregar el contenido correcto al destino correcto. Este concepto habilita las capacidades de distribución del catálogo.
   - Ejemplo: tiendas físicas, mercados, canalizaciones de anuncios (Google, Facebook, Instagram) del punto de venta
- **Ámbito** - Representa el idioma (configuración regional) para los catálogos, por ejemplo `en-US`. El ámbito se establece en un nivel de SKU durante la ingesta de datos del catálogo.

Durante la ingesta y actualización de datos del producto, un SKU contiene los detalles de ámbitos y atributos (los atributos se asignan a canales y directivas). Definen los identificadores de contexto de producto a los que pertenece un SKU:

![[!DNL Merchandising Services] identificadores de contexto de producto](../assets/merchandising-svcs-product-id.png)

En la imagen anterior, cada SKU proporciona:

- Identificadores de ámbito
   - Configuración regional: obligatorio
- Atributos del producto
   - Los atributos del producto se utilizan para asignarse a los canales y políticas relevantes
   - Ejemplo: Como fabricante de automóviles, puede optar por crear una combinación de canal y directiva para los atributos del producto: (1) Concesionarios (2) Marcas de automóviles.
- Precios y libros de precios asignados
   - Cada unidad de almacén puede tener múltiples precios definidos utilizando múltiples libros de precios.
   - Ejemplo: Usted oferta a los empleados un precio regular reducido en autopartes con un descuento adicional del 25%. Usted oferta VIP a los clientes un precio regular más alto con un descuento del 10%. La información de productos unidad de almacén precios garantiza que se muestre el precio correcto para cada cliente segmento.

Las definiciones canal y directiva se crean mediante API dedicadas:

![[!DNL Merchandising Services] Asignación de canal, política y ámbito](../assets/merchandising-svcs-scope-map.png)

- **Ámbito** (configuración regional): se establece en un nivel unidad de almacén durante la ingesta de datos del producto.
- **Canal** : definición creada mediante API dedicadas.
- **Política** : Definición creada mediante API dedicadas.

## Funciones principales

| Funciones principales | Beneficio |
|---|---|
| **Ingesta directa de datos de catálogo en la canalización** de servicios de escaparate: Ingiera los datos del catálogo directamente en la canalización del servicio de catálogo para la exploración del escaparate y el ciclo de vida del búsqueda (Página de visualización de productos, Lista de productos Página, Search Página de resultados, etc.). | <ul><li>Ingiera directamente datos de catálogo en la canalización de servicio de escaparate que alimenta: Servicio de catálogo, Descubrimiento de productos (Search en vivo) y Recommendations de productos. Con esto, puede entregar actualizaciones de catálogo a escala para millones de SKU. Esto desbloquea la gestión de promoción a gran escala sensible al tiempo. </li></ul> |
| **Nuevo alcance de los productos** del catálogo: Canal, directiva y ámbito son nuevos alcances de productos introducidos por los Servicios de comercialización. Estos ámbitos de producto sustituyen los ámbitos de sitio web, tienda y storeview de la capa de servicios de escaparate. [Más información](#product-context-management). | <ul><li>Con los nuevos ámbitos, los servicios de comercialización permiten ampliar fácilmente la aplicación a casos de uso de varias regiones geográficas, unidades de negocio, marcas múltiples e idiomas utilizando un único catálogo base.</li><li>Elimine la redundancia de datos en la administración de catálogos.</li></ul> |
| **Escalar a decenas de millones de SKU** | Desbloquee la administración del catálogo a escala. Aquí puede ingerir y administrar más de 200 MM de SKU con facilidad. |
| **Compatibilidad con tipo de producto** | <ul><li>Sencillo y configurable</li><li>Paquetes y paquetes de paquetes (hoja de ruta futura)</li><li>Suscripciones y planes (hoja de ruta futura)</li></ul> |
| **Comercio sin encabezado** | <ul><li>Compatibilidad total con implementaciones de comercio sin encabezado mediante el servicio de catálogo, la detección de productos (búsqueda en directo) y las API de recomendaciones de productos.</li></ul> |
| **Componentes modernos de la interfaz de usuario con gran rapidez** | <ul><li>Compatibilidad con los componentes de la interfaz de usuario predeterminados para la búsqueda de productos y recomendaciones de productos.</li><li>Los componentes IU son extensibles y flexibles para que puedan ser utilizados tanto por el servicio de entrega Edge de Adobe Systems como por cualquier otro implementación de escaparate.</li></ul> |

## ¿Qué tipo de comerciante se beneficia más de los servicios de comercialización?

La siguiente tabla destaca los desafíos comunes que enfrentan los comerciantes y cómo los servicios de comercialización impulsados por canales y políticas los abordan.

| Tipo de comerciante | Caso de uso | Problemas resueltos |
|---|---|---|
| Conglomerado multimarca | <ul><li>Venden varias marcas</li><li>Venden en varios países</li><li>Venden en diferentes idiomas</li></ul> | Utilice un único catálogo unificado base y logre la eficacia operativa a la vez que se expande a varias marcas, regiones geográficas e idiomas. |
| Conglomerado de piezas de automóvil/fabricación | <ul><li>Vende piezas de automóviles o máquinas. Los productos son los mismos para todos los clientes.</li><li>Diferentes distribuidores venden piezas a los clientes</li><li>Cada distribuidor tiene sus propios precios, stock y métodos de envío</li></ul> | Para tener diferentes integraciones de envío, cada distribuidor debe tener un sitio web separado. Sin embargo, los sitios web separados fuerzan al modelo de datos de catálogo típico a duplicar los datos. Así, si hay 3000 distribuidores en EE.UU., un comerciante crea 3000 copias de catálogo a pesar de que el mismo catálogo es utilizado por todos los distribuidores. Esta duplicación de datos interfiere con los límites de rendimiento. Los servicios de comercialización eliminan la duplicación de datos. |
| Empresa de embalaje/logística | <ul><li>Tienen varias ubicaciones de envío</li><li>Tienen un precio diferente para cada cliente</li><li>El mismo producto disponible en 2 ubicaciones para 2 clientes tiene 4 precios posibles</li></ul> | A pesar del uso de grupos de clientes para cubrir los precios por cliente, el modelo de datos de catálogo típico no tiene la capacidad de administrar los precios por ubicación. Además, los comerciantes quieren reglas de visibilidad únicas por ubicación/sitio web. La administración de reglas de visibilidad y precios tan complejas se puede desbloquear a escala con Servicios de comercialización. |

<!--### Where to go from here

- Ingest data into Merchandising Services using the [data ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/).
- Manage your catalog and define the channels, policies, and scopes using the [catalog management API](https://developer-stage.adobe.com/commerce/services/composable-catalog/admin/using-the-api/)
- [Complete a tutorial](https://developer-stage.adobe.com/commerce/services/composable-catalog/merchandising-services-use-case/) that shows how a company with a single base catalog can use the Merchandising Services APIs to add product data, define catalogs using projections, and retrieve the catalog data for display in a headless storefront.-->
