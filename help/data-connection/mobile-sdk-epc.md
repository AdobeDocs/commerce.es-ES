---
title: Integración de Adobe Experience Platform Mobile SDK con Commerce
description: Aprenda a utilizar Adobe Experience Platform Mobile SDK con su tienda de Commerce personalizada o sin encabezado.
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Integración de Adobe Experience Platform Mobile SDK con Commerce

>[!IMPORTANT]
>
>Adobe Experience Platform Mobile SDK para iOS es compatible con iOS 11 o versiones posteriores.

La integración de [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/) con la aplicación móvil de Commerce permite a los comerciantes enviar [datos de evento](events.md) de Commerce al perímetro de Experience Platform.

Cuando los datos de evento de Commerce están disponibles en el perímetro, otras aplicaciones de Adobe Experience Cloud pueden acceder a ellos. Por ejemplo, puede usar los datos para crear audiencias en Real-Time CDP y luego [usar esas audiencias](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=es) para personalizar su aplicación móvil de Commerce.

## Configuración

Para empezar a utilizar Adobe Experience Platform Mobile SDK con Commerce, instale y configure SDK en Experience Platform. A continuación, finalice la configuración en Commerce.

### Experience Platform

1. Obtenga información acerca de las funcionalidades de la aplicación móvil al revisar el tutorial de [Adobe Experience Cloud en aplicaciones móviles](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html?lang=es).

1. [Instalar y configurar](https://developer.adobe.com/client-sdks/documentation/getting-started/) SDK en Experience Platform.

   >[!NOTE]
   >
   >El esquema que cree y configure en Experience Platform es el mismo que utiliza en el código de la aplicación en su aplicación móvil de Commerce.

### Commerce

Una vez completada la configuración de SDK para Experience Platform, añada la configuración de SDK a Commerce.

1. Para enviar datos de evento de Commerce a Experience Platform a través de SDK, debe proporcionar un esquema XDM en el código de aplicación. Este esquema debe coincidir con el esquema [configurado](https://developer.adobe.com/client-sdks/home/getting-started/set-up-schemas-and-datasets/) para SDK en Experience Platform.

   El siguiente ejemplo muestra cómo realizar un seguimiento del evento `web.webpagedetails.pageViews` y establecer `identityMap` mediante el campo de correo electrónico.

   ```swift
   let stateName = "luma: content: ios: us: en: home"
   var xdmData: [String: Any] = [
       "eventType": "web.webpagedetails.pageViews",
       "web": [
           "webPageDetails": [
               "pageViews": [
                   "value": 1
               ],
               "name": "Home page"
           ]
       ]
   ]
   
   let experienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: experienceEvent)
   
   // Adobe Experience Platform - Update Identity
   
   let emailLabel = "mobileuser@example.com"
   
   let identityMap: IdentityMap = IdentityMap()
   identityMap.add(item: IdentityItem(id: emailLabel), withNamespace: "Email")
   Identity.updateIdentities(with: identityMap)
   ```

1. Conéctese al entorno de Commerce Cloud.

   En la configuración de compilación del proyecto, agregue la dirección URL al extremo de Commerce GraphQL. Por ejemplo:

   - Depuración: http://_debug_.commerce.site.cloud/graphql/
   - Versión: http://_release_.commerce.cloud/graphql/

1. Para recuperar datos de los extremos de Commerce GraphQL, genere primero los archivos y directorios necesarios en su proyecto mediante [Apollo Code Generator](https://www.apollographql.com/docs/ios/).

   1. Desde el directorio de tu proyecto, [instala](https://www.apollographql.com/docs/ios/get-started#1-install-the-apollo-frameworks) Apollo iOS.

   1. [Inicializar](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#initialize) la CLI de Apollo Codegen.

      Esto crea un archivo de `apollo-codegen-configuration.json`.

   1. Genere los archivos y directorios GraphQL necesarios en su proyecto reemplazando el contenido del archivo `apollo-codegen-configuration.json` por el siguiente:

      ```json
      {
      "schemaName" : "MagentoAPI",
      "input" : {
          "operationSearchPaths" : [
          "**/*.graphql"
          ],
          "schemaSearchPaths" : [
          "**/*.graphqls"
          ]
      },
      "output" : {
          "testMocks" : {
          "none" : {
          }
          },
          "schemaTypes" : {
          "path" : "../MagentoAPI",
          "moduleType" : {
              "swiftPackageManager" : {
              }
          }
          },
          "operations" : {
          "inSchemaModule" : {
          }
          }
      },
      "schemaDownloadConfiguration": {
          "downloadMethod": {
              "introspection": {
                  "endpointURL": "http://magento24.com/graphql/",
                  "httpMethod": {
                      "POST": {}
                  },
                  "includeDeprecatedInputValues": false,
                  "outputFormat": "SDL"
              }
          },
          "downloadTimeout": 60,
          "headers": [],
          "outputPath": "magento.graphqls"
      }
      }
      ```

   1. [Recuperar](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#fetch-schema) el esquema de Commerce GraphQL.

      Asegúrese de que la ruta de acceso es al archivo `./apollo-codegen-config.json`, que contiene la referencia al esquema de Commerce GraphQL.

   1. [Generar](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#generate) el código fuente.

      Asegúrese de que la ruta de acceso es al archivo `./apollo-codegen-config.json`, que contiene la información de configuración para generar los archivos y directorios necesarios.

   1. En la carpeta **GraphQLGenerated** recién creada, agregue o edite tipos de GraphQL. Por ejemplo, puede agregar un tipo `DynamicBlocks.graphql` con el siguiente contenido:

      ```graphql
      query dynamicBlocks($input: DynamicBlocksFilterInput){
          dynamicBlocks(input: $input)
          {
              items {
                  content {
                      html
                  }
              }
          }
      }
      ```

   Ya ha integrado Adobe Experience Platform Mobile SDK con su aplicación móvil de Commerce. Los datos de evento fluyen desde la aplicación al perímetro de Experience Platform.

## Cómo distinguir los eventos de Commerce generados desde aplicaciones móviles

Todos [los eventos](events.md) contienen un campo llamado `channel`. El campo `channel` contiene `channel._id` y `channel._type`, que para una tienda de Luma tienen valores de área de nombres de `"https://ns.adobe.com/xdm/channels/web"` y `"https://ns.adobe.com/xdm/channel-types/web"` respectivamente. Sin embargo, para una tienda móvil, los valores de área de nombres son `"https://ns.adobe.com/xdm/channels/mobile-app"` y `"https://ns.adobe.com/xdm/channel-types/mobile"` respectivamente.

## Pasos siguientes

Para obtener información sobre cómo recuperar audiencias de Real-Time CDP desde la aplicación móvil de Commerce con el fin de informar las reglas de precios del carro de compras, los bloques dinámicos y las reglas de productos relacionadas, consulta [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=es#retrieve-audiences-using-the-adobe-experience-platform-mobile-sdk).
