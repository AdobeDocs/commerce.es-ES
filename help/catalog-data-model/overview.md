---
title: '[!DNL Composable Catalog Data Model]'
description: Descubra cómo  [!DNL Composable Catalog Data Model] for Adobe Commerce le ayuda a configurar su catálogo para que se ajuste a su modelo empresarial y a su estrategia de comercialización
hidefromtoc: true
hide: true
recommendations: noCatalog
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1626'
ht-degree: 0%

---

# [!DNL Composable Catalog Data Model]

Un catálogo de productos es esencial para las experiencias de compra en línea, lo que permite a los clientes examinar, buscar y realizar compras. Para lograr una mayor eficiencia operativa, un catálogo de productos debe reflejar fielmente la estructura empresarial de la empresa. Las empresas a menudo necesitan vender productos a precios variables en función del mercado geográfico, el canal de distribución, el segmento de clientes y otras variables. Para dar cabida a esto, una plataforma de comercio electrónico debe ofrecer un modelo de datos de catálogo flexible que permita a las empresas producir variaciones de su catálogo adaptadas a estos escenarios. El Modelo de datos de catálogo compuesto (CCDM) de Adobe Commerce aborda estas necesidades. CCDM proporciona bloques de creación que los comerciantes pueden utilizar para crear y administrar catálogos a escala. Esto permite a las empresas configurar catálogos que se alinean con su estructura empresarial y estrategias de comercialización.

En un nivel superior, con CCDM puede:

