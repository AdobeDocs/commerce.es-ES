---
title: Capa de catálogo
description: Descubra cómo las capas de catálogo le permiten modificar los datos de producto sin cambiar los datos de origen originales, para que pueda personalizar con seguridad y revertir los cambios en cualquier momento.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 4a904527af172a5e35b87410135d55484d07ad84
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 0%

---

# Capa de catálogo

Las capas de catálogo permiten modificar los datos del producto sin cambiar los datos de origen originales. Las capas aplican cambios a atributos de producto específicos, como nombre, descripción, imágenes, vínculos y metadatos, creando una capa sobre el catálogo base. Los datos originales del producto permanecen intactos, lo que permite personalizar los productos de forma segura y revertir los cambios en cualquier momento.

![Capas de catálogo](../assets/catalog-layers.png)

## Cómo funcionan las capas del catálogo

Cuando un cliente ve su tienda, el sistema combina los datos del catálogo base con las capas de catálogo activas para mostrar la información final del producto. Así es como funciona el proceso:

1. **Aplicación de capa**: cuando se realiza una solicitud con un ID de canal y un ID de entorno, el servicio de tienda recupera la vista de catálogo correspondiente.

1. **Combinación de datos**: el sistema aplica capas de catálogo a los datos del producto en función del orden de prioridad de las capas.

1. **Control de campos**: los distintos tipos de campos se procesan de forma diferente:

   - **Sobrescribir campos**: los campos de texto como nombre, descripción y metatítulos se reemplazan por los valores definidos en la capa, teniendo prioridad la capa de mayor prioridad.
   - **Combinar campos**: los campos de matriz como imágenes, vínculos y atributos se combinan desde varias capas, lo que proporciona una respuesta unificada.

1. **Resolución de prioridad**: el campo de orden determina qué capa tiene prioridad. Cuando varias capas modifican el mismo campo, la capa con el número de orden inferior tiene mayor prioridad (por ejemplo, el orden 1 es el más alto).

## Casos de uso de capa de catálogo

Las capas de catálogo se utilizan comúnmente para:

- **Optimización de SEO**: anula los metatítulos y las descripciones de los productos según las recomendaciones de IA de [Sites Optimizer](../manage-results/opportunities.md).
- **Campañas de temporada**: actualice temporalmente nombres, descripciones o imágenes de productos para las promociones sin cambiar los datos de origen.
- **Personalización regional**: muestra información de producto diferente según la ubicación geográfica o el idioma.
- **Pruebas A/B**: Pruebe diferentes presentaciones de productos para optimizar las tasas de conversión.
- **Administración de varias marcas**: personalice los atributos del producto para las distintas vistas del catálogo de marcas.

## Adición de una capa de catálogo mediante ingesta de datos

Puede añadir capas de catálogo a los productos durante el proceso de ingesta de datos. Este método es ideal para operaciones masivas o flujos de trabajo automatizados.

