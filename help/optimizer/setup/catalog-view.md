---
title: Vista de catálogo
description: Obtenga información sobre cómo crear y administrar vistas de catálogo en  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 553490762ef10e43ccce1654acec59aeb83bb5f9
workflow-type: tm+mt
source-wordcount: '1896'
ht-degree: 0%

---

# Crear vista de catálogo

[Las vistas de catálogo](#catalog-views) le ayudan a definir su estructura comercial en grupos comerciales significativos. Una vista de catálogo afecta a la visibilidad del producto al aplicar directivas y filtros específicos que determinan qué productos se muestran en una tienda. Estas políticas pueden incluir atributos como marca, modelo o categoría de artículo, lo que garantiza que solo los productos relevantes sean visibles para los compradores en función de la configuración de la vista de catálogo. Además, las vistas de catálogo pueden utilizar libros de precios para mostrar los precios específicos del cliente y adaptar aún más la experiencia de compra. [Más información](#catalog-views) sobre las vistas de catálogo.

En esta sección, crea una vista de catálogo, selecciona una [política](policies.md) y un [libro de precios](pricebooks.md).

1. En el menú de la izquierda, ve a _Configuración de la tienda_ y haz clic en **[!UICONTROL Catalog views]**.

1. Haga clic en **[!UICONTROL Create catalog view]**.

1. Añada los detalles de la vista del catálogo:

   - **Nombre**: escriba el nombre de la vista de catálogo. Por ejemplo, &quot;Celport&quot;. palo de golf
   - **Orígenes del catálogo**: agregue el origen del catálogo (configuración regional). Por ejemplo, &quot;en-US&quot;. Presione la tecla **enter**.
   - **Directivas**: utilice la lista desplegable para seleccionar las directivas relevantes. Por ejemplo, &quot;Marca&quot;, &quot;Modelo&quot;. palo de golfAsegúrese de que ya ha [creado una directiva](policies.md).

1. Seleccione el libro de precios que desea vincular a la vista de catálogo. Más información sobre [libros de precios](pricebooks.md).

1. Haga clic en **[!UICONTROL Add]** para crear la vista de catálogo con el libro de precios y las directivas vinculados.

   Si el botón **[!UICONTROL Add]** no está activo, asegúrese de que el origen del catálogo se agrega correctamente colocando el cursor en el campo Orígenes del catálogo y presionando **Intro**.

La página Vistas de catálogo se actualiza para mostrar la nueva vista de catálogo&#x200B;

Después de completar estos pasos, la nueva vista de catálogo se configura para mostrar los productos y los precios en función de las fuentes de catálogo y las directivas seleccionadas.

## Vistas de catálogo

Un catálogo de productos es esencial para las experiencias de compra en línea, lo que permite a los clientes examinar, buscar y realizar compras. Para lograr una mayor eficiencia operativa, un catálogo de productos debe reflejar fielmente la estructura empresarial de la empresa. Las empresas a menudo necesitan vender productos a precios variables en función del mercado geográfico, la vista del catálogo de distribución, el segmento del cliente y otras variables. Para dar cabida a esto, una plataforma de comercio electrónico debe ofrecer un modelo de datos de catálogo flexible que permita a las empresas producir variaciones de su catálogo adaptadas a estos escenarios. Adobe aborda estas necesidades ofreciendo servicios de comercialización basados en vistas de catálogo y políticas. Los servicios de comercialización ofrecen componentes básicos que los comerciantes pueden utilizar para crear y administrar catálogos a escala. Esto permite a las empresas configurar catálogos que se alinean con su estructura empresarial y estrategias de comercialización.

En un nivel superior, con los servicios de comercialización puede:

- Utilice un único catálogo base para todas sus necesidades empresariales. Escale su catálogo rápidamente entre nuevas marcas, mercados, unidades de negocio, vistas de catálogos de comercialización y segmentos de clientes sin necesidad de una reestructuración completa. Esto elimina la duplicación de datos y configura su plataforma de comercio electrónico para una alta eficiencia operativa.
- Desbloquee la distribución del catálogo y proporcione el contenido adecuado diseñando el catálogo de productos para que refleje su negocio, incluidos los productos, los clientes, los precios y la distribución.
- Ingeste y actualice rápidamente los datos del catálogo y envíe rápidamente las actualizaciones a la tienda para sus promociones y necesidades de campaña.
- Consiga puntuaciones perfectas en el faro con componentes de interfaz de usuario listos para usar y rápidos con la tecnología de Edge Delivery Services para una navegación y recomendaciones de productos sin problemas.
- Adopte una arquitectura componible moderna usando la arquitectura de extensibilidad de Adobe ([App Builder](https://experienceleague.adobe.com/es/playlists/commerce-get-started-app-builder-development)) para importar datos de productos y activar tiendas de comercio sin encabezado usando la [malla de API](https://experienceleague.adobe.com/es/playlists/commerce-get-started-app-builder-and-api-mesh) de Adobe.

>[!INFO]
>
>Para obtener más información acerca de las API disponibles en los servicios de comercialización que funcionan con las vistas y directivas del catálogo, consulte la [documentación para desarrolladores](https://developer-stage.adobe.com/commerce/services/composable-catalog).

## Arquitectura

Los servicios de comercialización ofrecidos por las vistas y directivas del catálogo son un modelo de datos de catálogo flexible y altamente escalable que desbloquea casos de uso en varios idiomas, unidades empresariales y marcas múltiples con facilidad. Este modelo reemplaza el uso de las fuentes del catálogo de productos clásico de Adobe Commerce (sitio web, tienda, vista de tienda) con las nuevas fuentes del catálogo de productos de Servicios de comercialización (vista de catálogo, directiva y configuración regional).

El diagrama siguiente proporciona una vista de alto nivel del marco de comercialización.

![[!DNL Merchandising Services] arquitectura](../assets/merchandising-svcs-architecture.png)

En la parte superior de este diagrama, los datos de catálogo (PIM, ERP, etc.) se incorporan al marco de servicios de comercialización. Estos datos de catálogo contienen SKU. Cada SKU contiene detalles de la fuente del catálogo (configuración regional) y atributos del producto, que se asignan a las nuevas fuentes de catálogo de productos de los servicios de comercialización (vistas de catálogo, directivas y configuración regional).

Cuando todos estos datos se incorporan al marco de trabajo de comercialización, el resultado es un nuevo catálogo base unificado que está disponible en la canalización de datos del servicio de catálogo. En la siguiente parte del diagrama, verá varias vistas de catálogo. Cada vista de catálogo representa una unidad de negocio. Por ejemplo, *comercio minorista de Texas*, *comercio minorista de Texas de temporada*, etc. Como puede ver, en el diagrama, las configuraciones regionales, las directivas y los libros de precios se pueden compartir en las vistas de catálogo&#x200B;

Por último, el diagrama muestra cómo se pueden mostrar estos datos de catálogo distintos en varias ubicaciones, como una tienda Edge Delivery Services, un mercado, una vista de catálogo de anuncios o una microtienda personalizada, entre otras.

Para obtener información sobre cómo introducir los datos del catálogo en comercialización mediante la API de ingesta de datos del catálogo y cómo configurar las configuraciones regionales, las directivas y los libros de precios mediante la API de reglas y la administración del catálogo, consulte [documentación para desarrolladores](https://developer-stage.adobe.com/commerce/services/composable-catalog/).

Para obtener más información sobre los conceptos que componen los servicios de comercialización, consulte las siguientes secciones.

## Administración del catálogo de productos

La administración del catálogo de productos abarca dos aspectos distintos: datos y contexto del producto. Servicios de Comercialización respeta la separación de estas funciones, ofreciendo una gestión independiente para cada uno.

- **Datos del producto** - ¿Qué producto se está vendiendo y a qué precio?
- **Contexto del producto** - ¿Quién le vende a quién y dónde?

![[!DNL Merchandising Services] aspectos](../assets/merchandising-svcs-parts.png)

### Datos del producto

Los datos del producto incluyen los siguientes tipos:

- **Productos**: SKU individuales o colecciones de SKU que representan bienes físicos o servicios intangibles con atributos que representan el producto, incluidos la descripción, el peso, el tamaño, las dimensiones, etc. Los atributos también especifican la vista del catálogo y los orígenes del catálogo de directivas para un SKU. Los productos se pueden agrupar en varios tipos de productos, como simple, configurable, paquete, paquete de paquetes, suscripciones, etc.
- **Metadatos**: los metadatos de atributos del producto definen y administran cómo se muestran los atributos del producto en la tienda en las listas de productos, las páginas de detalles, los resultados de búsqueda, etc. Los metadatos también definen cómo se utilizan los atributos de producto en las búsquedas (clasificación, filtrado, ponderaciones de búsqueda, etc.).
- **Libros de precios y precios** - Determina los precios de venta de los productos. En los servicios de comercialización, un SKU de producto y un precio están disociados, por lo que puede definir varios libros de precios para un único SKU. Al desvincular los precios del SKU, puede desbloquear los precios específicos de la fuente del catálogo en diferentes niveles de clientes, unidades de negocio y regiones geográficas. Puede definir precios regulares y con descuento y administrar todo esto a escala.
- **Assets**: artefactos asociados con productos, como imágenes, vídeos, PDF u otros tipos de archivo (hoja de ruta futura).

### Administración del contexto del producto

La administración del contexto del producto cubre los siguientes aspectos:

- **vista de catálogo**: la vista de catálogo de distribución define la ruta por la que una empresa desea vender productos. Una vista de catálogo es la abstracción de nivel superior que encapsula configuraciones regionales y directivas.
   - Ejemplo: Distribuidores para la industria del automóvil. Filiales para conglomerados multimarca. Ubicación de fabricación para proveedores.
- **Directiva**: filtro de acceso a datos que te permite entregar el contenido correcto al destino correcto. Este concepto habilita las capacidades de distribución del catálogo.
   - Ejemplo: tiendas físicas, mercados, canalizaciones de anuncios (Google, Facebook, Instagram) del punto de venta
- **origen del catálogo**: representa el idioma (configuración regional) de los catálogos, por ejemplo `en-US`. el origen del catálogo se establece en un nivel SKU durante la ingesta de datos del catálogo.

Durante la ingesta y actualización de datos del producto, un SKU contiene los detalles de las fuentes y los atributos del catálogo (los atributos se asignan a las vistas y directivas del catálogo). Definen los identificadores de contexto de producto a los que pertenece un SKU:

![[!DNL Merchandising Services] identificadores de contexto de producto](../assets/merchandising-svcs-product-id.png)

En la imagen anterior, cada SKU proporciona:

- identificadores de origen de catálogo&#x200B;
   - Configuración regional: obligatorio&#x200B;
- Atributos del producto
   - Los atributos de producto se utilizan para asignarlos a las vistas de catálogo y directivas relevantes&#x200B;
   - Ejemplo: Como fabricante de automóviles, puede elegir crear una vista del catálogo y una combinación de directivas para los atributos del producto: (1) Concesionarios (2) Marcas de automóviles&#x200B;
- Precios y libros de precios asignados
   - Cada SKU puede tener varios precios definidos utilizando varios libros de precios.
   - Ejemplo: ofrece a los empleados un precio regular reducido de las piezas de automóviles con un descuento adicional del 25%. Ofrece a los clientes de VIP un precio normal más alto con un descuento del 10%. La información del precio del SKU del producto garantiza que se muestre el precio correcto para cada segmento de clientes.

La vista de catálogo y las definiciones de directivas se crean mediante API dedicadas:

![[!DNL Merchandising Services] vista de catálogo, directiva y asignación de origen de catálogo](../assets/merchandising-svcs-scope-map.png)

- **origen del catálogo** (configuración regional): establecido en un nivel de SKU durante la ingesta de datos del producto&#x200B;
- **vista de catálogo**: definición creada con API dedicadas. palo de golf
- **Directiva**: definición creada con API dedicadas.

## Características principales

| Características principales | Beneficio |
|---|---|
| **Ingesta directa de datos de catálogo en la canalización de servicios de tienda**: Ingresa los datos de catálogo directamente en la canalización de servicios de catálogo para la navegación de tienda y el ciclo de vida de búsqueda (Página de visualización de producto, Página de lista de productos, Página de resultados de búsqueda, etc.). | <ul><li>Introduzca directamente datos de catálogo en la canalización de servicios de tienda, que alimenta: Servicio de catálogo, Descubrimiento de productos y Recommendations. Con esto, puede entregar actualizaciones de catálogo a escala para millones de SKU. Esto desbloquea la administración de promociones a gran escala con distinción de tiempo. </li></ul> |
| **Nuevos orígenes de catálogo de productos**: la vista de catálogo, la directiva y el origen de catálogo son nuevos orígenes de catálogo de productos introducidos por Servicios de comercialización. Estos orígenes de catálogo de productos reemplazan a los orígenes de catálogo de sitio web, tienda y vista de tienda en la capa de servicios de tienda. [Más información](#product-context-management). | <ul><li>Con las nuevas fuentes de catálogo, los servicios de comercialización permiten ampliar fácilmente la aplicación a casos de uso de varias regiones geográficas, unidades de negocio, marcas múltiples e idiomas utilizando un único catálogo base.</li><li>Elimine la redundancia de datos en la administración de catálogos.</li></ul> |
| **Escalar a decenas de millones de SKU** | Desbloquee la administración del catálogo a escala. Aquí puede ingerir y administrar más de 200 MM de SKU con facilidad. |
| **Compatibilidad con tipo de producto** | <ul><li>Sencillo y configurable</li><li>Paquetes y paquetes de paquetes (hoja de ruta futura)</li><li>Suscripciones y planes (hoja de ruta futura)</li></ul> |
| **Comercio sin encabezado** | <ul><li>Compatibilidad total con implementaciones de comercio sin encabezado mediante el servicio de catálogo, el descubrimiento de productos y las API de Recommendations.</li></ul> |
| **Componentes modernos de la interfaz de usuario con gran rapidez** | <ul><li>Compatibilidad con los componentes de la interfaz de usuario predeterminados para la búsqueda de productos y Recommendations.</li><li>Los componentes de la interfaz de usuario son ampliables y flexibles para que puedan utilizarse tanto en el servicio Edge Delivery de Adobe como en cualquier otra implementación de tienda.</li></ul> |

## ¿Qué tipo de comerciante se beneficia más de los servicios de comercialización?

En la tabla siguiente se destacan los desafíos comunes que encuentran los comerciantes y cómo los Servicios de comercialización basados en Vistas de catálogo y Políticas los resuelven.

| Tipo de comerciante | Caso de uso | Problemas resueltos |
|---|---|---|
| Conglomerado multimarca | <ul><li>Venden varias marcas</li><li>Venden en varios países</li><li>Venden en diferentes idiomas</li></ul> | Utilice un único catálogo unificado base y logre la eficacia operativa a la vez que se expande a varias marcas, regiones geográficas e idiomas. |
| Conglomerado de piezas de automóvil/fabricación | <ul><li>Vende piezas de automóviles o máquinas. Los productos son los mismos para todos los clientes.</li><li>Diferentes distribuidores venden piezas a los clientes</li><li>Cada distribuidor tiene sus propios precios, stock y métodos de envío</li></ul> | Para tener diferentes integraciones de envío, cada distribuidor debe tener un sitio web separado. Sin embargo, los sitios web separados fuerzan al modelo de datos de catálogo típico a duplicar los datos. Así, si hay 3000 distribuidores en EE.UU., un comerciante crea 3000 copias de catálogo a pesar de que el mismo catálogo es utilizado por todos los distribuidores. Esta duplicación de datos interfiere con los límites de rendimiento. Los servicios de comercialización eliminan la duplicación de datos. |
| Empresa de embalaje/logística | <ul><li>Tienen varias ubicaciones de envío</li><li>Tienen un precio diferente para cada cliente</li><li>El mismo producto disponible en 2 ubicaciones para 2 clientes tiene 4 precios posibles</li></ul> | A pesar del uso de grupos de clientes para cubrir los precios por cliente, el modelo de datos de catálogo típico no tiene la capacidad de administrar los precios por ubicación. Además, los comerciantes quieren reglas de visibilidad únicas por ubicación/sitio web. La administración de reglas de visibilidad y precios tan complejas se puede desbloquear a escala con Servicios de comercialización. |
