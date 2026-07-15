---
title: Configuración de AEM Assets para Commerce Optimizer
description: Obtenga información sobre cómo configurar la integración de AEM Assets para  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---


# Configurar AEM Assets para [!DNL Adobe Commerce Optimizer]

[!BADGE Solo SaaS]{type=Positive tooltip="Solo se aplica a los proyectos de Adobe Commerce Optimizer."}

La integración de AEM Assets para [!DNL Adobe Commerce Optimizer] permite que los comerciantes utilicen AEM Assets como solución de administración centralizada de recursos digitales para las imágenes de los productos. Esta guía describe la configuración específica de [!DNL Commerce Optimizer].

El diagrama siguiente es una descripción general de la sincronización de productos entre [!DNL Adobe Commerce Optimizer] y la integración de AEM Assets.

![AEM Assets a [!DNL Commerce Optimizer] flujo](../assets/aco-asset-sync-architecture.png){width="700"}

Esta integración tiene dos flujos de eventos independientes. Ambos usan [Adobe I/O Events](https://developer.adobe.com/events/docs/) para transferir eventos al servicio de integración de Assets, pero cada dirección usa su propio proveedor de eventos:

* **De AEM Assets al servicio de integración de Assets**: cuando se aprueba, rechaza o elimina un recurso, el evento se envía al servicio de integración de Assets. El servicio hace coincidir recursos con productos que usan `match-by-SKU` (controlado por metadatos) o un [elemento de coincidencia personalizado (App Builder)](../synchronize/custom-match.md){target=_blank}, y luego envía las asignaciones de `product-asset` a [!DNL Commerce Optimizer], donde se almacenan como capas de producto.

  >[!NOTE]
  >
  >La capa de catálogo `AEM-Assets` utilizada por la integración se crea automáticamente durante la incorporación. No es necesario crearlo de antemano. Para obtener información general sobre cómo funcionan las capas de catálogo y cómo se comporta la capa AEM-Assets, consulte [AEM-Assets layer](../../optimizer/setup/catalog-layer.md#aem-assets-layer).

* **De [!DNL Adobe Commerce Optimizer] al servicio de integración de Assets**: cuando se actualiza un producto en [!DNL Commerce Optimizer], el evento se entrega al servicio de integración de Assets. El servicio sincroniza todas las asignaciones de recursos coincidentes con [!DNL Commerce Optimizer].

## Limitaciones

La integración de [!DNL Commerce Optimizer] tiene las siguientes limitaciones:

### Restricciones relacionadas con la capa

* Utilice una capa específica para el contenido de los AEM Assets.

  Las cargas enviadas desde los AEM Assets rellenan una capa de catálogo de Commerce Optimizer. Los valores de esa capa sobrescriben los atributos del catálogo base donde se proporcionan los campos. Cuando la integración omite un campo en la carga útil, los valores correspondientes de esa capa se pueden sobrescribir con valores vacíos. Compartir una capa con flujos de trabajo de Commerce no relacionados (o reutilizar una capa que ya almacena datos de productos que no son de AEM o Assets) puede causar **pérdida involuntaria de datos** o sobrescrituras confusas. Reserve el nombre de la capa (por ejemplo, la predeterminada **`AEM-Assets`**) principalmente para la sincronización de imágenes de producto impulsada por AEM.

* La integración admite un origen de catálogo por inquilino: una sola configuración regional y una capa con nombre. En este momento no se admite la configuración de varias capas AEM-Assets o varias configuraciones regionales para el mismo inquilino.

* La reutilización de una capa existente o el uso compartido de una capa con flujos de trabajo no relacionados es una causa frecuente de casos de soporte evitables.

### Otras restricciones

* **Solo imágenes**: la integración no admite vídeo u otros tipos de medios en este momento.
* **No hay imágenes de categoría**: la sincronización de imágenes de categoría no está disponible. No se admiten imágenes de categoría de AEM Assets para el Selector de Assets (inserción en la IU).
* **Sin distinción de varios sitios**: la integración no administra varios sitios; se muestra una imagen asociada a un producto de la misma manera en todos los canales y directivas.
* **Posición/orden de la imagen**: no se admiten la posición y el orden de la imagen.
* **El producto debe existir**: Si el producto no existe en [!DNL Commerce Optimizer], la capa no se crea para esa asignación de productos a recursos.

## Requisitos previos

Antes de configurar la integración, asegúrese de lo siguiente:

* Una instancia de [!DNL Adobe Commerce Optimizer] activa con la asignación de **elementos visuales del producto** (agrupa Dynamic Media con capacidades de OpenAPI + [Prime de AEM Assets](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-prime)) o una licencia de AEM Assets proporcionada por el cliente (por ejemplo, **Ultimate de AEM Assets**) con Dynamic Media habilitado.
* Acceso a un entorno de as a Cloud Service de AEM Assets.
* Tanto [!DNL Commerce Optimizer] como AEM Assets en la misma organización de Adobe IMS.
* Dynamic Media con OpenAPI habilitado en su entorno de AEM Assets (consulte [Configuración del proyecto de AEM Assets](configure-aem.md#prerequisites) para ver los pasos de habilitación).

### Configuración de AEM Assets primero

Para admitir la integración, configure el proyecto de AEM Assets y los entornos antes de iniciar el proceso para incorporar la integración de AEM Assets con [!DNL Commerce Optimizer]. Esto incluye habilitar Dynamic Media con funciones de OpenAPI y hacer que los esquemas de metadatos, los eventos y la interfaz de usuario de Commerce estén disponibles en su proyecto de AEM.

* [!BADGE Recomendado]{type=Positive} En la versión de AEM `2026.5.26309` y posterior, habilite la integración desde Cloud Manager sin implementación de código. Seguir [Habilitar la integración de Commerce (autoservicio)](configure-aem.md#enable-aem-commerce-self-service).

* En versiones anteriores de AEM, implemente el paquete `assets-commerce` manualmente.
Seguir [Instalar el paquete de assets-commerce manualmente](configure-aem.md#install-the-assets-commerce-package-manually).

>[!TIP]
>
> Puede comprobar la versión actual de AEM en el menú superior derecho: **[!UICONTROL Help]** > **[!UICONTROL About AEM]**.

## Incorporación

>[!IMPORTANT]
>
>Antes de enviar un vale de soporte técnico para habilitar la integración con [!DNL Commerce Optimizer], complete el proceso para [configurar AEM Assets](#configure-aem-assets-first). La compatibilidad requiere que los entornos y el proyecto de los AEM Assets estén configurados para admitir la integración de AEM Commerce, incluida la implementación del paquete `assets-commerce` (o equivalente de autoservicio) para metadatos y eventos. Abrir un ticket antes de configurar AEM puede retrasar la incorporación.

Para integrar la integración de AEM Assets con [!DNL Commerce Optimizer], el Soporte técnico de Adobe debe registrar su instancia de Adobe Commerce Optimizer con el Servicio de integración de Assets y suscribirla a:

* Eventos de AEM Assets (recursos aprobados, actualizados y eliminados)
* [!DNL Commerce Optimizer] eventos de catálogo (producto creado, actualizado)

Para iniciar este proceso, [cree un vale de soporte técnico](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) que incluya la siguiente información:

* **[!DNL Adobe Commerce Optimizer]ID de inquilino** (ID de instancia) encontrado en su URL [!DNL Commerce Optimizer] o IU de Commerce Cloud Manager.
* **ID de programa AEM e ID de entorno** que configuró al [configurar AEM Assets](#configure-aem-assets-first) para la integración.
* **Regla de coincidencia**: Coincidencia por SKU o [coincidencia externa (App Builder)](../synchronize/custom-match.md){target=_blank}.
* **Capa**: El nombre de la capa de catálogo con la que registrar al inquilino (consulte **Restricciones relacionadas con la capa**). Especifique un nombre personalizado solo si es intencional; de lo contrario, se usa el valor predeterminado **`AEM-Assets`**.
* **Configuración regional**: La configuración regional de origen del catálogo con la que registrar al inquilino (por ejemplo, `en-US`). Esta configuración regional debe coincidir con la configuración regional que utilice en la vista de catálogo y en los datos del catálogo de productos.

### Configuración de la vista de catálogo

Una vez registrado el inquilino [!DNL Commerce Optimizer], configure la vista del catálogo para que la tienda y las API muestren datos de imagen impulsados por AEM:

* **Seleccione el origen del catálogo (configuración regional)**: seleccione la misma configuración regional especificada en su vale de soporte técnico (por ejemplo, **`en-US`**). La integración registra una configuración regional por inquilino; una discrepancia impide que las imágenes sincronizadas aparezcan en la vista de catálogo deseada.
* **Asignar la capa de catálogo** — Asigne la capa **`AEM-Assets`** (o su nombre de capa personalizado del ticket) a esa vista de catálogo.

Si la configuración regional o la capa no se asignan correctamente, los datos de imagen **no aparecen** o se comportan de forma inesperada, aunque la sincronización se haya realizado correctamente en sentido ascendente.

## Sincronización

Una vez configurada, la integración sincroniza `product-asset` asignaciones automáticamente.

Consulte [Coincidencia automática personalizada](../synchronize/custom-match.md) para obtener más información.

### Ejemplo de flujo de trabajo Coincidencia por SKU

Flujo típico al añadir un recurso existente a un nuevo producto:

1. Crear el producto en [!DNL Commerce Optimizer] (mediante API o ingesta de datos). El producto puede existir sin imágenes inicialmente.

1. En AEM Assets, abra el recurso que desee asignar al producto.

1. Agregue el SKU del producto a los metadatos de **commerce:skus** y asigne las funciones de imagen (por ejemplo, `thumbnail`, `image`).

1. Apruebe el recurso para su envío. Esto déclencheur el evento que procesa el servicio de integración de Assets.

1. El servicio de integración de Assets envía la asignación de imagen de producto a [!DNL Commerce Optimizer]. El producto de [!DNL Commerce Optimizer] se ha actualizado con las imágenes del recurso.

1. Compruebe que la imagen esté visible. Espere unos minutos para que se complete la sincronización y, a continuación, compruebe el producto en la interfaz de usuario de [!DNL Commerce Optimizer] o consulte las API de tienda para confirmar que se devuelve la imagen.

## Administración de funciones de imagen

Cuando un producto tiene varios recursos que utilizan la misma función de imagen (por ejemplo, dos recursos con la función `thumbnail`), la integración garantiza que solo un recurso retenga esa función para evitar funciones duplicadas en la capa [!DNL Commerce Optimizer] y un comportamiento de tienda inesperado.

**Comportamiento:** Cuando se envía una actualización desde los AEM Assets, el recurso actualizado más recientemente recibe el rol de imagen (por ejemplo, `thumbnail`) y el rol se elimina del recurso anterior que lo tenía. Esto evita que aparezcan roles de imagen duplicados en la tienda.

## Más parecido a esto

* [Visuales del producto](../../optimizer/setup/product-visuals.md)
* [Configuración del proyecto de AEM Assets](configure-aem.md)
* [Coincidencia automática personalizada](../synchronize/custom-match.md)
* [Resumen de integración de AEM Assets](../overview.md)
