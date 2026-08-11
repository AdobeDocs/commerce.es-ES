---
title: Vistas de catálogo
description: Conozca cuáles son las vistas de catálogo y cómo crearlas para organizar el catálogo de productos por estructura empresarial, políticas y precios.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
nudge: true
source-git-commit: 38fa0734562a631fdcdd7510580571c5d37cb598
workflow-type: tm+mt
source-wordcount: 1276
ht-degree: 0%

---

# Vistas de catálogo de Servicios de comercialización

Una vista de catálogo define los productos y los precios que un cliente puede recuperar. Combina fuentes de catálogo, capas de catálogo, directivas y libros de precios para admitir diferentes marcas, regiones, unidades de negocio o canales.

## ¿Qué son las vistas de catálogo?

Las vistas de catálogo definen cómo se organiza y muestra el catálogo de productos. Actúan como filtros que determinan lo siguiente:

- **Qué productos son visibles** según la estructura de la empresa (marcas, regiones, distribuidores)
- **Qué precios se muestran** a través de los libros de precios vinculados
- **Cómo se filtran los productos** mediante directivas (atributos como marca, modelo y categoría)
- **El [origen del catálogo](catalog-sources.md) que se usa** según atributos como la configuración regional
- **Quién puede tener acceso a los datos de la vista** mediante [Protección de catálogo](private-catalog-view.md) y [claves de acceso restringido](restricted-access-keys.md)

Por ejemplo, puede crear vistas de catálogo independientes para:

- Una marca o unidad de negocio
- Una región geográfica
- Un distribuidor o canal de socios
- Un segmento de clientes con precios específicos

## Creación de una vista de catálogo

Antes de crear una vista de catálogo, prepare los siguientes elementos según sea necesario:

- Un [origen de catálogo](catalog-sources.md)
- [Directivas](policies.md) que definen los filtros de producto
- [Capas de catálogo](catalog-layer.md) si necesita anular los atributos del producto
- [Libros de precios](pricebooks.md) para los precios mostrados en la vista
- [Claves de acceso restringido](restricted-access-keys.md) si desea crear una vista de catálogo privado

### Configuración

En esta sección, crea una vista de catálogo, selecciona una [política](policies.md) y un [libro de precios](pricebooks.md).

1. En el menú de la izquierda, vaya a **[!UICONTROL Store setup]** y haga clic en **[!UICONTROL Catalog views]**.

1. Haga clic en **[!UICONTROL Create catalog view]**. &#x200B;

1. Configure los detalles de la vista del catálogo:

   - **Nombre**: escriba el nombre de la vista de catálogo, por ejemplo `Celport`. &#x200B;
   - **Orígenes de catálogo**: seleccione el [origen de catálogo](catalog-sources.md), por ejemplo `en-US`.
   - **Capas de catálogo**: revise las capas ingeridas y la prioridad.
   - **Directivas**: utilice la lista desplegable para seleccionar las directivas relevantes. Por ejemplo, &quot;Marca&quot;, &quot;Modelo&quot;. &#x200B;Asegúrese de que ya ha [creado una directiva](policies.md).

1. Seleccione el libro de precios que desea vincular a la vista de catálogo.

   - **Usar todos los libros de precios disponibles**: esta opción extrae los datos de precios de todos los libros de precios disponibles.
   - **Permitir solo los libros de precios seleccionados**—Esta opción muestra el cuadro de diálogo **Agregar libros de precios permitidos**. Utilice este cuadro de diálogo para seleccionar qué libro de precios específico se utilizará para la vista de catálogo.
   - **Deshabilitar precios**: esta opción no está disponible en este momento.

   >[!NOTE]
   >
   >Un ID de libro de precios controla qué precios se solicitan. No restringe el acceso a la vista del catálogo. Para restringir el acceso, habilite Protección de catálogo para crear una [vista de catálogo privado](private-catalog-view.md).

