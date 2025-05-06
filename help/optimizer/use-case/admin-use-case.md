---
title: Caso de uso de Carvelo
description: Aprenda a usar [!DNL Adobe Commerce Optimizer] para administrar su catálogo mediante canales y directivas, y a configurar su tienda en función de la configuración de su catálogo.
hide: true
role: Admin, Developer
feature: Personalization, Integration
exl-id: d11663f8-607e-4f1d-b68f-466a69bcbd91
source-git-commit: 149b87fc822e5d07eed36f3d6a38c80e7b493214
workflow-type: tm+mt
source-wordcount: '1672'
ht-degree: 0%

---

# Caso de uso de Carvelo

>[!NOTE]
>
>Esta documentación describe un producto en desarrollo de acceso anticipado y no refleja todas las funcionalidades pensadas para una disponibilidad general.

En el siguiente caso de uso se muestra cómo se puede utilizar [!DNL Adobe Commerce Optimizer] para organizar el catálogo de modo que coincida con las operaciones comerciales mediante un único catálogo base. También muestra cómo configurar una tienda con tecnología de Edge Delivery Services.

## Requisito previo

Antes de pasar por este caso de uso, asegúrate de que has [configurado tu tienda](../storefront.md).

## Vamos a empezar.

En este caso de uso, trabajará con lo siguiente:

1. IU [!DNL Adobe Commerce Optimizer]: configure los canales y las directivas necesarios para administrar la configuración operativa compleja del catálogo.

1. Tienda Commerce: procese la tienda con los datos del catálogo configurados en la interfaz de usuario de [!DNL Adobe Commerce Optimizer] y los archivos de configuración de Tienda Commerce, `fstab.yaml` y `config.json`.

### ‌Lecciones clave

Al final de este artículo, deberá hacer lo siguiente:

- Conozca los aspectos básicos de [!DNL Adobe Commerce Optimizer] con su modelo de datos de catálogo escalable y de rendimiento único.
- Descubra cómo el modelo de datos de catálogo se vincula sin problemas con los componentes de tienda independientes de la plataforma creados por Adobe.
- Aprenda a utilizar los canales y las directivas de Adobe Commerce Optimizer para crear vistas de catálogo personalizadas y filtros de acceso a datos, y a enviar los datos a una tienda de Adobe Commerce con tecnología de Edge Delivery.

## Escenario de negocio - Carvelo Automobile

Carvelo Automobile es un conglomerado automovilístico ficticio con una configuración operativa compleja.

![Carvelo Automobile](../assets/carvelo.png)

En este diagrama, ven que Carvelo vende productos de automóviles de tres marcas. Cada marca es una compañía secundaria diferente:

- Aurora (vehículos eléctricos)
- Tornillo (SUV)
- Cruz (híbrido)

Vende estas marcas a través de tres distribuidores:

- Arkbridge
- Kingsbluff
- Celport

Estos concesionarios pertenecen a dos empresas matrices de concesionarios diferentes:

- West Coast Inc. (Arkbridge)
- East Coast Inc. (Kingsbluff, Celport)

Cada compañía tiene dos libros de precios que se utilizan para vender productos a un precio específico para diferentes compradores (base, VIP).

- `west_coast_inc` y `vip_west_coast_inc`
- `east_coast_inc` y `vip_east_coast_inc`

Como puede ver, este es un caso de uso empresarial muy complejo. Con [!DNL Adobe Commerce Optimizer], un comerciante puede admitir una estructura empresarial compleja mediante un único catálogo base para distribuir los datos sin duplicación de catálogos, escalar los libros de precios (más de 30 000 libros de precios) y enviar todos estos datos a una tienda de Edge Delivery Services.

Ahora que tiene una visión general del caso práctico empresarial, este es su objetivo a medida que trabaja en este tutorial:

>[!BEGINSHADEBOX]

Carvelo quiere vender piezas en sus tres marcas (Aurora, Bolt y Cruz) a través de los diferentes concesionarios (Akbridge, Kingsbluff y Celport). Carvelo quiere asegurarse de que los concesionarios solo tengan acceso a las piezas y precios correctos según sus respectivos acuerdos de licencia.

En última instancia, Carvelo tiene dos objetivos principales:

