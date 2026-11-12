---
title: Vistas de catálogo
description: Conozca cuáles son las vistas de catálogo y cómo crearlas para organizar el catálogo de productos por estructura empresarial, políticas y precios.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y a [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
nudge: true
source-git-commit: d081e975b03805a0f46d5194f8c3cd46e3c86839
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%
---
# Vistas de catálogo de Servicios de comercialización

{{$include /help/_includes/ccdm-shared/setup/catalog-view.md}}

## Administrar vistas de catálogo

Siga estas instrucciones para administrar las vistas de catálogo:

- [Crear una vista de catálogo](#create-a-catalog-view): defina el nombre, el origen del catálogo, las directivas y el libro de precios. A continuación, [especifique la vista de catálogo para las recomendaciones y las reglas de detección de productos](#specify-catalog-views-for-recommendations-and-product-discovery-rules), revise [las capas de catálogo](#catalog-layers) que anulan los atributos de producto o [haga que la vista de catálogo sea privada](#make-a-catalog-view-private).
- [Editar una vista de catálogo](#edit-a-catalog-view): actualice sus orígenes, directivas, libro de precios y configuración de protección.
- [Eliminar una vista de catálogo](#delete-a-catalog-view): elimine una vista de catálogo que ya no necesite.
- [Ver detalles de vista de catálogo](#view-catalog-view-details): revise la configuración de una vista de catálogo desde la tabla Vistas de catálogo.

### Creación de una vista de catálogo

Antes de crear una vista de catálogo, prepare los siguientes elementos según sea necesario:

- Un [origen de catálogo](catalog-sources.md)
- [Directivas](policies.md) que definen los filtros de producto
- [Capas de catálogo](catalog-layer.md) si necesita anular los atributos del producto
- [Libros de precios](pricebooks.md) para los precios mostrados en la vista
- [Claves de acceso restringido](restricted-access-keys.md) si desea crear una vista de catálogo privado

#### Configuración

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
   - **Sólo libro de precios individual**—Seleccione esta opción si sólo se aplica un libro de precios. Esta opción es necesaria si desea configurar una vista de catálogo privado, que sólo puede hacer referencia a un libro de precios. Ver [Restricción del libro de precios en las vistas del catálogo privado](private-catalog-view.md#price-book-restriction-on-private-catalog-views).
   - **Deshabilitar precios**: esta opción no está disponible en este momento.

   >[!NOTE]
   >
   >Un ID de libro de precios controla qué precios se solicitan. No restringe el acceso a la vista del catálogo. Para restringir el acceso, habilite Protección de catálogo para crear una [vista de catálogo privado](private-catalog-view.md).

1. (Opcional) Cambie **[!UICONTROL Catalog Protection]** a **[!UICONTROL Enabled]** para restringir los datos de esta vista del catálogo a los clientes con un token firmado válido. Consulte [Proteger una vista de catálogo](private-catalog-view.md#protect-a-catalog-view) para ver los pasos de configuración.

1. Haga clic en **[!UICONTROL Add]** para crear la vista de catálogo con los libros de precios y las directivas vinculados.

La página Vistas de catálogo se actualiza para mostrar la nueva vista de catálogo&#x200B;

Después de completar estos pasos, la vista de catálogo ahora está configurada para mostrar productos y precios en función de las fuentes y directivas seleccionadas.

#### Especificar vistas de catálogo para recomendaciones y reglas de descubrimiento de productos

Puede especificar una vista de catálogo al [crear unidades de recomendación](../merchandising/recommendations/create.md) o [reglas de comercialización](../merchandising/rules/add.md).

#### Capas de catálogo

Las capas de catálogo permiten anular los atributos de producto seleccionados sin cambiar los datos del catálogo de origen. Utilice capas para personalizar nombres, descripciones, imágenes, vínculos o metadatos para una vista de catálogo.

Ver [capas de catálogo](catalog-layer.md).

#### Hacer privada una vista de catálogo

De forma predeterminada, una vista de catálogo es pública para las aplicaciones cliente que pueden acceder a la API de comercialización de GraphQL. Para restringir el acceso, habilite **[!UICONTROL Catalog Protection]** para configurar una vista de catálogo privado.

Para obtener información sobre cómo proteger una vista de catálogo y comprobar que el acceso es obligatorio, consulte [Vistas de catálogo privadas](private-catalog-view.md).

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

En el área de trabajo **[!UICONTROL Catalog views]**, seleccione el ![icono de información](/help/assets/ccdm-shared/recommendations/info-icon.png) de una vista de catálogo para ver los detalles de configuración.

![Detalles de vista de catálogo](../assets/catalog-view-details.png)

Desde aquí puede ver los detalles de configuración de la vista de catálogo, como:

- Ver ID
- Nombre
- Fuentes de catálogo
- Políticas
- Fecha de creación
- Datos modificados

Algunos de estos ajustes de configuración son necesarios al configurar la tienda o utilizar la API de ingesta de datos.
