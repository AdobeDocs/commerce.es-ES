---
title: Configuración del proyecto de AEM Assets
description: Habilite la sincronización perfecta de recursos entre Adobe Commerce y los AEM Assets agregando los metadatos necesarios para la integración.
feature: CMS, Media, Integration
exl-id: a5d2cbab-5ea1-446b-8ab2-2c638128a40c
source-git-commit: 995fb071953ddad6cb2076207910679905bb0347
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# Configuración del proyecto de AEM Assets para que admita metadatos de Commerce

Para administrar archivos de recursos de Commerce en AEM Assets, complete los siguientes pasos para configurar el proyecto de AEM Assets con el código de plantillas y los metadatos necesarios para administrar los recursos de Commerce desde el entorno de creación de AEM.

* **Paso 1:** Instale una plantilla de proyecto de AEM con el código de repetidor para agregar los recursos de esquema de metadatos y el área de nombres de Commerce a la configuración del entorno de as a Cloud Service de Experience Manager Assets.
* **Paso 2:** Configure el perfil de metadatos para aplicarlo a los archivos de recursos de Commerce

## Añada el código de las plantillas al proyecto de AEM

Adobe proporciona una plantilla de AEM Commerce, `assets-commerce`, para agregar recursos de esquema de metadatos y área de nombres de Commerce a la configuración del entorno de Experience Manager Assets as a Cloud Service. Implemente este código en su entorno como paquete de **Maven**. A continuación, configure los metadatos de Commerce en el entorno de creación de AEM Assets para completar la configuración.

La plantilla agrega los siguientes recursos al entorno de creación de AEM Assets:

* Un [espacio de nombres personalizado](https://github.com/ankumalh/assets-commerce/blob/main/ui.config/jcr_root/apps/commerce/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~commerce-namespaces.cfg.json), `Commerce` para identificar propiedades relacionadas con Commerce.

   * Un tipo de metadatos personalizado `commerce:isCommerce` con la etiqueta `Eligible for Commerce` para etiquetar recursos de Commerce asociados con un proyecto de Adobe Commerce.

   * Un tipo de metadatos personalizado `commerce:skus` y un componente de interfaz de usuario correspondiente para agregar una propiedad **[!UICONTROL Product Data]**. Los datos de producto incluyen las propiedades de metadatos para asociar un recurso de Commerce con los SKU de producto.

     ![Control de IU de datos de productos personalizados](../assets/aem-commerce-sku-metadata-fields-from-template.png){width="600" zoomable="yes"}

   * Atributos de tipo de metadatos personalizados `commerce:roles` y `commerce:positions` para mostrar cómo se visualiza el recurso en Commerce.

* Un formulario de esquema de metadatos con una pestaña de Commerce que incluye los campos `Eligible for Commerce` y `Product Data` para etiquetar recursos de Commerce. El formulario también proporciona opciones para mostrar u ocultar los campos `roles` y `position` de la interfaz de usuario de AEM Assets.

  ![Ficha Commerce para el formulario de esquema de metadatos de AEM Assets](../assets/assets-configure-metadata-schema-form-editor.png){width="600" zoomable="yes"}

* Un [recurso de ejemplo etiquetado y aprobado por Commerce](https://github.com/ankumalh/assets-commerce/blob/main/ui.content/src/main/content/jcr_root/content/dam/wknd/en/activities/hiking/equipment_6.jpg/.content.xml) `equipment_6.jpg` para admitir la sincronización inicial de recursos. Solo los recursos de Commerce aprobados se pueden sincronizar de AEM Assets a Adobe Commerce.

>[!NOTE]
>
> Consulte la página [readme](https://github.com/ankumalh/assets-commerce) para obtener más información sobre la **plantilla de AEM Commerce**.

### Requisitos previos

Necesita los siguientes recursos y permisos para implementar el paquete `commerce-assets` en el entorno de AEM de as a Cloud Service para AEM Assets:

* [Acceso al Programa Cloud Manager de AEM Assets y a los entornos](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager#access-sysadmin-bo) con los roles de Administrador de implementación y Programa.

* Un [entorno de desarrollo local de AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview) y conocimiento del proceso de desarrollo local de AEM.

* Comprenda la [estructura del proyecto AEM](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure) y cómo implementar paquetes de contenido personalizado mediante Cloud Manager.

### Instalar el paquete `commerce-assets`

1. Desde AEM Cloud Manager, cree entornos de producción y ensayo para su proyecto de AEM Assets, si es necesario.

1. Configure una canalización de implementación, si es necesario.

1. En GitHub, descargue el código de la [plantilla de AEM Commerce](https://github.com/ankumalh/assets-commerce).

1. Desde su [entorno de desarrollo local de AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview), instale el código personalizado en la configuración de su entorno de AEM Assets como paquete de Maven o copiando manualmente el código en la configuración de proyecto existente.

1. Confirme los cambios e inserte la rama de desarrollo local en el repositorio de Git de Cloud Manager.

1. Desde AEM Cloud Manager, [implemente su código para actualizar el entorno de AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code#deploying-code-with-cloud-manager).

## Opcional. Configuración de un perfil de metadatos

En el entorno de creación de AEM Assets, establezca los valores predeterminados para los metadatos de recursos de Commerce creando un perfil de metadatos. A continuación, aplique el nuevo perfil a las carpetas de recursos de AEM para utilizar automáticamente estos valores predeterminados. Esta configuración optimiza el procesamiento de recursos al reducir los pasos manuales.

Al configurar el perfil de metadatos, solo debe configurar los siguientes componentes:

* Agregue una pestaña Commerce. Esta pestaña habilita las opciones de configuración específicas de Commerce que agrega la plantilla
* Agregue el campo `Eligible for Commerce` a la ficha Commerce.

El componente de interfaz de usuario de datos del producto se agrega automáticamente en función de la plantilla.

### Definición del perfil de metadatos

1. Inicie sesión en el entorno de creación de Adobe Experience Manager.

1. En Adobe Experience Manager Workspace, vaya al espacio de trabajo Administración de contenido de autor para AEM Assets haciendo clic en el icono Adobe Experience Manager.

   ![AEM Assets creando](../assets/aem-assets-authoring.png){width="600" zoomable="yes"}

1. Abra las Herramientas de administración seleccionando el icono de martillo.

   ![Administrador de autor de AEM administra perfiles de metadatos](../assets/aem-manage-metadata-profiles.png){width="600" zoomable="yes"}

1. Abra la página de configuración del perfil haciendo clic en **[!UICONTROL Metadata Profiles]**.

1. **[!UICONTROL Create]** un perfil de metadatos para la integración de Commerce.

   ![El administrador de autores de AEM agregó perfiles de metadatos](../assets/aem-create-metadata-profile.png){width="600" zoomable="yes"}

1. Agregue una pestaña para los metadatos de Commerce.

   1. A la izquierda, haga clic en **[!UICONTROL Settings]**.

   1. Haga clic en **[!UICONTROL +]** en la sección de la ficha y, a continuación, especifique **[!UICONTROL Tab Name]**, `Commerce`.

1. Agregue el campo `Eligible for Commerce` al formulario.

   ![El administrador de autores de AEM agregó campos de metadatos al perfil](../assets/aem-edit-metadata-profile-fields.png){width="600" zoomable="yes"}

   * Haga clic en **[!UICONTROL Build form]**.

   * Arrastre el campo `Single Line text` al formulario.

   * Agregue el texto `Eligible for Commerce` para la etiqueta haciendo clic en **[!UICONTROL Field Label]**.

   * En la pestaña Configuración, agregue el texto de la etiqueta a **Etiqueta de campo**.

   * Establezca el texto del marcador de posición en `yes`.

   * En el campo **[!UICONTROL Map to Property]**, copie y pegue el siguiente valor

     ```terminal
     ./jcr:content/metadata/commerce:isCommerce
     ```

1. Opcional. Para sincronizar automáticamente los recursos de Commerce aprobados a medida que se cargan en el entorno de AEM Assets, establezca el valor predeterminado del campo _[!UICONTROL Review Status]_en la pestaña `Basic` en `approved`.

1. Guarde la actualización.

#### Aplicar el perfil de metadatos a la carpeta de origen de los recursos de Commerce

1. En la página [!UICONTROL  Metadata Profiles], seleccione el perfil de integración de Commerce.

1. En el menú de acción, seleccione **[!UICONTROL Apply Metadata Profiles to Folders]**.

1. Seleccione la carpeta que contiene los recursos de Commerce.

   Cree una carpeta de Commerce si no existe.

1. Haga clic en **[!UICONTROL Apply]**.

## Siguiente paso

[!BADGE Solo PaaS]{type=Informative tooltip="Solo se aplica a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe)."} [Instalar paquetes de Adobe Commerce](configure-commerce.md)
