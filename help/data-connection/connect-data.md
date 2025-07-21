---
title: Conexión de datos de Commerce a Adobe Experience Platform
description: Obtenga información sobre cómo conectar los datos de Commerce a Adobe Experience Platform.
feature: Personalization, Integration, Configuration
exl-id: 8ba33277-38a5-45af-86e0-906cfb3b998d
source-git-commit: 5f7565f5bb80fcc65cbbcdc31c5c3b12fed4e5ee
workflow-type: tm+mt
source-wordcount: '2917'
ht-degree: 0%

---

# Conexión de datos de Commerce a Adobe Experience Platform

Al instalar la extensión [!DNL Data Connection], aparecen dos nuevas páginas de configuración en el menú **Sistema** en **Servicios** en Commerce _Admin_.

- Commerce Services Connector
- [!DNL Data Connection]

Para conectar la instancia de Adobe Commerce a Adobe Experience Platform, debe configurar ambos conectores, empezando por el conector de Commerce Services y terminando con la extensión [!DNL Data Connection].

## Configuración del conector de Servicios de Commerce

Si ya ha instalado un servicio de Adobe Commerce, probablemente ya haya configurado el conector de servicios de Commerce. Si no es así, debe completar las tareas siguientes en la página [Conector de servicios de Commerce](../landing/saas.md):