>[!NOTE]
>
>Las capas de catálogo se importan mediante la API de ingesta, pero [la configuración del orden](#manage-layer-priorities) de las capas se realiza mediante la interfaz de usuario.

**Requisitos previos:**

- Credenciales de API con permiso para acceder al servicio de ingesta de datos
- SKU de producto que ya existen en su catálogo base

**Pasos:**

1. Prepare los datos de la capa en el formato requerido con los atributos de producto que desee modificar.

1. Utilice el punto final de la API de capas de producto para introducir los datos de capa.

1. Compruebe que la capa se ha introducido correctamente marcando la configuración de la vista del catálogo.

Para obtener especificaciones de API detalladas y ejemplos de carga útil, consulte [Capas de producto](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers) en la documentación para desarrolladores.

## Adición manual de una capa de catálogo en la interfaz de usuario

>[!NOTE]
>
>Esta función aún no está disponible.

La IU de vista de catálogo permite crear y administrar capas manualmente, lo que resulta especialmente útil para integraciones como Sites Optimizer que generan recomendaciones con tecnología de IA.

>[!NOTE]
>
>Si no existe una capa de Sites Optimizer en la vista de catálogo, la función de corrección automática de Sites Optimizer crea una y la asigna en el orden 1 (prioridad más alta). Si elimina esta capa, se volverá a crear la próxima vez que se ejecute la función de corrección automática en Sites Optimizer y cambiará las capas existentes a números de orden inferior. Si la capa de Sites Optimizer ya existe en un número de pedido diferente, la función de corrección automática no cambiará su prioridad.

>[!TIP]
>
>Para las operaciones de capa masiva, use el método de API de ingesta de datos [descrito anteriormente](#add-a-catalog-layer-via-data-ingestion).

**Para crear una capa manual:**

1. Vaya a **Configuración de tienda** > **Vistas de catálogo**.

1. Seleccione la vista de catálogo en la que desea aplicar la capa.

1. En la sección de capas de catálogo, haga clic en **Agregar capa de catálogo**.

1. Configure las propiedades de la capa:

   - **Nombre de capa**: escriba un nombre descriptivo para identificar el propósito de la capa.
   - **Productos**: seleccione los productos a los que se aplica esta capa.
   - **Atributos**: elija qué atributos de producto desea modificar (nombre, descripción, imágenes, etiquetas meta, etc.).
   - **Valores**: introduzca los nuevos valores para cada atributo seleccionado.

1. Haga clic en **Guardar** para crear la capa.

La nueva capa se añade a la vista de catálogo y se asigna automáticamente al siguiente número de pedido disponible.

## Previsualizar efectos de capa

>[!NOTE]
>
>Esta función aún no está disponible.

Antes de activar capas o cambiar prioridades, puede obtener una vista previa de cómo afectan a los datos del producto.

**Para obtener una vista previa de los cambios de capa:**

1. Vaya a **Configuración de tienda** > **Vistas de catálogo**.

1. Seleccione la vista de catálogo con las capas que desee previsualizar.

1. En la sección de capas de catálogo, seleccione un producto específico o utilice la función de previsualización.

1. Revise los datos de productos combinados que muestran cómo las capas modifican los valores del catálogo base.

1. Realice los ajustes necesarios en el contenido de la capa o en el orden de prioridad.

## Activar, desactivar o eliminar capas

Puede activar o desactivar las capas de catálogo sin eliminarlas, lo que le permite controlar cuándo se aplican personalizaciones específicas.

**Para activar o desactivar una capa:**

1. Vaya a **Configuración de tienda** > **Vistas de catálogo**.

1. Seleccione la vista de catálogo que contiene la capa.

1. En la sección de capas de catálogo, busque la capa que desee alternar.

1. Haga clic en el botón de activación para activar o desactivar la capa.

   - **Activo**: la capa se aplica a los datos del producto.
   - **Inactivo**: la capa se conserva, pero no se aplica a los datos del producto.

1. El cambio entra en vigor inmediatamente en tu tienda.

**Para eliminar una capa:**

Use la API de ingesta de datos para [eliminar una capa de catálogo](https://developer.adobe.com/commerce/services/reference/rest/#operation/deleteProductLayers).

## Administrar prioridades de capa

El orden en que se aplican las capas determina qué valores aparecen en la tienda cuando varias capas modifican el mismo atributo de producto. La administración de prioridades garantiza que se muestren los datos correctos.

**Explicación del orden de prioridad:**

- A cada capa se le asigna un número de orden (1, 2, 3, etc.)
- El orden 1 tiene la prioridad más alta y anula todas las demás capas
- Cuando varias capas modifican el mismo campo, la capa con el número de orden inferior tiene prioridad
- La prioridad solo se aplica a los campos de anulación (nombre, descripción, etiquetas meta)
- Los campos combinados (imágenes, vínculos, atributos) combinan datos de todas las capas

**Para reordenar las prioridades de la capa:**

1. Vaya a **Configuración de tienda** > **Vistas de catálogo**.

1. Seleccione la vista de catálogo que contiene las capas que desea reordenar.

1. En la sección de capas de catálogo, busque la capa que desee mover.

1. Arrastre y suelte la capa para cambiar su posición o utilice los controles de reordenación.

1. El sistema actualiza automáticamente los números de pedido en función de la nueva secuencia.

1. Haga clic en **Guardar** para aplicar el nuevo orden de prioridad.

>[!IMPORTANT]
>
>Los cambios en la prioridad de las capas se aplican inmediatamente y pueden afectar a lo que los clientes ven en la tienda. Revise la vista previa antes de guardar para asegurarse de que se aplican los valores correctos (**vista previa aún no está disponible**).

## Prácticas recomendadas

Siga estas recomendaciones al trabajar con capas de catálogo:

- **Use nombres descriptivos**: Asigne nombres a las capas claramente para indicar su propósito (por ejemplo, &quot;Campaña de vacaciones de 2025&quot; o &quot;Optimización de SEO: páginas de producto&quot;).

- **Limitar capas**: aunque el sistema admite varias capas, el uso de demasiadas puede afectar al rendimiento. Consolide las capas siempre que sea posible.

<!--- **Test before activating**—Always preview layer effects before activating them on your live storefront. !!!REMOVE IF PREVIEW NOT AVAILABLE FOR GA!!!-->

- **Lógica de prioridad de documento**: haga un seguimiento de las capas que deben tener prioridad para evitar invalidaciones no deseadas.

- **Revisar capas de Sites Optimizer**: cuando se utiliza la corrección automática desde Sites Optimizer, el sistema crea capas con la máxima prioridad. Tenga en cuenta al añadir capas manuales que puedan anular las recomendaciones de IA. Más información sobre cómo usar [Sites Optimizer](../manage-results/opportunities.md).

- **Supervisar el rendimiento**: si observa cargas lentas en la página del producto, revise la configuración de la capa y considere la posibilidad de consolidar las capas.

## Más parecido a esto

- [Vistas de catálogo](catalog-view.md) - Configurar vistas de catálogo para diferentes tiendas
- [Oportunidades](../manage-results/opportunities.md): obtenga información acerca de la optimización con tecnología de IA mediante capas de catálogo
