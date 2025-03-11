---
title: Notas de la versión [!DNL Live Search]
description: La información de la versión más reciente de  [!DNL Live Search]  de Adobe Commerce.
feature: Services, Search, Release Notes
exl-id: 099cf79c-968c-4381-b66d-7f6141ad2db3
source-git-commit: eb016fa8e53cfb9d035d73979495171feccb764f
workflow-type: tm+mt
source-wordcount: '2186'
ht-degree: 0%

---

# Notas de la versión [!DNL Live Search]

Estas notas de la versión describen las versiones más recientes de [!DNL Live Search].
Se proporciona soporte para la versión publicada principal actual. Las notas de la versión de las versiones anteriores se proporcionan como referencia.
Las actualizaciones incluyen:

![Nuevas](../assets/new.svg) nuevas características
![Corrección](../assets/fix.svg) Correcciones y mejoras
![Error](../assets/bug.svg) Problemas conocidos

## Actualizaciones de servicios alojados

Estas notas describen las actualizaciones que se publicaron fuera de una versión con versiones o las mejoras realizadas en el servicio alojado.

_20 de febrero de 2025_

![Nuevo](../assets/new.svg) Commerce admite sinónimos de varias palabras. [Más información](synonyms-type.md#multi-word-synonym-behavior). La compatibilidad con sinónimos de varias palabras solo está disponible después de esta fecha de lanzamiento del 20 de febrero. Cualquier sinónimo de varias palabras existente requiere un reíndice completo para funcionar, que puedes solicitar al [crear un ticket de asistencia](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

_31 de enero de 2025_

![Nuevo](../assets/new.svg): hay una nueva directiva de retención de datos para los datos de catálogo no consultados en el entorno de prueba. [Más información](overview.md#catalog-data-retention-policy).

_19 de septiembre de 2024_

![Nuevo](../assets/new.svg) lanzó una versión beta que admite tres nuevas funciones de búsqueda: con capas, empieza por y contiene. [Más información](install.md#install-the-live-search-beta).

_4 de septiembre de 2024_

![Corrección](../assets/fix.svg) ha aumentado el número máximo de contenedores que se pueden devolver [dentro de una faceta](boundaries-limits.md#facets) a 100.

_7 de agosto de 2024_

![Corrección](../assets/fix.svg): se ha aumentado el valor de intervalo máximo o el intervalo de precios de [facetado de precios](settings.md#price-faceting) de 10 000 a 40 000 000.

_13 de febrero de 2024_

![Nuevo](../assets/new.svg) [!DNL Live Search] ahora admite la configuración de una regla predeterminada para [Buscar comercialización](rules.md).

_12 de octubre de 2023_

![Nuevos](../assets/new.svg) administradores de Commerce ahora pueden especificar el idioma del índice para [!DNL Live Search]. Ver [Configuración](settings.md).
![Corrección](../assets/fix.svg): Se cambió el nombre de la pestaña &quot;Reglas de búsqueda&quot; a &quot;Buscar comercialización&quot;.

_13 de junio de 2023_

![Corregir](../assets/fix.svg) Se corrigió un problema por el cual algunos caracteres como comillas o apóstrofos causaban problemas de clasificación. La reindexación resuelve estos problemas.

_25 de abril de 2023_

![Nuevos](../assets/new.svg) [!DNL Live Search] clientes ahora pueden aprovechar el nuevo [indexador de precios SaaS](../price-index/price-indexing.md).

### Widget PLP

_31 de mayo de 2024_

![Nuevo](../assets/new.svg) Lanzamiento de la versión 2.0.0 del widget PLP, que agrega compatibilidad con las siguientes características:

- Botones Añadir al carrito: disponible solo para productos simples.
- Varias imágenes por producto: la imagen puede cambiar cuando se elige un color diferente para un producto configurable.

_27 de octubre de 2023_

![Nuevo](../assets/new.svg) El widget PLP [!DNL Live Search] ahora admite muestras de color.

## [!DNL Live Search] 4.3.0

_11 de marzo de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"}

![Corrección](../assets/fix.svg) [!DNL Live Search] ahora es compatible con PHP 8.4 para instalaciones que ejecutan Adobe Commerce 2.4.8-beta2.
![Corrección](../assets/fix.svg) Se ha corregido un problema por el que el adaptador de búsqueda no era compatible con `psr/http-message:2.0`.

## [!DNL Live Search] 4.2.3

_13 de febrero de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"}

![Corrección](../assets/fix.svg) Se ha corregido un problema por el que a la página de detalles de pedido le faltaban el número de pedido, la fecha y el botón **[!UICONTROL Reorder]**.

## [!DNL Live Search] 4.2.2

_6 de enero de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"}

![Corregir](../assets/fix.svg) Se ha corregido un problema que causaba un error con la consulta GraphqL `categoryList` en la versión 2.4.5 y anteriores de Adobe Commerce.

## [!DNL Live Search] 4.2.1

_31 de julio de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"}

![Corregir](../assets/fix.svg) Se corrigió un problema en el cual algunos scripts no se cargaban en la página de cierre de compra.
![Corrección](../assets/fix.svg) Se ha corregido una versión de dependencia en el archivo `composer.json`.

## [!DNL Live Search] 4.2.0

_31 de mayo de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"}

![Nueva](../assets/new.svg) extensión de Live Search actualizada para usar widgets PLP versión 2.0.0.

## [!DNL Live Search] 4.1.2

_16 de mayo de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"}

### Actualizaciones

![Corrección](../assets/fix.svg) Se ha corregido la consulta de GraphQL [`productSearch`](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#filtering-by-categories) para que filtre correctamente en función de `categoryPath` y `categoryList` para las categorías.

## [!DNL Live Search] 4.1.1

_19 de marzo de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"}

### Nuevas funciones

![Nuevo](../assets/new.svg) agregó compatibilidad con el idioma polaco.
![Nuevo](../assets/new.svg) [!DNL Live Search] ahora es compatible con PHP 8.3 para instalaciones que ejecutan Adobe Commerce 2.4.4.

## [!DNL Live Search] 4.1.0

_22 de febrero de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"}

### Nuevas funciones

![Nuevo](../assets/new.svg) El [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard) ya está disponible. Este panel modificado proporciona información sobre las secuencias de datos de [!DNL Product Recommendations], [!DNL Live Search] y [!DNL Catalog Service].

### Actualizaciones

![Corregir](../assets/fix.svg) Se ha corregido un problema que causaba un error cuando los usuarios invitados agregaban productos a un carro de compras en vistas de tiendas no predeterminadas.
![Corrección](../assets/fix.svg) Se ha corregido un problema que hacía que la ventana emergente de búsqueda siempre mostrara el símbolo de moneda delante del valor de precio, independientemente de la configuración regional.
![Corrección](../assets/fix.svg) eliminó definiciones de tipo innecesarias para los complementos principales deshabilitados a fin de corregir los problemas de compatibilidad en la instalación.

## [!DNL Live Search] 4.0.0

_13 de noviembre de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"}

### Nuevas funciones

![Nuevo](../assets/new.svg) [!DNL Live Search] ahora admite muestras de color en el widget PLP.
![Nuevo](../assets/new.svg) [!DNL Live Search] ahora muestra el nombre de la categoría en lugar del Id. de categoría.
![Nuevo](../assets/new.svg) [!DNL Live Search] ahora admite el tachado de precios en el widget PLP.
![Nuevo](../assets/new.svg) introdujo el botón &quot;Ocultar filtros&quot; para ocultar el panel de filtros.


### Actualizaciones

![Corrección](../assets/fix.svg) El widget PLP [!DNL Live Search] ahora está habilitado de forma predeterminada para las nuevas instalaciones.
![Corrección](../assets/fix.svg) El adaptador de búsqueda está obsoleto. En adelante, el adaptador de búsqueda solo se actualizará para abordar los problemas de seguridad.
![Corregir](../assets/fix.svg) estilos CSS reconfigurados para aislar mejor las clases de widgets.
![Corregir](../assets/fix.svg) correcciones de errores menores

Después de instalar la versión 3.1.1 o superior de, habilite los nuevos indexadores:

- Fuente de precios de productos
- Fuente de datos del sitio web Ámbitos
- Fuente de datos de grupos de clientes ámbitos

Después de la actualización, pruebe la configuración actualizada en Control de calidad o Ensayo antes de insertar los cambios en producción.

+++3.1.1 y anteriores

### [!DNL Live Search] 3.1.1

_15 de septiembre de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"}

![Nueva](../assets/new.svg) nueva pestaña de comercialización de categoría. Los usuarios ahora pueden añadir clasificaciones inteligentes y clasificaciones manuales (fijar, aumentar, enterrar, ocultar) por categoría
![Nuevo](../assets/new.svg) Los usuarios pueden agregar una sola regla de categoría con clasificación inteligente o manual
![Nuevos](../assets/new.svg) usuarios ahora pueden agregar reglas de clasificación inteligente a las subcategorías
![Se proporciona información detallada](../assets/new.svg) nueva al eliminar subcategorías con clasificación inteligente
![Nuevo](../assets/new.svg) agregó la capacidad de eliminar reglas para estrategias de clasificación heredadas
![Nuevo](../assets/new.svg) agregó la capacidad de eliminar reglas para una sola categoría
![Nuevos](../assets/new.svg) usuarios ahora pueden buscar por nombre de categoría al agregar una regla
![Nuevo](../assets/new.svg): con la vista de árbol de categorías, los usuarios ahora pueden ver qué categoría tiene reglas aplicadas.
![Nueva](../assets/new.svg) vista previa de categoría solo muestra la categoría seleccionada.
Los componentes ![Nuevo](../assets/new.svg) AEM CIF [Widget emergente](https://github.com/adobe/aem-cif-guides-venia/pull/319) y [Widget PLP](https://github.com/adobe/aem-cif-guides-venia/pull/320) permiten que los sitios de AEM se beneficien de [!DNL Live Search].

#### Actualizaciones

![Corrección](../assets/fix.svg) El tamaño de tabla de las fuentes Products y Price se ha reducido considerablemente. Las tablas `catalog_data_exporter_products` y `catalog_data_exporter_product_prices` deberían ver una reducción de tamaño sustancial.
![Corrección](../assets/fix.svg): Se cambió el nombre de la ficha &#39;Reglas&#39; a &#39;Reglas de búsqueda&#39;
![Corregir](../assets/fix.svg) Al clasificar por &quot;tendencias&quot;, ahora puede elegir entre:
- 3 días (predeterminado)
- 14 días
- 30 días
![Corregir](../assets/fix.svg) &#39;Eventos&#39; (Boost/Pin/Bury/Hide) se ha cambiado a &#39;Clasificación manual&#39;.
![Corrección](../assets/fix.svg) &#39;Tipo de clasificación&#39; ha pasado a llamarse &#39;Clasificación inteligente&#39;
![Corregir](../assets/fix.svg) correcciones de errores menores

### [!DNL Live Search] 3.1.0

_1 de septiembre de 2023_

[!BADGE Compatible]{type="Informativo" tooltip="Admitido"}

#### Actualizaciones

![Corrección](../assets/fix.svg): El widget de lista de productos se ha actualizado para usar la [API de servicio de catálogo](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/).

### [!DNL Live Search] 3.0.2

_7 de agosto de 2023_

[!BADGE Compatible]{type="Informativo" tooltip="Admitido"}

#### Nuevas funciones

![Nuevo](../assets/new.svg) Los siguientes valores se han agregado al objeto `storeDetails`:

- &quot;Permitir todos los productos por página&quot;
- Tipo de cambio
- &quot;Productos por página en la cuadrícula Valores permitidos&quot;
- &quot;Productos por página en valor predeterminado de cuadrícula&quot;
- Idioma del almacén

#### Actualizaciones

![Corrección](../assets/fix.svg) Los módulos del servicio de catálogo se han agregado al metapaquete para admitir la recuperación avanzada de datos.
![Corregir](../assets/fix.svg) La navegación por la página de **Mi cuenta** ya no desaparece al usar el widget de página de lista de productos.

Los comerciantes deben actualizar la versión de la extensión [!DNL Live Search] >= 3.0.2 para tener acceso a estas características.

Se recomienda actualizar y probar antes de pasar a producción. Considere la posibilidad de actualizar el entorno de producción durante las horas de menor actividad después de verificar los resultados de su entorno de prueba.

#### Limitaciones

El uso del widget de página de lista de productos de Live Search provoca que Google Tag Manager falle. Utilice el adaptador de búsqueda predeterminado si se necesita el Administrador de etiquetas de Google.

### [!DNL Live Search] 3.0.1

_14 de marzo de 2023_

[!BADGE Compatible]{type="Informativo" tooltip="Admitido"}

#### Nuevas funciones

![Nueva](../assets/new.svg) tarjeta de producto en vista previa de reglas
![Nuevo](../assets/new.svg) [widget de página de lista de productos](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-storefront/plp-styling)
![Nuevas](../assets/new.svg) [Opciones de filtrado de categorías](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#facets)
![Nuevo](../assets/new.svg) Se agregó la capacidad de arrastrar y soltar para crear eventos Pin
![Nuevas](../assets/new.svg) nuevas acciones de anclaje:
- Pin to spot - Botón Pin para crear un evento Pin con un clic
- Pin to top - Coloca el producto en la primera posición
- Anclar a la parte inferior: coloca el producto en la parte inferior de los resultados
- Desanclar un evento con un clic
![Nuevo](../assets/new.svg) [Clasificación inteligente para reglas](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/rules/rules-add)
![Nuevo](../assets/new.svg) [!DNL Live Search] ahora admite capacidades completas de [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) en Commerce (anteriormente conocido como Multi-Source Inventory o MSI). Para habilitar la compatibilidad total, debe [actualizar](install.md#update) el módulo de dependencia `commerce-data-export` a la versión 102.2.0+.

#### Actualizaciones

![Corregir](../assets/fix.svg) Configurar reglas ahora ordena automáticamente las posiciones de forma única
![Corrección](../assets/fix.svg) Al eliminar un evento existente, ahora se actualiza la vista previa
![Corregir](../assets/fix.svg) reglas sin eventos pueden guardarse
![Corregir](../assets/fix.svg) Quitar selector de &quot;Seleccionar tipo&quot; de facetas
![Corregir](../assets/fix.svg) Se agregó el nuevo estado &quot;Editando&quot; para las reglas no guardadas

#### Correcciones

![Corregir](../assets/fix.svg) Se corrigió un error del servidor cuando hay un evento no finalizado durante la operación de guardar
![Corrección](../assets/fix.svg) Se corrigió al eliminar correctamente un evento específico cuando hay varios eventos
![Corrección](../assets/fix.svg): se ha corregido el evento de regla existente que no se actualizaba cuando se agregaba un nuevo evento
![Corrección](../assets/fix.svg) corregido en el segundo clic de &quot;Editar&quot; de los detalles, la página [!DNL Live Search] requiere recarga
![Corregir](../assets/fix.svg) sinónimos: se corrigió un problema cuando un usuario hacía clic fuera de la entrada y no podía devolver el enfoque al campo
![Corrección](../assets/fix.svg) Otras correcciones de errores menores y actualizaciones de rendimiento
![Error](../assets/bug.svg): la clasificación por &quot;Recomendado para ti&quot; solo es compatible con los widgets de Live Search. No es compatible con la funcionalidad de búsqueda predeterminada de Luma y PWA.
![Error](../assets/bug.svg): las facetas de atributo de precio personalizadas no se representan correctamente en Luma, pero la API filtra correctamente en ellas.

Los comerciantes deben actualizar la versión de la extensión [!DNL Live Search] >= 3.0.1 para tener acceso a estas características.

Se recomienda actualizar y probar antes de pasar a producción. Considere la posibilidad de actualizar el entorno de producción durante las horas de menor actividad después de verificar los resultados de su entorno de prueba.

### [!DNL Live Search] 2.0.5

[!BADGE Compatible]{type="Informativo" tooltip="Admitido"}

![Corrección](../assets/fix.svg): Live Search generaría un error cuando los recursos de SDK no estuvieran disponibles debido a problemas de red. Este error se ha corregido.

Los comerciantes deben actualizar la versión de la extensión de Live Search >= 2.0.5 para acceder a estas funciones.

Se recomienda actualizar y probar antes de pasar a producción. Considere la posibilidad de actualizar el entorno de producción durante las horas de menor actividad después de verificar los resultados de su entorno de prueba.

### [!DNL Live Search] 2.0.4

[!BADGE Compatible]{type="Informativo" tooltip="Admitido"}

![Nuevo](../assets/new.svg) Live Search ahora admite el filtrado por la configuración &quot;Mostrar productos sin existencias&quot; del administrador. Si &quot;Mostrar productos sin existencias&quot; se establece en &quot;falso&quot;, se agrega `inStock = true` al filtro.
![Corrección](../assets/fix.svg) Para mejorar el rendimiento, el bloque &quot;Sugerencias&quot; se ha eliminado de la ventana emergente de Live Search. Los datos se siguen pasando a través de GraphQL, en caso de que desee reemplazar la función.
![Corrección](../assets/fix.svg) `categories` y `categoryPath` han reemplazado a `categoryIds` para el filtrado de categorías. Obtenga más información en el tema [productSearch](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/).
![Corrección](../assets/fix.svg) Anteriormente, un usuario vinculado a una compañía B2B recibía un código de grupo de clientes incorrecto al realizar búsquedas. Live Search ahora devuelve el valor correcto.
![Corregir](../assets/fix.svg) Anteriormente, al buscar un término que no existe, Live Search devolvía un error. Ese error ya está solucionado.

Los comerciantes deben actualizar la versión de la extensión [!DNL Live Search] >= 2.0.4 para tener acceso a estas características.

Se recomienda a los usuarios actualizar y probar antes de pasar a producción. Considere la posibilidad de actualizar el entorno de producción durante las horas de menor actividad después de verificar los resultados de su entorno de prueba.

### [!DNL Live Search] 2.0.3

[!BADGE Compatible]{type="Informativo" tooltip="Admitido"}

![Nuevo](../assets/new.svg) Live Search ahora admite características B2B al respetar los permisos de categoría, los catálogos compartidos y los precios específicos de grupos de clientes.

Los comerciantes deben actualizar la versión de la extensión [!DNL Live Search] >= 2.0.3 para tener acceso a estas características.

Se recomienda a los usuarios actualizar y probar antes de pasar a producción. Considere la posibilidad de actualizar el entorno de producción durante las horas de menor actividad después de verificar los resultados de su entorno de prueba.

### [!DNL Live Search] 2.0

[!BADGE Compatible]{type="Informativo" tooltip="Admitido"}

Las instalaciones existentes de [!DNL Live Search] deben actualizarse a [!DNL Live Search] 2.0.0 para aprovechar las siguientes nuevas características, correcciones y mejoras:

![Nuevo](../assets/new.svg) [!DNL Live Search] ahora es compatible con PHP 8.1 para instalaciones que ejecutan Adobe Commerce 2.4.4.
![Nuevo](../assets/new.svg) El módulo `Magento_ElasticsearchCatalogPermissionsGraphQl` se agrega a la lista de módulos deshabilitados durante la instalación.
![Nuevo](../assets/new.svg) El número de líneas disponibles en [[!DNL storefront popover]](overview.md) se puede configurar desde *Admin*.
![Nuevo](../assets/new.svg) Beta [PWA](https://developer.adobe.com/commerce/pwa-studio/) compatible con [!DNL Live Search].
![Nuevo](../assets/new.svg) El proceso de instalación de [!DNL Live Search] se ha actualizado con cambios avanzados en el proceso.
![Corrección](../assets/fix.svg) Se ha eliminado el vínculo [Búsqueda avanzada](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) del pie de página de la tienda.
![Error](../assets/bug.svg): [Commerce GraphQL API](https://developer.adobe.com/commerce/services/graphql/live-search/) no admite los siguientes atributos de producto cuando se usan en relación con la versión beta de PWA: `description`, `name`, `short_description`
![Error](../assets/bug.svg) La versión beta de PWA para [!DNL Live Search] no admite [la administración de eventos](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/).

### [!DNL Live Search] 1.3.1

[!BADGE Compatible]{type="Informativo" tooltip="Admitido"}

![Corrección](../assets/fix.svg) [El atributo de precio personalizado](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types) ya no devuelve un error cuando se configura como una [faceta](facets-add.md).
![Corregir](../assets/fix.svg) Se ha corregido un problema que provocaba que se produjera un error cuando no estaba disponible ningún [símbolo de moneda](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration#step-5-customize-currency-symbols-optional) (`data-currency-symbol`).
![Corrección](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md) ahora muestra el [Precio especial](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-special) (precio mínimo final) cuando está disponible.

### [!DNL Live Search] 1.3.0

[!BADGE Compatible]{type="Informativo" tooltip="Admitido"}

El tablero de informes ![Nuevo](../assets/new.svg) [Rendimiento](performance.md) proporciona información sobre los términos de búsqueda que usan los compradores.
![Nuevo](../assets/new.svg) [!DNL Live Search] [Eventos de tienda SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/) proporciona acceso a una capa de datos común con servicios de publicación de eventos y suscripción, y métricas.
![Corrección](../assets/fix.svg): [[!DNL Storefront popover]](storefront-popover.md) tiene una nueva clase `active` para el contenedor `.search-autocomplete` que controla la visibilidad.
![Corregir](../assets/fix.svg) En la tienda, se quita el vínculo de pie de página de [Términos de búsqueda](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-terms) y se deshabilita su caché para [!DNL Live Search] instalaciones.
![Error](../assets/bug.svg) de revisión para el adaptador de búsqueda administra los productos duplicados.
![Error](../assets/bug.svg) [!DNL Live Search] admite [ubicaciones de inventario de origen único](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/sources/sources-manage) (físico) con múltiples [existencias](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/stocks/stocks-manage) (virtuales). Ahora no se admiten varios orígenes de inventario.

### [!DNL Live Search] 1.2.0

[!BADGE Compatible]{type="Informativo" tooltip="Admitido"}

![Nuevo](../assets/new.svg) [[!DNL Storefront popover]](storefront-popover.md) muestra productos sugeridos e imágenes en miniatura de los principales resultados de búsqueda mientras los compradores escriben consultas en el cuadro de búsqueda.
La sesión ![Nueva](../assets/new.svg) de *Administrador* de Commerce permanece abierta durante largos períodos de inactividad del teclado
![Nuevo](../assets/new.svg) [!DNL Live Search] se habilita automáticamente después de la incorporación
![Corrección](../assets/fix.svg) El tiempo de indexación inicial es inferior a una hora
![Corregir](../assets/fix.svg) actualizaciones incrementales de productos casi en tiempo real (después de la instalación y configuración)
![Corregir](../assets/fix.svg) columnas que se pueden ordenar en el editor de sinónimos
![Corregir](../assets/fix.svg) [!DNL Live Search] ya no genera un error si los criterios de búsqueda contienen un valor de criterio de ordenación vacío
![Corrección](../assets/fix.svg) El filtrado de intervalos ya no se interrumpe si los códigos de atributo contienen cadenas &quot;to&quot; o &quot;from&quot;

### [!DNL Live Search] 1.1.0

[!BADGE Compatible]{type="Informativo" tooltip="Admitido"}

![Error](../assets/bug.svg) El servicio [!DNL Live Search] solo admite la [divisa base](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration) de la instalación de Adobe Commerce.
![Error](../assets/bug.svg) Al agregar una faceta, la Fuente de atributos del producto no se actualiza correctamente cuando se establece en `Update on Save`. Para evitar este problema, vaya a [Administración de índices](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) y establezca la Fuente de atributos de productos en `Update by Schedule`.
Los sinónimos de ![Bug](../assets/bug.svg) [!DNL Live Search] se definen por vista de tienda, pero actualmente se almacenan por sitio web y se identifican con una combinación de `environmentId` y `storeViewCode`. Como resultado, todos los sitios web y las vistas de tienda dentro de la instalación de Adobe Commerce comparten sinónimos. El conjunto de sinónimos creado más recientemente para la vista de tienda tiene prioridad.
![Error](../assets/bug.svg) Si un término sinónimo contiene varias palabras, cada palabra se trata como un sinónimo independiente. Por ejemplo, si define &quot;reloj&quot; como sinónimo de &quot;reloj&quot;, tanto &quot;tiempo&quot; como &quot;pieza&quot; se tratan como sinónimos de reloj.

+++

## Documentación

Para obtener más información:

- [Documentación para desarrolladores de Adobe Commerce](https://developer.adobe.com/commerce/docs)
- [Guía del usuario de Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce)
- [[!DNL Live Search] en Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html)
