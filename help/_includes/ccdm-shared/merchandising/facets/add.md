---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%
---
Cualquier atributo de producto filtrable puede utilizarse como faceta. Las facetas ayudan a los clientes a filtrar y encontrar productos más fácilmente en su tienda. Este artículo explica cómo agregar, administrar y configurar facetas en la tienda.

![Crear una faceta](/help/assets/ccdm-shared/facets/create-facet.png)

## Creación de una faceta

1. En el menú, selecciona _Comercialización_ > **Facetas** y luego haz clic en **Crear facetas**.
1. En la lista *Crear facetas*, cada atributo disponible tiene un ![botón Agregar](/help/assets/ccdm-shared/facets/btn-add.png) independiente. Complete cualquiera de las siguientes opciones:

   - En la lista *Atributos de facetas*, elija el atributo de producto que desee usar como faceta y haga clic en **Agregar**.
   - Para buscar un atributo de producto específico, escriba los primeros caracteres del nombre del atributo en el cuadro *Buscar*. A continuación, haga clic en **Agregar**.

   La faceta se agrega al final de la lista *Facetas dinámicas* y el botón *Publicar cambios* pasa a estar disponible.

1. Si la faceta que desea agregar no se encuentra, use la [API de metadatos](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata){target="_blank"} para establecer el parámetro `filterable`:

   `"filterable": true`

   La faceta estará disponible en la tienda la próxima vez que el catálogo se sincronice con la capa de datos de Servicios de comercialización. Si la faceta no está disponible después de dos horas, consulte [sincronización de datos](../../setup/data-sync.md).

## Editar propiedades de faceta (opcional)

1. Busque la faceta que desee editar.
1. Haga clic en el selector más (![Más](/help/assets/ccdm-shared/recommendations/btn-more.png)).
1. En el menú, haga clic en **Editar**. A continuación, ajuste las siguientes propiedades según sea necesario:

   - Etiqueta (Label): introduzca la etiqueta de faceta que desee utilizar.
   - Tipo de orden: elija una de las siguientes opciones:
     - Alfabético: Ordena las facetas alfabéticamente
     - Recuento: ordena las facetas según el número de coincidencias encontradas
   - Valor máximo (Max Value): permite introducir el número máximo de valores de faceta mostrados en la tienda. Entradas válidas: 0 - 100; Predeterminado: 8.

1. Una vez finalizado, haga clic en **Guardar**.

## Fijar/desanclar facetas

El fijador cambia de color cuando se hace clic y se usa para mover la faceta a la sección *Facetas fijadas* o *Facetas dinámicas*.

1. Para anclar una faceta a la parte superior de la lista *Filtros*, busque la faceta en la lista *Facetas dinámicas* y haga clic en la chincheta gris (![Selector de chincheta](/help/assets/ccdm-shared/facets/btn-pin-gray.png)).

   El pin se volverá azul y la faceta se moverá a la sección *Facetas ancladas*.

1. Para desanclar una faceta, búsquela en la lista *Facetas ancladas* y haga clic en el pin azul (![Selector de anclaje](/help/assets/ccdm-shared/facets/btn-pin-blue.png)).

   La chincheta se volverá gris y la faceta pasará a la sección *Facetas dinámicas*.

>[!NOTE]
>
>El orden de facetas anclado puede ser incoherente si hay dos etiquetas con el mismo nombre.

## Eliminar facetas

1. Busque la faceta en la lista y haga clic en el selector más (![Más](/help/assets/ccdm-shared/recommendations/btn-more.png)).
1. Haga clic en **Eliminar**.
1. Cuando se le pida que confirme, haga clic en **Eliminar faceta**.
La faceta se eliminará de la tienda una vez publicados los cambios.

## Publicar cambios

1. Para actualizar la tienda con los cambios, haz clic en **[!UICONTROL Publish]**.
1. Espera unos 15 minutos para que las actualizaciones aparezcan en tu tienda.

## Más información

- Para configurar los intervalos y agrupaciones de facetas de precios, consulte [Configuración](../../settings.md).
- Obtenga más información sobre los [tipos](type.md) de facetas.
