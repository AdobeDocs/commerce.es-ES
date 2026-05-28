---
title: Configuración de AEM Assets para Commerce Optimizer
description: Obtenga información sobre cómo configurar la integración de AEM Assets para  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
source-git-commit: 42f0e0cb72c6429eb6f08f1922c4171195a78d2b
workflow-type: tm+mt
source-wordcount: '1460'
ht-degree: 0%

---


# Configurar AEM Assets para [!DNL Adobe Commerce Optimizer]

[!BADGE Solo SaaS]{type=Positive tooltip="Solo se aplica a los proyectos de Adobe Commerce Optimizer."}

La integración de AEM Assets para [!DNL Adobe Commerce Optimizer] permite que los comerciantes utilicen AEM Assets como solución de administración centralizada de recursos digitales para las imágenes de los productos. Esta guía describe la configuración específica de [!DNL Commerce Optimizer].

A diferencia de Adobe Commerce (PaaS) o Adobe Commerce as a Cloud Service (ACCS), [!DNL Commerce Optimizer] no tiene una interfaz de usuario de configuración de administración. Para habilitar la integración, cree un vale de soporte con los detalles de [!DNL Adobe Commerce Optimizer] y los AEM Assets. El Soporte de Adobe configura la integración y registra su inquilino con el Servicio de integración de Assets.

**Prepare a los AEM Assets antes de enviar el ticket.** El registro de inquilinos supone que el lado de AEM se puede utilizar para Commerce. Por ejemplo, después de implementar el paquete de AEM Commerce `assets-commerce`, los metadatos y los eventos funcionarán según se explica. **Abrir un ticket antes de que se configure AEM puede retrasar la incorporación.**

El diagrama siguiente es una descripción general de la sincronización de productos entre [!DNL Adobe Commerce Optimizer] y la integración de AEM Assets.

![AEM Assets a [!DNL Commerce Optimizer] flujo](../assets/aco-asset-sync-architecture.png){width="700"}

Esta integración tiene dos flujos principales:

* **De AEM Assets**: cuando se aprueba, rechaza o elimina un recurso, el evento fluye a través de la canalización de Adobe al servicio de integración de Assets. El servicio hace coincidir recursos con productos que usan `match-by-SKU` (controlado por metadatos) o un [elemento de coincidencia personalizado (App Builder)](../synchronize/custom-match.md){target=_blank}, y envía las asignaciones de `product-asset` a Commerce Optimizer, donde se almacenan como capas de producto.

* **Desde[!DNL Adobe Commerce Optimizer]**: cuando se actualiza un producto en [!DNL Commerce Optimizer], el evento fluye a través de la canalización de Adobe hasta el servicio de integración de Assets. El servicio sincroniza todas las asignaciones de recursos coincidentes con [!DNL Adobe Commerce Optimizer].

## Requisitos previos

Antes de configurar la integración, asegúrese de lo siguiente:

