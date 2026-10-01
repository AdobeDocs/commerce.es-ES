---
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%
---
# Obtener detalles de instancia de [!DNL Commerce Optimizer]

Obtenga el _id. de inquilino_ del campo _[!DNL Instance Id]_&#x200B;en la instancia [!DNL Commerce Optimizer] [[!DNL Instance details] página](/help/optimizer/get-started.md#manage-instances), o de la URL utilizada para acceder a la instancia. Por ejemplo, en `https://experience.adobe.com/#/@<your organization>/in:<tenant>/commerce-optimizer-studio/home`.

1. En el Administrador de Commerce, seleccione **[!UICONTROL Adobe Commerce Optimizer]** para mostrar la página de configuración con instrucciones.

   ![[!DNL Commerce Optimizer] página de configuración](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. Desde la línea de comandos, [use SSH](https://experienceleague.adobe.com/es/docs/commerce-on-cloud/user-guide/develop/secure-connections) para conectarse al entorno de ensayo [!DNL Adobe Commerce].

1. Para configurar la integración, ejecute el siguiente comando CLI [!DNL Adobe Commerce], reemplazando los valores de marcador de posición por los valores de su proyecto [!DNL Commerce Optimizer]:

   ```shell
   bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
   ```

1. Compruebe la conexión volviendo al administrador de Commerce y seleccionando la opción [!UICONTROL Adobe Commerce Optimizer].

   Al seleccionar la opción, se abre la interfaz de usuario de [!DNL Commerce Optimizer] en una nueva pestaña.