1. (Opcional) Cambie **[!UICONTROL Catalog Protection]** a **[!UICONTROL Enabled]** para restringir los datos de esta vista del catálogo a los clientes con un token firmado válido. Consulte [Proteger una vista de catálogo](private-catalog-view.md#protect-a-catalog-view) para ver los pasos de configuración.

1. Haga clic en **[!UICONTROL Add]** para crear la vista de catálogo con los libros de precios y las directivas vinculados.

La página Vistas de catálogo se actualiza para mostrar la nueva vista de catálogo&#x200B;

Después de completar estos pasos, la vista de catálogo ahora está configurada para mostrar productos y precios en función de las fuentes y directivas seleccionadas.

### Especificar vistas de catálogo para recomendaciones y reglas de descubrimiento de productos

Puede especificar una vista de catálogo al [crear unidades de recomendación](../merchandising/recommendations/create.md) o [reglas de comercialización](../merchandising/rules/add.md).

## Capas de catálogo

Las capas de catálogo permiten anular los atributos de producto seleccionados sin cambiar los datos del catálogo de origen. Utilice capas para personalizar nombres, descripciones, imágenes, vínculos o metadatos para una vista de catálogo.

Ver [capas de catálogo](catalog-layer.md).

## Hacer privada una vista de catálogo

De forma predeterminada, una vista de catálogo es pública para las aplicaciones cliente que pueden acceder a la API de comercialización de GraphQL. Para restringir el acceso, habilite **[!UICONTROL Catalog Protection]** para configurar una vista de catálogo privado.

Para obtener información sobre cómo proteger una vista de catálogo y comprobar que el acceso es obligatorio, consulte [Vistas de catálogo privadas](private-catalog-view.md).

## Administrar vistas de catálogo

Para actualizar o ver las propiedades de vistas de catálogo existentes, siga estas instrucciones.

### Edición de una vista de catálogo

1. En el área de trabajo **[!UICONTROL Catalog views]**, busque la vista de catálogo.
1. Para abrir el menú de acciones, seleccione (**[!UICONTROL ...]**).
1. Seleccione **[!UICONTROL Edit]** para acceder al editor de vista de catálogo.
1. Actualice el nombre, los orígenes de catálogo, las directivas, la información del libro de precios y la configuración de **[!UICONTROL Catalog Protection]** (incluidas las claves de acceso restringido asignadas) según sea necesario.
1. Haga clic en **[!UICONTROL Save]**.

### Eliminación de una vista de catálogo

1. En el área de trabajo **[!UICONTROL Catalog views]**, busque la vista de catálogo.
1. Para abrir el menú de acciones, seleccione (**[!UICONTROL ...]**).
1. Seleccione **[!UICONTROL Delete]**.
1. Confirme la eliminación.

   Cuando aparezca el diálogo de confirmación, haga clic en **[!UICONTROL Delete]**.

### Ver detalles de la vista del catálogo

Esta opción proporciona una forma rápida de ver todos los parámetros de vista de catálogo mientras se mantiene en la tabla **[!UICONTROL Catalog views]**.

En el área de trabajo **[!UICONTROL Catalog views]**, seleccione el ![icono de información](../assets/info-icon.png) de una vista de catálogo para ver los detalles de configuración.

![Detalles de vista de catálogo](../assets/catalog-view-details.png)

Desde aquí puede ver los detalles de configuración de la vista de catálogo, como:

- Ver ID
- Nombre
- Fuentes de catálogo
- Políticas
- Fecha de creación
- Datos modificados

Algunos de estos ajustes de configuración son necesarios al configurar la tienda o utilizar la API de ingesta de datos.

## Descripción general de arquitectura

Las vistas de catálogo forman parte del marco de servicios de comercialización que reemplaza el marco de sitio web, tienda y vista de tienda utilizado en las fundaciones de Adobe Commerce por un modelo más flexible:

![[!DNL Merchandising Services] arquitectura](../assets/merchandising-svcs-architecture.png)

### Cómo funciona

**1. Ingesta de datos**
Los datos de catálogo de PIM, ERP y otros sistemas se incorporan al marco de servicios de comercialización. Cada SKU contiene información de configuración regional y atributos de producto que se asignan a vistas de catálogo, políticas y configuraciones regionales. Para obtener más información sobre la ingesta de datos, consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/services/optimizer/).

