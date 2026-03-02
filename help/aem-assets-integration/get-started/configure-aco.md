---
title: Configuración de AEM Assets para Commerce Optimizer
description: Obtenga información sobre cómo configurar la integración de AEM Assets para  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
source-git-commit: bf1d88ef7daec25872678bb27bce0bb7c97fd296
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---


# Configurar AEM Assets para [!DNL Adobe Commerce Optimizer]

[!BADGE Solo SaaS]{type=Positive tooltip="Solo se aplica a los proyectos de Adobe Commerce Optimizer."}

La integración de AEM Assets para [!DNL Adobe Commerce Optimizer] permite que los comerciantes utilicen AEM Assets como solución de administración centralizada de recursos digitales para las imágenes de los productos. Esta guía describe la configuración específica de [!DNL Commerce Optimizer].

A diferencia de Adobe Commerce (PaaS) o Adobe Commerce as a Cloud Service (ACCS), [!DNL Commerce Optimizer] no tiene una interfaz de usuario de configuración de administración. Para habilitar la integración, cree un vale de soporte con los detalles de [!DNL Adobe Commerce Optimizer] y los AEM Assets. El Soporte de Adobe configura la integración y registra su inquilino con el Servicio de integración de Assets.

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
* Dynamic Media con OpenAPI habilitado en su entorno de AEM Assets.

## Incorporación

Para integrar la integración de AEM Assets con [!DNL Commerce Optimizer], debe [Crear un vale de soporte](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket).

El Soporte de Adobe utiliza la información de su ticket para registrar su inquilino con el Servicio de integración de Assets y configurar la integración.

Incluya la siguiente información en su vale de soporte:

* **[!DNL Adobe Commerce Optimizer]ID de inquilino** (ID de instancia) encontrado en su URL [!DNL Commerce Optimizer] o IU de Commerce Cloud Manager.
* **ID de programa de AEM**.
* **ID. de entorno de AEM**.
* **Regla de coincidencia**: Coincidencia por SKU o [coincidencia externa (App Builder)](../synchronize/custom-match.md){target=_blank}.
* **Capa**: El nombre de la capa de catálogo con la que registrar al inquilino. Especifique un nombre personalizado si es necesario. De lo contrario, se utiliza el valor predeterminado `AEM-Assets`.
* **Configuración regional**: La configuración regional de origen del catálogo con la que registrar al inquilino (por ejemplo, `en-US`).

>[!IMPORTANT]
>
> La integración admite una fuente por inquilino, que es la combinación de una configuración regional y una capa.

Una vez que el Soporte de Adobe procesa el ticket, la integración se configura y el inquilino se registra con el Servicio de integración de Assets.

Una vez completada la incorporación:

1. **Registro con el servicio de integración de Assets**: el inquilino de [!DNL Commerce Optimizer] está registrado con el servicio de integración de Assets usando el identificador de inquilino de [!DNL Adobe Commerce Optimizer], el identificador de programa de AEM, el identificador de entorno de AEM y el inquilino.

1. **Configuración de autenticación**: la autenticación del token del servicio IMS está configurada entre [!DNL Commerce Optimizer] y el servicio de integración de Assets para una comunicación segura.

1. **Suscripción de evento**: Assets Integration Service se suscribe a:

   * Eventos de AEM Assets (recursos aprobados, actualizados y eliminados)
   * [!DNL Commerce Optimizer] eventos de catálogo (producto creado, actualizado)

### Limitaciones

La integración de [!DNL Commerce Optimizer] tiene las siguientes limitaciones:

* **Una capa por comerciante**: la integración de AEM Assets admite una capa de AEM-Assets por comerciante (una fuente por inquilino). En este momento no se admite la configuración de varias capas por comerciante.
* **Solo imágenes**: la integración no admite vídeo ni otros tipos de medios.
* **Sin imágenes de categoría**: la sincronización de imágenes de categoría no está disponible. No se admiten imágenes de categoría de AEM Assets para el Selector de Assets (inserción en la IU).
* **Sin distinción de varios sitios**: la integración no gestiona varios sitios; se muestra la misma imagen asociada a un producto en todos los canales y directivas.
* **Posición/orden de la imagen**: no se admiten la posición y el orden de la imagen.
* **El producto debe existir**: si el producto no existe en [!DNL Commerce Optimizer], la capa no se creará para esa asignación de producto a recurso.
* **Sobrescritura de campo de capa**: los valores de una capa sobrescriben el catálogo base. Si un campo no se envía en la carga útil de capa, se puede sobrescribir con un valor vacío. Utilice una capa específica para el contenido de los AEM Assets; la reutilización de una capa existente para otros fines puede causar la pérdida involuntaria de datos.

### Configuración de los AEM Assets

El proceso de instalación y configuración de los AEM Assets para [!DNL Commerce Optimizer] es el mismo que para Adobe Commerce as a Cloud Service. Consulte [Configuración del proyecto de AEM Assets para admitir metadatos de Commerce](configure-aem.md) para ver los pasos completos.

Asegúrese de que el entorno de los AEM Assets esté listo:

1. **Configuración de AEM Assets**: configure el perfil de metadatos de Commerce. Consulte [Configurar un perfil de metadatos](configure-aem.md#configure-a-metadata-profile).

1. **Habilitación de Dynamic Media**: compruebe que Dynamic Media con las capacidades de OpenAPI esté habilitada en su entorno de AEM Assets.

## Configuración de AEM Assets

Para habilitar la sincronización de productos y recursos, configure el entorno de AEM Assets.

### Paso 1: Habilitar Dynamic Media con OpenAPI

Dynamic Media con OpenAPI debe estar habilitado en el entorno de los AEM Assets. Las licencias Visuales del producto y de nuevos AEM Assets le permiten activarlo en forma de autoservicio a través de Cloud Manager. Las licencias de AEM Assets más antiguas requieren la asistencia de Adobe para habilitarlas. Consulte [Configuración del proyecto de AEM Assets](configure-aem.md#prerequisites) para ver los pasos de habilitación.

### Paso 2: Opcional. Configuración del perfil de metadatos de Commerce

Configure el perfil de metadatos en AEM Assets para almacenar metadatos específicos de Commerce.

Consulte [Configurar un perfil de metadatos](configure-aem.md#step-2-optional-configure-a-metadata-profile) para obtener instrucciones detalladas.

### Paso 3: Aplicar metadatos a los recursos

Añada metadatos de Commerce a las imágenes de sus productos en AEM Assets.

Consulte el [contenido del paquete de AEM Commerce](configure-aem.md#aem-commerce-assets-commerce-package-contents) para ver las definiciones de los campos y [Configurar un perfil de metadatos](configure-aem.md#step-2-optional-configure-a-metadata-profile) para ver los pasos de configuración.

El recurso debe estar en estado **aprobado** para la sincronización de datos con el déclencheur. Guardar metadatos por sí solo no almacena el evento en déclencheur.

>[!CAUTION]
>
> Asigne la capa `AEM-Assets` a su [vista de catálogo](https://experienceleague.adobe.com/es/docs/commerce/optimizer/setup/catalog-view). Si la capa no está asignada, los datos de imagen del producto pueden sobrescribirse inesperadamente.

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