- Utilice un único catálogo base para todas sus necesidades empresariales. Escale su catálogo rápidamente entre nuevas marcas, mercados, unidades de negocio, canales de comercialización y segmentos de clientes sin necesidad de una reestructuración completa. Esto elimina la duplicación de datos y configura su plataforma de comercio electrónico para obtener una alta eficiencia operativa.
- Desbloquee la distribución del catálogo y proporcione el contenido adecuado diseñando el catálogo de productos para que refleje su negocio, incluidos los productos, los clientes, los precios y la distribución.
- Ingeste y actualice rápidamente los datos del catálogo y envíe rápidamente las actualizaciones a la tienda para sus promociones y necesidades de campaña.
- Consiga puntuaciones perfectas en el faro con componentes de interfaz de usuario listos para usar y rápidos con la tecnología de Edge Delivery Services para una navegación y recomendaciones de productos sin problemas.
- Adopte una arquitectura componible moderna usando la arquitectura de extensibilidad de Adobe ([App Builder](https://experienceleague.adobe.com/en/playlists/commerce-get-started-app-builder-development)) para importar datos de productos y activar tiendas de comercio sin encabezado usando la [malla de API](https://experienceleague.adobe.com/en/playlists/commerce-get-started-app-builder-and-api-mesh) de Adobe.

>[!INFO]
>
>Para obtener más información sobre las API disponibles en CCDM, consulte [documentación para desarrolladores](https://developer-stage.adobe.com/commerce/services/composable-catalog).

## Arquitectura

CCDM es un modelo de datos de catálogo flexible y altamente escalable que desbloquea casos de uso de varias marcas, unidades de varias empresas e idiomas con facilidad. El modelo reemplaza el uso de los ámbitos de producto clásicos de Adobe Commerce (sitio web, tienda, vista de tienda) con nuevos ámbitos de producto de CCDM (canal, directiva y configuración regional).

En el diagrama siguiente se ofrece una vista de alto nivel del marco del MDL.

![[!DNL Composable Catalog Data Model] arquitectura](assets/ccdm-architecture.png)

En la parte superior de este diagrama, los datos de catálogo (PIM, ERP, etc.) se incorporan al marco de CCDM. Estos datos de catálogo contienen SKU. Cada SKU contiene detalles de ámbito (configuración regional) y atributos de producto, que se asignan a los nuevos ámbitos de producto de CCDM (canales, directivas y configuración regional).

Cuando todos estos datos se incorporan al marco de trabajo de CCDM, el resultado es un nuevo catálogo base unificado que está disponible en la canalización de datos del servicio de catálogo. En la siguiente parte del diagrama, verá varios canales. Cada canal representa una unidad empresarial. Por ejemplo, *comercio minorista de Texas*, *comercio minorista de Texas de temporada*, etc. Como puede ver en el diagrama, las configuraciones regionales, las directivas y los libros de precios se pueden compartir en todos los canales&#x200B;

Por último, el diagrama muestra cómo se pueden mostrar estos datos de catálogo distintos en varias ubicaciones, como una tienda Edge Delivery Services, un mercado, un canal de publicidad, una microtienda personalizada, etc.

Para obtener información sobre cómo introducir los datos del catálogo en CCDM mediante la API de ingesta de datos del catálogo y cómo configurar las configuraciones regionales, las directivas y los libros de precios mediante la API de reglas y la administración del catálogo, consulte [documentación para desarrolladores](https://developer-stage.adobe.com/commerce/services/composable-catalog/).

Para obtener más información sobre los conceptos que componen CCDM, consulte las secciones siguientes.

## Administración del catálogo de productos

La administración del catálogo de productos abarca dos aspectos distintos: datos y contexto del producto. El MDL respeta la separación de estas funciones y ofrece una gestión independiente para cada una de ellas.

- **Datos del producto** - ¿Qué producto se está vendiendo y a qué precio?
- **Contexto del producto** - ¿Quién le vende a quién y dónde?

![[!DNL Composable Catalog Data Model] aspectos](assets/ccdm-parts.png)

### Datos del producto

Los datos del producto incluyen los siguientes tipos:

- **Productos**: SKU individuales o colecciones de SKU que representan bienes físicos o servicios intangibles con atributos que representan el producto, incluidos la descripción, el peso, el tamaño, las dimensiones, etc. Los atributos también especifican los ámbitos de canal y directiva de un SKU. Los productos se pueden agrupar en varios tipos de productos, como simple, configurable, paquete, paquete de paquetes, suscripciones, etc.
- **Metadatos**: los metadatos de atributos del producto definen y administran cómo se muestran los atributos del producto en la tienda en las listas de productos, las páginas de detalles, los resultados de búsqueda, etc. Los metadatos también definen cómo se utilizan los atributos de producto en las búsquedas (clasificación, filtrado, ponderaciones de búsqueda, etc.).
- **Libros de precios y precios** - Determina los precios de venta de los productos. En CCDM, un SKU de producto y un precio están disociados, por lo que puede definir varios libros de precios para un único SKU. Al desvincular los precios del SKU, puede desbloquear los precios específicos del ámbito en diferentes niveles de clientes, unidades de negocio y regiones geográficas. Puede definir precios regulares y con descuento y administrar todo esto a escala.
- **Assets**: artefactos asociados con productos, como imágenes, vídeos, PDF u otros tipos de archivo (hoja de ruta futura).

### Administración del contexto del producto

La administración del contexto del producto cubre los siguientes aspectos:

- **Canal**: el canal de distribución define la ruta por la que una empresa quiere vender productos. Un canal es la abstracción de nivel superior que encapsula configuraciones regionales y directivas.
   - Ejemplo: Distribuidores para la industria del automóvil. Filiales para conglomerados multimarca. Ubicación de fabricación para proveedores.
- **Directiva**: filtro de acceso a datos que te permite entregar el contenido correcto al destino correcto. Este concepto habilita las capacidades de distribución del catálogo.
   - Ejemplo: tiendas físicas, mercados, canalizaciones de anuncios (Google, Facebook, Instagram) del punto de venta
- **Ámbito** - Representa el idioma (configuración regional) para los catálogos, por ejemplo `en-US`. El ámbito se establece en un nivel de SKU durante la ingesta de datos del catálogo.

Durante la ingesta y actualización de datos del producto, un SKU contiene los detalles de ámbitos y atributos (los atributos se asignan a canales y directivas). Definen los identificadores de contexto de producto a los que pertenece un SKU:

![[!DNL Composable Catalog Data Model] identificadores de contexto de producto](assets/ccdm-product-id.png)

En la imagen anterior, cada SKU proporciona:

- Identificadores de ámbito&#x200B;
   - Configuración regional: obligatorio&#x200B;
- Atributos del producto
   - Los atributos del producto se utilizan para asignarlos a los canales y directivas relevantes&#x200B;
   - Ejemplo: Como fabricante de automóviles, puede elegir crear una combinación de canal y política para los atributos del producto: (1) Concesionarios (2) Marcas de automóviles&#x200B;
- Precios y libros de precios asignados
   - Cada SKU puede tener varios precios definidos mediante varios libros de precios.
   - Ejemplo: ofrece a los empleados un precio regular reducido de las piezas de automóviles con un descuento adicional del 25%. Ofrece a los clientes de VIP un precio normal más alto con un descuento del 10%. La información del precio del SKU del producto garantiza que se muestre el precio correcto para cada segmento de clientes.

Las definiciones de canal y política se crean mediante API dedicadas:

Asignación de canal, directiva y ámbito de ![[!DNL Composable Catalog Data Model]](assets/ccdm-scope-map.png)

- **Ámbito** (configuración regional): establecido en un nivel de SKU durante la ingesta de datos del producto&#x200B;
- **Canal**: definición creada con API dedicadas. palo de golf
- **Directiva**: definición creada con API dedicadas.

## Características principales

| Características principales | Beneficio |
|---|---|
| **Ingesta directa de datos de catálogo en la canalización de servicios de tienda**: Ingresa los datos de catálogo directamente en la canalización de servicios de catálogo para la navegación de tienda y el ciclo de vida de búsqueda (Página de visualización de producto, Página de lista de productos, Página de resultados de búsqueda, etc.). | <ul><li>Introduzca directamente datos de catálogo en la canalización de servicios de tienda que alimenta: Servicio de catálogo, Descubrimiento de productos (Live Search) y Recomendaciones de productos. Con esto, puede entregar actualizaciones de catálogo a escala para millones de SKU. Esto desbloquea la administración de promociones a gran escala con distinción de tiempo. </li></ul> |
| **Nuevos ámbitos de producto de catálogo**: El canal, la directiva y el ámbito son nuevos ámbitos de producto introducidos por CCDM. Estos ámbitos del producto reemplazan los ámbitos del sitio web, el almacén y la vista de tienda en la capa de servicios de tienda. [Más información](#product-context-management). | <ul><li>Con los nuevos ámbitos, CCDM libera la capacidad de ampliación para casos de uso de varias regiones geográficas, unidades de varias empresas, marcas múltiples e idiomas con facilidad mediante un único catálogo base.</li><li>Elimine la redundancia de datos en la administración de catálogos.</li></ul> |
| **Escalar a decenas de millones de SKU** | Desbloquee la administración del catálogo a escala. Aquí puede ingerir y administrar más de 200 MM de SKU con facilidad. |
| **Compatibilidad con tipo de producto** | <ul><li>Sencillo y configurable</li><li>Paquetes y paquetes de paquetes (hoja de ruta futura)</li><li>Suscripciones y planes (hoja de ruta futura)</li></ul> |
| **Comercio sin encabezado** | <ul><li>Compatibilidad total con implementaciones de comercio sin encabezado mediante el servicio de catálogo, la detección de productos (búsqueda en directo) y las API de recomendaciones de productos.</li></ul> |
| **Componentes modernos de la interfaz de usuario con gran rapidez** | <ul><li>Compatibilidad con los componentes de la interfaz de usuario predeterminados para la búsqueda de productos y recomendaciones de productos.</li><li>Los componentes de la interfaz de usuario son ampliables y flexibles para que puedan utilizarse tanto en el servicio Edge Delivery de Adobe como en cualquier otra implementación de tienda.</li></ul> |

## ¿Qué tipo de comerciante se beneficia más del CCDM?

En la tabla siguiente se destacan los desafíos comunes que encuentran los comerciantes y cómo los aborda CCDM.

| Tipo de comerciante | Caso de uso | Problemas resueltos |
|---|---|---|
| Conglomerado multimarca | <ul><li>Venden varias marcas</li><li>Venden en varios países</li><li>Venden en diferentes idiomas</li></ul> | Utilice un único catálogo unificado base y logre la eficacia operativa a la vez que se expande a varias marcas, regiones geográficas e idiomas. |
| Conglomerado de piezas de automóvil/fabricación | <ul><li>Vende piezas de automóviles o máquinas. Los productos son los mismos para todos los clientes.</li><li>Diferentes distribuidores venden piezas a los clientes</li><li>Cada distribuidor tiene sus propios precios, stock y métodos de envío</li></ul> | Para tener diferentes integraciones de envío, cada distribuidor debe tener un sitio web separado. Sin embargo, los sitios web separados fuerzan al modelo de datos de catálogo típico a duplicar los datos. Así, si hay 3000 distribuidores en EE.UU., un comerciante crea 3000 copias de catálogo a pesar de que el mismo catálogo es utilizado por todos los distribuidores. Esta duplicación de datos interfiere con los límites de rendimiento. CCDM elimina la duplicación de datos. |
| Empresa de embalaje/logística | <ul><li>Tienen varias ubicaciones de envío</li><li>Tienen un precio diferente para cada cliente</li><li>El mismo producto disponible en 2 ubicaciones para 2 clientes tiene 4 precios posibles</li></ul> | A pesar del uso de grupos de clientes para cubrir los precios por cliente, el modelo de datos de catálogo típico no tiene la capacidad de administrar los precios por ubicación. Además, los comerciantes quieren reglas de visibilidad únicas por ubicación/sitio web. La gestión de reglas de precio y visibilidad tan complejas se puede desbloquear a escala con CCDM. |

### A dónde ir desde aquí

- Ingresar datos en CCDM usando la [API de ingesta de datos](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/).
- Administre su catálogo y defina los canales, directivas y ámbitos mediante la [API de administración de catálogos](https://developer-stage.adobe.com/commerce/services/composable-catalog/admin/using-the-api/)
- [Complete un tutorial](https://developer-stage.adobe.com/commerce/services/composable-catalog/ccdm-use-case/) que muestra cómo una empresa con un único catálogo base puede usar las API de CCDM para agregar datos de productos, definir catálogos mediante proyecciones y recuperar los datos del catálogo para mostrarlos en una tienda sin encabezado.