1. Mantenga un sitio web &quot;global&quot; que tenga todos los SKU de las tres marcas.
1. Proporcione una ruta para que los concesionarios configuren sus propias tiendas en función de la visibilidad del SKU único y los precios de cada SKU para cada concesionario. Todo mientras se utiliza un único catálogo base, lo que elimina la duplicación de catálogos.

>[!ENDSHADEBOX]

Ahora, obtenga acceso a su instancia de [!DNL Adobe Commerce Optimizer].

## 1. Acceder a la instancia [!DNL Adobe Commerce Optimizer]

Después de incorporarse al programa Acceso anticipado, Adobe envía un mensaje de correo electrónico que proporciona la dirección URL para acceder a la instancia de l[!DNL Adobe Commerce Optimizer] aprovisionada para usted. Esta instancia está preconfigurada con todo lo que necesita para completar correctamente los pasos descritos en este tutorial, incluidos los datos de catálogo que admiten el caso de uso de Carvelo Automobile.

Cuando inicie [!DNL Adobe Commerce Optimizer], verá lo siguiente:

IU ![[!DNL Adobe Commerce Optimizer]](../assets/user-interface.png)

>[!NOTE]
>
>Consulte el artículo de [descripción general](../overview.md) para obtener más información sobre las diferentes partes que conforman la interfaz de usuario de [!DNL Adobe Commerce Optimizer].

En el panel de navegación izquierdo, expanda la sección **[!UICONTROL Catalog]** y haga clic en **[!UICONTROL Channels]**. Observe que los concesionarios Arkbridge y Kingsbluff ya tienen canales creados:

![Canales preconfigurados](../assets/existing-channels-list.png)

>[!NOTE]
>
>Por ahora, puedes ignorar el canal **Global**.

Haga clic en el icono de información para revisar los detalles del canal.

Arkbridge tiene las siguientes políticas:

- Marca
- Modelo
- Marcas West Coast Inc
- Categorías de piezas de Arkbridge

Kingsbluff tiene las siguientes políticas:

- Marca
- Modelo
- Marcas East Coast Inc
- Categorías de partes de Kingsbluff

En la siguiente sección, creará un canal y políticas para el concesionario Celport.

## 2. Crear una directiva y un canal

El gerente comercial de Carvelo necesita configurar una nueva tienda para un distribuidor llamado *Celport* que pertenece a la compañía *East Coast Inc*. Celport venderá frenos y suspensiones para las marcas Bolt y Cruz.

![Concesionario Celport](../assets/celport-dealer.png)

Con [!DNL Adobe Commerce Optimizer], el administrador de comercio:

1. Cree una nueva póliza llamada *Celport part categories* para que Celport venda solamente piezas de frenos y suspensión.
1. Cree un nuevo canal para la tienda de Celport.

   Este canal usa las *categorías de piezas de Celport* de la directiva recién creada y las marcas *East Coast Inc* para garantizar que Celport pueda vender solamente las marcas Bolt y Cruz como parte del acuerdo con East Coast Inc. El canal de Celport usará el catálogo de precios de `east_coast_inc` para admitir las programaciones de precios de productos que se alineen con los acuerdos de licencia de marca.
1. Actualice la configuración de la tienda de comercio para utilizar los datos del canal de Celport que ha creado.

Al final de esta sección, Celport estará lista para vender los productos de Carvelo.

### Crear una directiva

Vamos a crear una nueva directiva llamada *categorías de piezas Celport* para filtrar las SKU que vende el concesionario Celport, que incluyen piezas de frenos y suspensión.

1. En el panel de navegación izquierdo, expanda la sección **[!UICONTROL Catalog]** y haga clic en **[!UICONTROL Policies]**.

1. Haga clic en **[!UICONTROL Add Policy]**.

   Aparece una nueva página para agregar los detalles de la directiva.

1. Añada los detalles necesarios:

   **Nombre** = *Categorías de piezas de Celport*

1. Haga clic en **[!UICONTROL Add Filter]**.

   Se muestra un cuadro de diálogo para añadir detalles del filtro.

