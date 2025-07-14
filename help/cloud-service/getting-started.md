---
title: Introducción a  [!DNL Adobe Commerce as a Cloud Service]
description: Obtenga información sobre cómo empezar a usar  [!DNL Adobe Commerce as a Cloud Service].
role: Admin, Developer, User
exl-id: 58d98b9e-b41d-44db-9666-c924a5b005b3
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 81dd617b0a6460b8dcb01c0a21b696663b0ae493
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Primeros pasos

[!DNL Adobe Commerce as a Cloud Service] proporciona la mayor parte de la configuración de forma predeterminada. Después de completar algunos procesos de configuración básicos, su tienda estará lista en poco tiempo. Esta guía le explica cómo crear y trabajar con una instancia.

Haga clic en las pestañas siguientes para ver información general de flujo de trabajo de alto nivel de los siguientes tipos de usuarios:

* Administradores
* Comerciantes
* Desarrolladores

>[!BEGINTABS]

>[!TAB Flujo de trabajo de administrador y comerciante]

Este diagrama proporciona información general de alto nivel sobre cómo los administradores y comerciantes acceden y administran [!DNL Adobe Commerce as a Cloud Service] instancias. Consulte la [Guía de Adobe Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html) para obtener más información sobre los flujos de trabajo de administrador.

![[!DNL Adobe Commerce as a Cloud Service] diagrama de flujo comercial](./assets/merchant-flow.svg){zoomable="yes"}

>[!TAB Flujo de trabajo para desarrolladores]

Este diagrama proporciona información general de alto nivel sobre cómo los desarrolladores crean integraciones para [!DNL Adobe Commerce as a Cloud Service] mediante App Builder. Consulte la [documentación de la API](https://developer.adobe.com/commerce/webapi/rest/) para obtener más información.

![[!DNL Adobe Commerce as a Cloud Service] diagrama de flujo de desarrollador](./assets/developer-flow.svg){zoomable="yes"}

>[!ENDTABS]

## Creación de una instancia

>[!NOTE]
>
>Para poder crear una instancia, el administrador de productos o del sistema de su organización debe agregarlo como usuario del producto [!DNL Adobe Commerce as a Cloud Service]. Consulte [Agregar usuarios y administradores](./user-management.md#add-users-and-admins) para obtener más información.

[!DNL Adobe Commerce as a Cloud Service] instancias utilizan un sistema basado en crédito. Puede crear varias instancias, pero cada una requiere una cantidad relativa de créditos. La cantidad de créditos que tienes inicialmente depende de tu suscripción.

1. Inicie sesión en su cuenta de [Adobe Experience Cloud](https://experience.adobe.com/).

1. En [!UICONTROL Quick access], haga clic en [!UICONTROL **Commerce**] para abrir [!UICONTROL Commerce Cloud Manager].

   [!UICONTROL Commerce Cloud Manager] muestra una lista de [!DNL Adobe Commerce as a Cloud Service] instancias disponibles en su organización de Adobe IMS.

1. Haga clic en [!UICONTROL **Agregar instancia**] en la esquina superior derecha de la pantalla.

   ![Crear instancia](./assets/create-instance.png){width="50%" align="center" zoomable="yes"}

1. Seleccione [!UICONTROL **Commerce as a Cloud Service**].

1. Escriba un **Nombre** y una **Descripción** para su instancia.

1. Seleccione la región en la que desea alojar la instancia.

   >[!NOTE]
   >
   >Una vez creada la instancia, no se puede modificar la región.

1. Elija [!UICONTROL **Tipo de entorno**] para su instancia. Puede elegir entre las siguientes opciones:

   * [!UICONTROL **Espacio aislado**]: ideal para fines de diseño y prueba. Debe comenzar el recorrido de [!DNL Adobe Commerce as a Cloud Service] usando el entorno de espacio aislado.
   * [!UICONTROL **Producción**]: para tiendas en vivo y sitios de cara al cliente.

   >[!NOTE]
   >
   >* Actualmente, las instancias de zona protegida están limitadas a la región de América del Norte.
   >* La opción para instalar datos de ejemplo no está disponible actualmente.

1. Haga clic en [!UICONTROL **Agregar instancia**].

## Acceso a una instancia

Después de crear una instancia, puede obtener acceso a ella desde el [!UICONTROL Commerce Cloud Manager].

1. Inicie sesión en su cuenta de [Adobe Experience Cloud](https://experience.adobe.com/).

1. En [!UICONTROL Quick access], haga clic en [!UICONTROL **Commerce**] para abrir [!UICONTROL Commerce Cloud Manager].

   [!UICONTROL Commerce Cloud Manager] muestra una lista de instancias disponibles en su organización de Adobe IMS.

1. Para abrir [!UICONTROL Commerce Admin] de una instancia, haga clic en el nombre de la instancia.

>[!TIP]
>
>Para ver información sobre la instancia, incluidos los extremos de REST y GraphQL y la URL del administrador, haga clic en el icono de información situado junto al nombre de la instancia.

## Importar el catálogo

De manera predeterminada, las instancias de [!DNL Adobe Commerce as a Cloud Service] no incluyen datos de productos. Tiene la opción de incluir datos de productos de ejemplo al crear una instancia para fines de prueba y aprendizaje antes de importar su propio catálogo.

Existen dos maneras de importar el catálogo en [!DNL Adobe Commerce as a Cloud Service]:

* [**Administrador de Commerce**](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import): Una interfaz fácil de usar que le permite importar los datos del catálogo en unos pocos clics.
* [**Importar API JSON**](https://developer.adobe.com/commerce/webapi/rest/modules/import/#import-json-api): una API de REST que le permite importar los datos del catálogo mediante programación.

<!-- TODO

- Add guidance about how to choose which method to use
- Add guidance for new vs existing customers (cross-reference OR and _include file for migration content)

-->

## Configurar la tienda

Ahora que has creado una instancia, estás listo para continuar [configurando](storefront.md) tu tienda Commerce con tecnología Edge Delivery Services.