1. Inicie sesión en su cuenta de Commerce para [recuperar las claves de API de producción y de zona protegida](../landing/saas.md#credentials).
1. Seleccione un [espacio de datos SaaS](../landing/saas.md#saas-configuration).
1. Inicie sesión en su cuenta de Adobe para [recuperar su ID de organización](../landing/saas.md#ims-organization-optional).

Después de configurar el conector de Commerce Services, configure la extensión [!DNL Data Connection].

## Configurar la extensión [!DNL Data Connection]

En esta sección, aprenderá a configurar la extensión [!DNL Data Connection].

### Agregar detalles de cuenta de servicio y credenciales

Si planea recopilar y enviar [datos históricos de pedidos](#send-historical-order-data) o [datos de perfil del cliente](#send-customer-profile-data), debe agregar detalles de cuenta de servicio y credenciales. Además, si está configurando la extensión [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=es), debe completar estos pasos.

Si solo está recopilando y enviando datos de tienda u oficina, puede saltar a la sección [general](#general).

#### Paso 1: Crear un proyecto en Adobe Developer Console

Cree un proyecto en Adobe Developer Console que autentique Commerce para que pueda realizar llamadas a la API de Experience Platform.

Para crear el proyecto, sigue los pasos descritos en el tutorial [Autenticar y acceder a las API de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=es).

A medida que avance en el tutorial, asegúrese de que su proyecto tenga lo siguiente:

- Acceso a los siguientes [perfiles de producto](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=es#select-product-profiles): **Acceso predeterminado para todo tipo de producción** y **Acceso predeterminado para todo AEP**.
- Se han configurado [funciones y permisos correctos](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=es#assign-api-to-a-role).
- Si ha decidido utilizar JSON Web Tokens (JWT) como método de autenticación de servidor a servidor, también debe cargar una clave privada.

El resultado de este paso crea un archivo de configuración que se utiliza en el siguiente paso.

#### Paso 2: Descargar archivo de configuración

Descargar el [archivo de configuración del área de trabajo](https://developer.adobe.com/commerce/extensibility/events/project-setup/#download-the-workspace-configuration-file). El archivo `<workspace-name>.json` contiene todos los valores que necesita ingresar en la página **Detalles de cuenta de servicio/credencial** del administrador de Commerce.

![[!DNL Data Connection] configuración de administración](./assets/epc-admin-config.png){width="700" zoomable="yes"}

1. En el Administrador de Commerce, vaya a **Tiendas** > Configuración > **Configuración** > **Servicios** > **[!DNL Data Connection]**.

1. Seleccione el método de autorización de servidor a servidor que implementó desde el menú **Tipo de autorización de Adobe Developer**. Adobe recomienda utilizar OAuth. JWT se ha desaprobado. [Más información](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

1. (Solo JWT) Copie y pegue el contenido del archivo `private.key` en el campo **Secreto del cliente**. Utilice el siguiente comando para copiar el contenido.

   ```bash
   cat config/private.key | pbcopy
   ```

   Consulte [Autenticación de cuenta de servicio (JWT)](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) para obtener más información sobre el archivo `private.key`.

1. Copie el contenido del archivo `<workspace-name>.json` en los campos **Detalles de cuenta de servicio/credencial**, como `"client_id"`, `"client_secrets"`, `"technical_account_email"`, `"technical_account_id"`, etc.

1. Haga clic en **Guardar configuración**.

1. Haga clic en el botón **[!UICONTROL Test connection]** para asegurarse de que la información de cuenta de servicio y credenciales que ha introducido es correcta.

### General

1. En el Administrador, vaya a **Sistema** > Servicios > **[!DNL Data Connection]**.

   Configuración de ![[!DNL Data Connection]](./assets/epc-settings.png){width="700" zoomable="yes"}

1. En la ficha **Configuración** en **General**, compruebe el identificador asociado a su cuenta de Adobe Experience Platform, según la configuración de [Commerce Services Connector](../landing/saas.md#organizationid). El ID de organización es global. Solo se puede asociar un ID de organización por cada instancia de Adobe Commerce.

1. En el menú desplegable **Ámbito**, establezca el contexto en **Sitio web**.

1. (Opcional) Si ya tiene [AEP Web SDK (alloy)](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es) implementado en su sitio, habilite la casilla de verificación y agregue el nombre de su AEP Web SDK. De lo contrario, deje estos campos en blanco y la extensión [!DNL Data Connection] implementará uno por usted.

   >[!NOTE]
   >
   >Si especifica su propio AEP Web SDK, la extensión [!DNL Data Connection] utilizará el ID de flujo de datos asociado a dicho SDK y no el ID de flujo de datos especificado en esta página (si existe).

### Recopilación de datos

En esta sección, especifique el tipo de datos que desea recopilar y enviar al perímetro de Experience Platform. Existen tres tipos de datos:

- **Funcionamiento** (datos del lado del cliente) son datos capturados en la tienda. Esto incluye información sobre las interacciones del comprador, como `View Page`, `View Product`, `Add to Cart` y [lista de solicitudes](events.md#b2b-events) (para comerciantes B2B).

- **Back office** (datos del lado del servidor) son datos capturados en los servidores de Commerce. Esto incluye información sobre el estado de un pedido, como si se ha realizado, cancelado, reembolsado, enviado o completado. También incluye [datos históricos de pedidos](#send-historical-order-data).

- El **perfil** son datos relacionados con la información de perfil del comprador. Más información [más](#send-customer-profile-data).

Para asegurarse de que la instancia de Adobe Commerce pueda iniciar la recopilación de datos, revise los [requisitos previos](overview.md#prerequisites).

Consulte el tema de eventos para obtener más información sobre los eventos de [tienda](events.md#storefront-events), [back office](events-backoffice.md) y [perfil](events-backoffice.md#customer-profile-events-server-side).

>[!NOTE]
>
>Todos los campos de la sección **Recopilación de datos** se aplican al ámbito **Sitio web** o superior.

1. Seleccione **Eventos de tienda** si quiere enviar datos de comportamiento de tienda.

1. Seleccione **Eventos de gestiones internas** si desea enviar información sobre el estado del pedido, por ejemplo, si se realizó, canceló, reembolsó o envió un pedido.

   >[!NOTE]
   >
   >Si selecciona **Eventos de back office**, todos los datos de back office se enviarán al perímetro de Experience Platform. Si un comprador decide excluirse de la recopilación de datos, debe establecer explícitamente la preferencia de privacidad del comprador en Experience Platform. Esto es diferente a los eventos de tienda en los que el coleccionista ya gestiona el consentimiento en función de las preferencias del comprador. Obtenga [más información](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/dataset.html?lang=es) sobre cómo establecer las preferencias de privacidad de un comprador en Experience Platform.

1. (Omita este paso si está usando su propio AEP Web SDK). [Cree](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=es#create) un conjunto de datos en Adobe Experience Platform o seleccione un conjunto de datos existente que desee usar para la recopilación. Escriba el id. de secuencia de datos en el campo **id. de secuencia de datos**.

1. Escriba el **ID del conjunto de datos** que desea que contenga sus datos de Commerce. Para encontrar la ID del conjunto de datos:

   1. Abra la interfaz de usuario de Experience Platform y seleccione **Conjuntos de datos** en el panel de navegación izquierdo para abrir el panel **Conjuntos de datos**. El panel enumera todos los conjuntos de datos disponibles para su organización. Se muestran los detalles de cada conjunto de datos enumerado, incluido su nombre, el esquema al que se adhiere y el estado de la ejecución de la ingesta más reciente.
   1. Abra el conjunto de datos asociado al conjunto de datos.
   1. En el panel derecho, vea los detalles sobre el conjunto de datos. Copie el ID del conjunto de datos.

1. Para garantizar que las actualizaciones de datos de eventos de back office se basen en una programación según un trabajo de [cron](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html?lang=es), debe cambiar el índice de `Sales Orders Feed` a `Update by Schedule`.

   1. En la barra lateral _Admin_, vaya a **[!UICONTROL System]** > _[!UICONTROL Tools]_>**[!UICONTROL Index Management]**.

   1. Seleccione la casilla de verificación del indizador `Sales Orders Feed`.

   1. Establezca **[!UICONTROL Actions]** en `Update by Schedule`.

   1. Si está habilitando los datos del back office por primera vez, ejecute los siguientes comandos para reindexar y almacenar en déclencheur una resincronización. Las resincronizaciones posteriores se producen automáticamente siempre y cuando el trabajo de [cron](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html?lang=es) esté configurado correctamente.

      ```bash
      bin/magento index:reindex sales_order_data_exporter_v2
      ```

      ```bash
      bin/magento saas:resync --feed orders
      ```

#### Descripciones de campos

| Campo | Descripción |
|--- |--- |
| Ámbito | Sitio web específico donde desea aplicar los ajustes de configuración. |
| ID de organización (global) | ID que pertenece a la organización que compró el producto Adobe DX. Este ID vincula su instancia de Adobe Commerce con Adobe Experience Platform. |
| ¿AEP Web SDK ya se ha implementado en el sitio? | Seleccione esta casilla de verificación si ha implementado su propio AEP Web SDK en el sitio |
| Nombre de AEP Web SDK (global) | Si ya tiene una Experience Platform Web SDK implementada en el sitio, especifique el nombre de esa SDK en este campo. Esto permite que el Recopilador de eventos de tienda y el SDK de eventos de tienda utilicen su Experience Platform Web SDK en lugar de la versión implementada por la extensión [!DNL Data Connection]. Si no tiene un Experience Platform Web SDK implementado en el sitio, deje este campo en blanco y la extensión [!DNL Data Connection] lo implementará por usted. |
| Eventos de tienda | Está activada de forma predeterminada siempre que el ID de organización y el ID de flujo de datos sean válidos. Los eventos de tienda recopilan datos de comportamiento anónimos de sus compradores a medida que navegan por el sitio. |
| Eventos de back office | Si se selecciona, la carga útil de evento contiene información anónima del estado del pedido, como si se ha realizado, cancelado, reembolsado o enviado un pedido. |
| ID de flujo de datos (sitio web) | ID que permite que los datos fluyan desde Adobe Experience Platform a otros productos Adobe DX. Este ID debe estar asociado a un sitio web específico dentro de la instancia de Adobe Commerce específica. Si especifica su propio Experience Platform Web SDK, no especifique ningún ID de flujo de datos en este campo. La extensión [!DNL Data Connection] utiliza el ID de flujo de datos asociado con ese SDK e ignora cualquier ID de flujo de datos especificado en este campo (si corresponde). |
| ID del conjunto de datos (sitio web) | ID del conjunto de datos que contiene los datos de Commerce. Este campo es obligatorio a menos que haya anulado la selección de las casillas de verificación de **Eventos de tienda** o **Eventos de oficina**. Además, si está utilizando su propio Experience Platform Web SDK y, por lo tanto, no especificó un ID de conjunto de datos, debe agregar el ID del conjunto de datos asociado a su conjunto de datos. De lo contrario, no podrá guardar este formulario. |

Después de la incorporación, los datos de la tienda comienzan a fluir al perímetro de Experience Platform. Los datos del back office tardan unos cinco minutos en aparecer en el perímetro. Las actualizaciones posteriores son visibles en el perímetro en función de la programación de cron.

### Envío de datos de perfil de cliente

Existen dos tipos de datos de perfil que puede enviar a Experience Platform: registros de perfil y eventos de perfil de series temporales.

Un registro de perfil contiene datos que se guardan cuando un comprador crea un perfil en su instancia de Commerce, como el nombre del comprador. Cuando el esquema y el conjunto de datos están [correctamente configurados](profile-data.md), se envía un registro de perfil a Experience Platform y se reenvía al servicio de segmentación y administración de perfiles de Adobe: [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=es).

Los eventos de perfil de series temporales contienen datos sobre la información de perfil del comprador; por ejemplo, si crean, editan o eliminan una cuenta del sitio. Cuando los datos de evento de perfil se envían a Experience Platform, residen en un conjunto de datos donde otros productos DX pueden utilizarlos.

1. Asegúrese de que ha [proporcionado](#add-service-account-and-credential-details) detalles de cuenta de servicio y credenciales.

1. Asegúrese de que ha especificado un esquema y un conjunto de datos para [ingesta de datos de registro de perfil](profile-data.md) y [ingesta de datos de evento de perfil de serie temporal](update-xdm.md#time-series-profile-event-data).

1. Active la casilla de verificación **Perfiles de cliente** si desea enviar datos de perfil a Experience Platform.

1. Escriba el **ID del conjunto de datos del perfil**.

   Los datos del registro de perfil deben utilizar un conjunto de datos diferente al que utiliza actualmente para los datos de evento de comportamiento y de back office.

1. Si no desea transmitir eventos de perfil a través del mismo ID de flujo de datos que esté usando para los datos de comportamiento y de back office, quite la marca de verificación de los **perfiles de clientes de Stream a través del mismo ID de flujo de datos** e introduzca el ID de flujo de datos que desee usar en su lugar.

Un registro de perfil puede tardar unos 10 minutos en estar disponible en Real-Time CDP. Los eventos de perfil comienzan a transmitirse inmediatamente.

>[!TIP]
>
>Si no ve datos de perfil en Experience Platform, consulte la [Base de conocimiento de Commerce](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-connection-customer-profiles-not-exported) para obtener sugerencias sobre solución de problemas.

#### Descripciones de campos

| Campo | Descripción |
|--- |--- |
| Perfiles de cliente | Seleccione esta casilla de verificación si desea recopilar y enviar registros de perfil de cliente. |
| ID de conjunto de datos de perfil | Un registro de perfil debe utilizar un conjunto de datos diferente al conjunto de datos utilizado para los eventos de comportamiento y back office. |
| Transmitir perfiles de clientes a través del mismo ID de flujo de datos | Decida si desea utilizar el mismo conjunto de datos que se utiliza actualmente para sus eventos de comportamiento y de back office o no. |
| Flujo de datos para perfiles de clientes | Especifique el conjunto de datos específico del registro de perfil del cliente. |

### Enviar datos de pedidos históricos

Adobe Commerce recopila hasta cinco años de [datos y estado de pedidos históricos](events-backoffice.md#back-office-events). Puede utilizar la extensión [!DNL Data Connection] para enviar esos datos históricos a Experience Platform a fin de enriquecer los perfiles de clientes y personalizar las experiencias de los clientes en función de esos pedidos anteriores. Los datos se almacenan en un conjunto de datos dentro de Experience Platform.

Aunque Commerce ya recopila los datos del historial de pedidos, debe completar varios pasos para enviar esos datos a Experience Platform.

Vea este vídeo para obtener más información sobre los pedidos históricos y, a continuación, complete los siguientes pasos para implementar la recopilación de pedidos históricos.

>[!VIDEO](https://video.tv.adobe.com/v/3450230?captions=spa)

#### Configuración del servicio de sincronización de pedidos

El servicio de sincronización de pedidos usa [Message Queue Framework](https://developer.adobe.com/commerce/php/development/components/message-queues/) y RabbitMQ. Después de completar estos pasos, los datos de estado de los pedidos se pueden sincronizar con SaaS, que es necesario antes de enviarlos a Experience Platform.

1. Asegúrese de que ha [proporcionado](#add-service-account-and-credential-details) detalles de cuenta de servicio y credenciales.

1. [Activar](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/rabbitmq.html?lang=es) RabbitMQ.

   >[!NOTE]
   >
   >RabbitMQ ya está configurado para las versiones 2.4.7 y posteriores de Commerce, pero debe habilitar a los consumidores.

1. Habilitar consumidores de cola de mensajes mediante el trabajo cron en `.magento.env.yaml` mediante la variable de entorno `CRON_CONSUMERS_RUNNER`.

   ```yaml
      stage:
        deploy:
          CRON_CONSUMERS_RUNNER:
            cron_run: true
   ```

   >[!NOTE]
   >
   >Consulte la [documentación de variables de implementación](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html?lang=es#cron_consumers_runner) para obtener más información sobre todas las opciones de configuración disponibles.

Con el servicio de sincronización de pedidos habilitado, puede especificar el intervalo de fechas de pedidos históricos en la página **[!UICONTROL [!DNL Data Connection]]**.

#### Especificar intervalo de fechas del historial de pedidos

Especifique el intervalo de fechas para los pedidos históricos que desea enviar a Experience Platform.

1. En el Administrador, vaya a **Sistema** > Servicios > **[!DNL Data Connection]**.

1. Seleccione la ficha **Historial de pedidos**.

   ![[!DNL Data Connection] historial de pedidos](./assets/epc-order-history.png){width="700" zoomable="yes"}

1. En **Sincronización del historial de pedidos**, la casilla de verificación **Copiar ID del conjunto de datos de la configuración** ya está habilitada. Esto garantiza que esté usando el mismo conjunto de datos especificado en la ficha **Configuración**.

1. En los campos **Desde** y **Hasta**, especifique el intervalo de fechas para los datos de pedidos históricos que desea enviar. No puede seleccionar un intervalo de fecha que exceda de cinco años.

1. Seleccione **[!UICONTROL Start Sync]** para almacenar en déclencheur el inicio de la sincronización. Los datos históricos de pedidos son datos por lotes, a diferencia de los datos de la tienda y el back office que transmiten los datos. Los datos por lotes tardan unos 45 minutos en llegar a Experience Platform.

##### Descripciones de campos

| Campo | Descripción |
|--- |--- |
| Copiar ID de conjunto de datos de configuración | Copia el ID del conjunto de datos que especificó en la ficha **Configuración**. |
| ID del conjunto de datos (sitio web) | ID del conjunto de datos que contiene los datos de Commerce. Este campo es obligatorio a menos que haya anulado la selección de las casillas de verificación de **Eventos de tienda** o **Eventos de oficina**. Además, si está utilizando su propio Experience Platform Web SDK y, por lo tanto, no especificó un ID de conjunto de datos, debe agregar el ID del conjunto de datos asociado a su conjunto de datos. De lo contrario, no podrá guardar este formulario. |
| Desde | Fecha a partir de la cual desea empezar a recopilar datos del historial de pedidos. |
| Hasta | Fecha a partir de la cual desea finalizar la recopilación de datos del historial de pedidos. |
| Iniciar sincronización | Inicia el proceso de sincronización de los datos del historial de pedidos con el perímetro de Experience Platform. Este botón está deshabilitado si el campo **[!UICONTROL Dataset ID]** está en blanco o si el ID del conjunto de datos no es válido. |

### Personalización de datos

En la ficha **Personalización de datos**, puede ver cualquier atributo personalizado configurado en [!DNL Commerce] y enviado a Experience Platform.

![[!DNL Data Connection] personalización de datos](./assets/epc-data-customization.png){width="700" zoomable="yes"}

>[!IMPORTANT]
>
>Asegúrese de que el ID de secuencia de datos que [especificó](#data-collection) en la ficha **Recopilación de datos** coincida con el ID vinculado al esquema para la ingesta de atributos personalizados.

Al crear atributos personalizados para pedidos y enviarlos a Experience Platform, los nombres de atributo en Commerce deben coincidir con los del esquema [!DNL Commerce] en Experience Platform. Si no coinciden, puede resultar difícil identificar las diferencias. Si tiene nombres que no coinciden, la tabla **Atributos de pedido personalizados** puede ayudarle a resolver el problema.

La tabla **Atributos de pedido personalizados** proporciona visibilidad sobre la configuración y asignación de atributos de pedido personalizados entre el back office [!DNL Commerce] y el esquema [!DNL Commerce] en Experience Platform. Esta tabla le permite ver los atributos personalizados de nivel de pedido y nivel de elemento de pedido en diferentes fuentes, lo que facilita la identificación de atributos que faltan o no se han alineado correctamente. También muestra los ID de conjuntos de datos para ayudar a diferenciar entre conjuntos de datos activos e históricos, ya que cada uno puede tener sus propios atributos personalizados.

Si no ve una marca de verificación verde junto a un nombre de atributo personalizado en la tabla, indica una discrepancia entre los nombres de atributo en los orígenes. Corrija el nombre del atributo en un origen y aparecerá una marca de verificación verde, que indica que los nombres ahora coinciden.

- Si el nombre del atributo se actualiza en el esquema de Experience Platform, debe guardar la configuración en la ficha **Personalización de datos** para almacenar en déclencheur el cambio de esquema de Experience Platform. Este cambio se reflejará en la tabla **Atributos de pedido personalizados** al hacer clic en el botón **[!UICONTROL Refresh]**.
- Si el nombre del atributo se actualiza en [!DNL Commerce], se debe generar un evento de pedido para actualizar el nombre en la tabla **Atributos de pedido personalizados**. El cambio se reflejará en unos 60 minutos.

Más información sobre cómo [configurar atributos personalizados](custom-attributes.md).

#### Descripciones de campos

| Campo | Descripción |
|--- |--- |
| Conjunto de datos | Muestra los conjuntos de datos que contienen los atributos personalizados. Los conjuntos de datos activos e históricos pueden tener sus propios atributos personalizados. |
| Adobe Commerce | Muestra cualquier atributo personalizado creado en el back office [!DNL Commerce]. |
| Experience Platform | Muestra cualquier atributo personalizado especificado en el esquema [!DNL Commerce] en Experience Platform. |
| Actualizar | Recupera cualquier nombre de atributo personalizado del esquema [!DNL Commerce] en Experience Platform. |

## Confirmar que se recopilan los datos del evento

Para confirmar que se están recopilando datos de tu tienda Commerce, usa [Adobe Experience Platform Debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html?lang=es) para examinar tu sitio Commerce. Después de confirmar que se están recopilando los datos, puede comprobar que los datos de evento de la tienda y del back office aparecen en el perímetro ejecutando una consulta que devuelva datos del [conjunto de datos que creó](overview.md#prerequisites).

1. Seleccione **Consultas** en el panel de navegación izquierdo de Experience Platform y haga clic en [!UICONTROL Create Query].

   ![Editor de consultas](assets/query-editor.png)

1. Cuando se abra el Editor de consultas, escriba una consulta que seleccione datos del conjunto de datos.

   ![Crear consulta](assets/create-query.png)

   Por ejemplo, la consulta podría tener el aspecto siguiente:

   ```sql
   SELECT * from `your_dataset_name` ORDER by TIMESTAMP DESC
   ```

1. Una vez ejecutada la consulta, los resultados se muestran en la ficha **Resultados**, junto a la ficha **Consola**. Esta vista muestra el resultado tabular de la consulta.

   ![Editor de consultas](assets/query-results.png)

En este ejemplo, verá datos de evento de [`commerce.productListAdds`](events.md#addtocart), [`commerce.productViews`](events.md#productpageview), [`web.webpagedetails.pageViews`](events.md#pageview), etc. Esta vista le permite comprobar que los datos de Commerce llegaron al perímetro de.

Si los resultados no son los esperados, abra el conjunto de datos y busque las importaciones de lotes fallidas. Obtenga más información sobre [solución de problemas con las importaciones por lotes](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/troubleshooting.html?lang=es).

### Verificar que los datos de perfil aparezcan en Experience Platform

Si no ve datos de perfil en Experience Platform, consulte la [Base de conocimiento de Commerce](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-connection-customer-profiles-not-exported) para obtener sugerencias sobre solución de problemas.

## Pasos siguientes

Cuando los datos de Commerce se envían al perímetro de Experience Platform, otros productos de Adobe Experience Cloud, como Adobe Journey Optimizer, pueden utilizar esos datos. Por ejemplo, puede configurar Journey Optimizer para que escuche ciertos eventos y, en función de esos datos de evento, almacenar en déclencheur un correo electrónico para un usuario primerizo o si hay un carro de compras abandonado. Aprenda a ampliar su plataforma de Commerce [creando recorridos de cliente](using-ajo.md) en Journey Optimizer.