1. Añada los detalles del filtro:

   - **Atributo** = *part_category*
   - **Operador** = **IN**
   - **Valor Source** = **ESTÁTICO**
   - **Valor** = *frenos*, *suspensión*

   >[!IMPORTANT]
   >
   >Asegúrese de que el nombre de atributo que especifique coincida exactamente con el nombre de atributo SKU del catálogo.

   Para obtener más información acerca de la diferencia entre un origen de valor ESTÁTICO y de DÉCLENCHEUR, vea [tipos de origen de valor](../catalog/policies.md#value-source-types).

1. En el diálogo **[!UICONTROL Filter details]**, haga clic en **[!UICONTROL Save]**.

1. Para habilitar el filtro que acaba de crear, haga clic en los puntos de acción (...) y seleccione **Habilitar**.

1. Haga clic en **[!UICONTROL Save]**.

   >[!NOTE]
   >
   >Si el botón **[!UICONTROL Save]** no está activo (azul), es posible que falte el nombre de la directiva. Haga clic en el icono de lápiz junto a *Nueva directiva* para agregarla.

1. Vuelva a la lista de directivas haciendo clic en la flecha hacia atrás.

   Su nueva directiva *Celport* categorías de partes aparece en la lista.

### Crear un canal

Cree un nuevo canal para el concesionario *Celport* y vincule las siguientes políticas: *marcas East Coast Inc* y *categorías de piezas Celport*.

1. En el panel de navegación izquierdo, expanda la sección **[!UICONTROL Catalog]** y haga clic en **[!UICONTROL Channels]**.

   ![Canales](../assets/channels.png)

   Observe los canales existentes: *Arkbridge*, *Kingsbluff* y *Global*.

   ![Página de canales existentes](../assets/existing-channels-list.png)

1. Haga clic en **[!UICONTROL Add Channel]**.

1. Rellene los detalles del canal:

   - **Nombre** = *Celport*
   - **Ámbitos** = *en-US* (entrar)
   - **Políticas** (usar lista desplegable) = *Marcas de East Coast Inc*; *Categorías de partes de Celport*; *Marca*; *Modelo*                          

1. Haga clic en **[!UICONTROL Add]** para crear el canal.

   La página Canales se actualiza para mostrar el nuevo canal.

   ![Lista de canales actualizada](../assets/updated-channels-list.png)

   >[!NOTE]
   >
   >Si el botón **[!UICONTROL Add]** no está en azul, asegúrese de que el ámbito esté seleccionado colocando el cursor en la sección **[!UICONTROL Scopes]** y presionando **intro**.

1. Obtenga el ID de canal de Celport.

   Haga clic en el icono de información del canal Celport en la página **Canales**.

   ![ID de canal de Celport](../assets/celport-channel-id.png)

   Copie y guarde el ID de canal. Necesita este ID cuando actualice la configuración de la tienda para enviar datos al nuevo catálogo de Celport.

Después de crear el canal de Celport y las políticas asociadas, el siguiente paso es configurar la tienda para crear el nuevo catálogo de Celport.

## 3. Actualiza tu tienda

La parte final de este tutorial implica actualizar la tienda que [ya has creado](#prerequisite) para enviar datos al nuevo catálogo de Celport. En esta sección, reemplace el ID de canal del archivo de configuración de la tienda por el ID de canal de Celport.

1. En su entorno de desarrollo local, abra la carpeta donde clonó el repositorio de GitHub con los archivos de configuración de las plantillas de tienda.

1. En el directorio raíz de la carpeta, abra el archivo `config.json`.

   código +++config.json

   ```json
   {
    "public": {
      "default": {
      "commerce-core-endpoint": "https://www.aemshop.net/graphql",
      "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/Fwus6kdpvYCmeEdcCX7PZg/graphql",
      "headers": {
         "cs": {
            "ac-channel-id": "9ced53d7-35a6-40c5-830e-8288c00985ad",
            "ac-environment-id": "Fwus6kdpvYCmeEdcCX7PZg",
            "ac-price-book-id": "west_coast_inc",
            "ac-scope-locale": "en-US"
           }
         },
         "analytics": {
            "base-currency-code": "USD",
            "environment": "Production",
            "store-id": 1,
            "store-name": "ACO Demo",
            "store-url": "https://www.aemshop.net",
            "store-view-id": 1,
            "store-view-name": "Default Store View",
            "website-id": 1,
            "website-name": "Main Website"
          }
       }
      }
   }
   ```

   Tenga en cuenta que el encabezado del canal contiene las siguientes líneas:

   - `ac-channel-id`:`"9ced53d7-35a6-40c5-830e-8288c00985ad"`
   - `ac-environment-id`: `"Fwus6kdpvYCmeEdcCX7PZg"`
   - `ac-price-book-id`: `"west_coast_inc"`

+++

1. Reemplace el valor `ac-channel-id` por el ID de canal de Celport que copió anteriormente.
1. Reemplace el valor `ac-environment-id` por el identificador de inquilino de su instancia [!DNL Adobe Commerce Optimizer]. Puede encontrar el ID en el correo electrónico de incorporación para el programa de acceso anticipado o poniéndose en contacto con el representante de la cuenta de Adobe.

   >[!IMPORTANT]
   >
   >Asegúrese de que el valor `commerce-endpoint` coincida con el extremo de GraphQL para la instancia [!DNL Adobe Commerce Optimizer]. Esto se proporciona en el correo electrónico de bienvenida.

1. Reemplazar el valor `ac-price-book-id` por `"east_coast_inc"`.
1. Guarde el archivo.

Cuando guarde los cambios, actualice la configuración del catálogo para utilizar el canal Carvelo, que se ha configurado para vender únicamente piezas de freno y suspensión.

1. Inicia la tienda para ver la experiencia de catálogo específica de Celport creada por la configuración de tu tienda.

   1. Desde la ventana de terminal del IDE, inicie la previsualización de la tienda local.

      ```shell
      npm start
      ```

   El explorador se abre en la vista previa de desarrollo local en `http://localhost:3000`.

   Si el comando falla o el explorador no se abre, revise las [instrucciones para el desarrollo local](../storefront.md) en el tema de configuración de Storefront.

   1. En el explorador, busque `brakes` y presione **Entrar**.

      La tienda se actualiza para mostrar la página de la lista de productos con las piezas de freno.

   ![Página de lista de productos de frenos](../assets/brakes-listing-page.png)

   Haga clic en una imagen de la pieza de freno para ver los detalles del producto con información sobre el precio y anote la información sobre el precio del producto.

1. Ahora busque `tires`, que es otra categoría de artículo disponible en los datos del caso de uso de la instancia [!DNL Adobe Commerce Optimizer].

   ![Configuración de tienda con encabezados incorrectos](../assets/storefront-configuration-with-incorrect-headers.png)

   Observe que no se devuelve ningún resultado. Esto se debe a que el canal Celport ha sido configurado para vender únicamente piezas de freno y suspensión.

1. Experimente con la actualización del archivo de configuración de la tienda (`config.json`).

   1. Cambie los valores `ac-channel-id` y `ac-price-book`.

      Por ejemplo, puede cambiar el ID de canal al canal de Kingsbluff y el ID del libro de precios a `east_coast_inc`. Puedes ver las categorías de piezas disponibles para Kingsbluff revisando la *política de categorías de piezas de Kingsbluff*.

   1. Guarde el archivo.

      Al guardar el archivo, la vista previa de la tienda local se actualiza automáticamente.

   1. Obtenga una vista previa de los cambios en el navegador mediante la función de búsqueda para encontrar las piezas de neumáticos.

      Observe los diferentes tipos de piezas disponibles y los precios asignados al canal Kingsbluff.

      Al cambiar los valores de los encabezados en el archivo de configuración de la tienda y explorar la tienda actualizada, puedes ver lo fácil que es actualizar la vista del catálogo y los filtros de datos para personalizar la experiencia de la tienda.

## ¡Eso es todo!

En este tutorial, ha aprendido cómo [!DNL Adobe Commerce Optimizer] puede ayudarle a organizar su catálogo para que coincida con sus operaciones de venta minorista mediante un único catálogo base. También aprendió a configurar una tienda con tecnología de Edge Delivery Services.

## A dónde ir desde aquí

Para obtener información sobre cómo usar Descubrimiento de productos y Recommendations con el fin de personalizar la experiencia de compra para sus clientes, consulte la [descripción general de la comercialización](../merchandising/overview.md).