* Una instancia de [!DNL Adobe Commerce Optimizer] activa con derechos de visualización del producto o cualquier licencia de AEM Assets con Dynamic Media.
* Acceso a un entorno de as a Cloud Service de AEM Assets.
* Tanto [!DNL Commerce Optimizer] como AEM Assets en la misma organización de Adobe IMS.
* Dynamic Media con OpenAPI habilitado en su entorno de AEM Assets (consulte [Configuración del proyecto de AEM Assets](configure-aem.md#prerequisites) para ver los pasos de habilitación).

## Configuración de AEM Assets primero

Complete los pasos de los AEM Assets **antes de** que [abra un ticket de asistencia](#onboarding) para el registro de inquilinos. El patrón de instalación coincide con Adobe Commerce as a Cloud Service (consulte [Configuración del proyecto de AEM Assets para que admita metadatos de Commerce](configure-aem.md).

### Paso 1: Implementar el paquete de AEM Commerce

Instale e implemente el paquete `assets-commerce` en su proyecto de AEM para que los esquemas de metadatos, los eventos y la interfaz de usuario de Commerce estén disponibles.

Complete el procedimiento completo en [Instalar el paquete `assets-commerce`](configure-aem.md#step-1-install-the-assets-commerce-package). Antes de abrir un ticket de asistencia, siga estos pasos:

1. Clone el repositorio Git de Cloud Manager y copie el código del [repositorio Commerce de AEM Assets](https://github.com/ankumalh/assets-commerce) en su proyecto.

1. En todos los archivos de `filter.xml` y `pom.xml` del proyecto, reemplace todas las apariciones de &lt;my-app> por el nombre de su aplicación.

1. Confirme, inserte, ejecute la canalización de implementación y valide que la pestaña **[!UICONTROL Commerce]** aparece en las propiedades del recurso.

Vea [Instalar el paquete `assets-commerce`](configure-aem.md#step-1-install-the-assets-commerce-package) para obtener capturas de pantalla de Cloud Manager, pasos de canalización y solución de problemas si falta la ficha **[!UICONTROL Commerce]**.

### Paso 2: Habilitar Dynamic Media con OpenAPI

Dynamic Media con capacidades OpenAPI debe estar habilitado en el entorno de los AEM Assets. Las rutas de autoservicio (por ejemplo, Cloud Manager para imágenes de productos) y las rutas de soporte de Adobe se describen en [Configuración del proyecto de AEM Assets](configure-aem.md#prerequisites).

### Paso 3: Aplicar metadatos de Commerce y aprobar recursos

Agregue metadatos de Commerce a sus imágenes de producto en AEM Assets; para ver las definiciones de los campos, consulte [Contenido del paquete de AEM Commerce](configure-aem.md#aem-commerce-assets-commerce-package-contents).

El recurso debe estar en estado **aprobado** para la sincronización de datos con el déclencheur. Guardar metadatos por sí solo no almacena el evento en déclencheur.

### Paso 4: Opcional: Configuración de un perfil de metadatos de Commerce

Si decide usar perfiles de metadatos de AEM para agilizar la creación, configúrelos **después de** de que se implemente el paquete y su equipo comprenda los campos de Commerce necesarios (el mismo patrón opcional que **Configuración del proyecto de AEM Assets**).

Consulte [Configurar un perfil de metadatos](configure-aem.md#step-2-optional-configure-a-metadata-profile).

## Limitaciones

La integración de [!DNL Commerce Optimizer] tiene las siguientes limitaciones:

### Restricciones relacionadas con la capa

Lea esta sección **antes de** para elegir un nombre de capa de catálogo en su vale de soporte. Elegir o compartir capas sin este contexto es una causa frecuente de casos de soporte evitables.

**Use una capa específica para el contenido de los AEM Assets.** Las cargas enviadas desde los AEM Assets rellenan un catálogo de Commerce Optimizer **layer**. Los valores de esa capa **sobrescriben** atributos de catálogo base donde se proporcionan los campos. Cuando la integración omite un campo en la carga útil, los valores correspondientes de esa capa pueden sobrescribirse con valores vacíos. Compartir una capa con flujos de trabajo de Commerce no relacionados (o reutilizar una capa que ya almacena datos de productos que no son de AEM o Assets) puede causar **pérdida involuntaria de datos** o sobrescrituras confusas. Planifique la opción de capa **antes de** de abrir su ticket de soporte y reserve ese nombre de capa (por ejemplo, la capa predeterminada **`AEM-Assets`**) principalmente para la sincronización de imágenes de producto impulsada por AEM.

>[!IMPORTANT]
>
>La integración admite **un origen de catálogo por inquilino**: una sola configuración regional y **un nivel con nombre**. En este momento no se admite la configuración de varias capas AEM-Assets o varias configuraciones regionales para el mismo inquilino.

### Otras restricciones

* **Solo imágenes**: la integración no admite vídeo u otros tipos de medios en este momento.
* **No hay imágenes de categoría**: la sincronización de imágenes de categoría no está disponible. No se admiten imágenes de categoría de AEM Assets para el Selector de Assets (inserción en la IU).
* **Sin distinción de varios sitios**: la integración no administra varios sitios; se muestra una imagen asociada a un producto de la misma manera en todos los canales y directivas.
* **Posición/orden de la imagen**: no se admiten la posición y el orden de la imagen.
* **El producto debe existir**: Si el producto no existe en [!DNL Commerce Optimizer], la capa no se crea para esa asignación de productos a recursos.

## Incorporación

Para integrar la integración de AEM Assets con [!DNL Commerce Optimizer], debe [Crear un vale de soporte](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket).

El Soporte de Adobe utiliza la información de su ticket para registrar su inquilino con el Servicio de integración de Assets y configurar la integración.

Asegúrese de haber [configurado AEM Assets primero](#configure-aem-assets-first) antes de enviar el ticket.

Incluya la siguiente información en su vale de soporte:

* **[!DNL Adobe Commerce Optimizer]ID de inquilino** (ID de instancia) encontrado en su URL [!DNL Commerce Optimizer] o IU de Commerce Cloud Manager.
* **ID de programa de AEM**.
* **ID. de entorno de AEM**.
* **Regla de coincidencia**: Coincidencia por SKU o [coincidencia externa (App Builder)](../synchronize/custom-match.md){target=_blank}.
* **Capa**: El nombre de la capa de catálogo con la que registrar al inquilino (consulte **Restricciones relacionadas con la capa**). Especifique un nombre personalizado solo si es intencional; de lo contrario, se usa el valor predeterminado **`AEM-Assets`**.
* **Configuración regional**: La configuración regional de origen del catálogo con la que registrar al inquilino (por ejemplo, `en-US`). Debe coincidir con la configuración regional que utilice en la vista de catálogo y en los datos del catálogo de productos.

Una vez que el Soporte de Adobe procesa el ticket, la integración se configura y el inquilino se registra con el Servicio de integración de Assets.

Una vez completada la incorporación:

1. **Registro con el servicio de integración de Assets**: el inquilino de [!DNL Commerce Optimizer] está registrado con el servicio de integración de Assets usando su identificador de inquilino de [!DNL Adobe Commerce Optimizer], identificador de programa de AEM, identificador de entorno de AEM, regla de coincidencia, configuración regional y nombre de capa proporcionados en el ticket.

1. **Suscripción de evento**: Assets Integration Service se suscribe a:

   * Eventos de AEM Assets (recursos aprobados, actualizados y eliminados)
   * [!DNL Commerce Optimizer] eventos de catálogo (producto creado, actualizado)

Configure la [vista de catálogo](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-view) para que las API y la tienda muestren datos de imagen generados por AEM:

* **Origen del catálogo (configuración regional)**: seleccione la misma configuración regional especificada en su vale de soporte técnico (por ejemplo, **`en-US`**). La integración registra una configuración regional por inquilino; una discrepancia impide que las imágenes sincronizadas aparezcan en la vista de catálogo deseada.
* **Capa de catálogo** — Asigne la capa **`AEM-Assets`** (o su nombre de capa personalizado del ticket) a esa vista de catálogo.

Si la configuración regional o la capa no se asignan correctamente, es posible que los datos de imagen **no aparezcan** o que se comporten de forma inesperada, aunque la sincronización se haya realizado correctamente en sentido ascendente.

## Sincronización

Una vez configurada, la integración sincroniza `product-asset` asignaciones automáticamente.

Consulte [Coincidencia automática personalizada](../synchronize/custom-match.md) para obtener más información.

### Ejemplo de flujo de trabajo Coincidencia por SKU

Flujo típico al añadir un recurso existente a un nuevo producto:

1. Crear el producto en [!DNL Commerce Optimizer] (mediante API o ingesta de datos). El producto puede existir sin imágenes inicialmente.

1. En AEM Assets, abra el recurso que desee asignar al producto.

1. Agregue el SKU del producto a los metadatos de **commerce:skus** y asigne las funciones de imagen (por ejemplo, `thumbnail`, `image`).

1. Apruebe el recurso para su envío. Esto déclencheur el evento que procesa Assets Integration Service.

1. El servicio de integración de Assets envía la asignación de imagen de producto a [!DNL Commerce Optimizer]. El producto de [!DNL Commerce Optimizer] se ha actualizado con las imágenes del recurso.

1. Compruebe que la imagen esté visible. Deje tiempo para que se complete la sincronización (normalmente en unos minutos) y, a continuación, compruebe el producto en la interfaz de usuario de [!DNL Commerce Optimizer] (por ejemplo, Sincronización de datos o vista de catálogo) o consulte las API de tienda (Servicio de catálogo, Live Search, API de GraphQL de tienda) para confirmar que se devuelve la imagen.

## Administración de funciones de imagen

Cuando un producto tiene varios recursos que utilizan la misma función de imagen (por ejemplo, dos recursos con la función `thumbnail`), la integración garantiza que solo un recurso retenga esa función para evitar funciones duplicadas en la capa [!DNL Commerce Optimizer] y un comportamiento de tienda inesperado.

**Comportamiento:** Cuando se envía una actualización desde los AEM Assets, el recurso actualizado más recientemente recibe el rol de imagen (por ejemplo, `thumbnail`) y el rol se elimina del recurso anterior que lo tenía. Esto evita que aparezcan roles de imagen duplicados en la tienda.

## Más parecido a esto

* [Visuales del producto](../../optimizer/setup/product-visuals.md)
* [Configuración del proyecto de AEM Assets](configure-aem.md)
* [Coincidencia automática personalizada](../synchronize/custom-match.md)
* [Resumen de integración de AEM Assets](../overview.md)