**2. Catálogo base unificado**
Los datos introducidos crean un catálogo base unificado en la canalización de datos del servicio de catálogo. Esta fuente única elimina la duplicación de datos entre unidades empresariales.

**3. Vistas de catálogo**
Varias vistas de catálogo representan diferentes unidades de negocio (por ejemplo, Texas Retail, Texas Retail Seasonal). Las configuraciones regionales, las directivas y los libros de precios se pueden compartir en las vistas de catálogo para mayor flexibilidad.

**4. Entrega multicanal**
Los datos del catálogo filtrado se envían a destinos como Edge Delivery Services, mercados, plataformas publicitarias y microtiendas personalizadas. Para obtener más información sobre la entrega de datos del catálogo, consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/services/optimizer/).

Cuando una vista de catálogo tiene **[!UICONTROL Catalog Protection]** habilitado, la entrega a ese destino requiere un token firmado válido de una [clave de acceso restringido](restricted-access-keys.md) asignada; se deniegan las solicitudes no autorizadas en lugar de recibir los datos del catálogo.

### Componentes clave

| Componente | Finalidad | Ejemplo |
|---|---|---|
| **Vista de catálogo** | Unidad de negocio o canal de distribución | Red de distribuidores, Tienda regional |
| **Directiva** | Filtro de productos basado en atributos | Marca, modelo y categoría |
| **Configuración regional** | Configuración de idioma/región | en-US, fr-CA, es-MX |
| **Libro de precios** | Estructura de precios | Comercial, Mayorista, Empleado |
| **Clave de acceso restringido** | Credencial de token firmado que comunica el acceso a una vista de catálogo protegida | Clave del portal de socios, clave de precios B2B |

### Flujo de datos

1. **Ingesta**: datos de productos de sistemas PIM/ERP
2. **Proceso**: aplicar vistas de catálogo, directivas y precios
3. **Enviar**: sirve el catálogo filtrado a tiendas, mercados, etc.

## Características principales

| Función | Beneficio |
|---|---|
| **Catálogo base único** | Eliminar la duplicación de datos entre unidades empresariales |
| **Precios flexibles** | Varios libros de precios por SKU para diferentes segmentos de clientes |
| **Escalable** | Gestione más de 200 millones de SKU de forma eficaz |
| **Canal múltiple** | Ofrecer catálogos a tiendas, mercados y plataformas publicitarias. |
| **Actualizaciones en tiempo real** | Actualización rápida de los datos de catálogo para promociones y campañas |
| **Vistas del catálogo privado** | Restringir una vista de catálogo a clientes autorizados mediante la validación de token firmado |

## Casos de uso

### Conglomerado multimarca

**Desafío**: administra varias marcas, países e idiomas<br>
**Solución**: catálogo único con vistas de catálogo para cada combinación de marca y región

### Distribuidor de piezas de automóviles

**Desafío**: 3.000 distribuidores con los mismos productos pero precios diferentes<br>
**Solución**: Un catálogo con vistas de catálogo y libros de precios específicos del distribuidor

### Retailer con varias ubicaciones

**Desafío**: Diferentes precios e inventarios por ubicación<br>
**Solución**: vistas de catálogo basadas en ubicación con directivas específicas de región

>[!NOTE]
>
>Para obtener información detallada acerca de la ingesta y entrega de datos de catálogo, consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/services/optimizer/).

## Más parecido a esto

- [Fuentes de catálogo](catalog-sources.md): defina el ámbito autorizado de productos, atributos y categorías para el comportamiento de búsqueda, filtrado y ordenación
- [Capas de catálogo](catalog-layer.md): aprenda a modificar los datos de productos sin cambiar el origen original
- [Vistas de catálogo privado](private-catalog-view.md): cree una vista de catálogo privado para restringir el acceso a los clientes autorizados
- [Claves de acceso restringido](restricted-access-keys.md): cree, asigne y gire las claves utilizadas para firmar tokens para la protección del catálogo
- [Directivas](policies.md): cree directivas para filtrar productos en las vistas de catálogo
- [Libros de precios](pricebooks.md): administre estructuras de precios para diferentes segmentos de clientes
