---
title: Cómo  [!DNL Commerce] Servicios administra las solicitudes de privacidad
description: Descubra cómo  [!DNL Commerce] services administra las solicitudes de acceso y eliminación de datos.
role: Admin, Leader
feature: Security, Compliance
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Solicitudes de privacidad

Adobe Experience Platform Privacy Service proporciona una API de RESTful y una interfaz de usuario para ayudarle a administrar las solicitudes de datos de los clientes. Con Privacy Service, puede enviar solicitudes para acceder a datos personales de clientes y eliminarlos de aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las regulaciones de privacidad legales y organizativas.

Para obtener más información sobre Privacy Service y cómo crear y administrar solicitudes de privacidad, consulte la documentación de Adobe Experience Platform:

* [Información general de Privacy Service](https://experienceleague.adobe.com/es/docs/experience-platform/privacy/home)
* [Administración de trabajos de privacidad en la IU de Privacy Service](https://experienceleague.adobe.com/es/docs/experience-platform/privacy/ui/user-guide)

## Administración de solicitudes de privacidad de datos individuales

Puede enviar solicitudes individuales para acceder a los datos de consumidores y eliminarlos de [!DNL Commerce] de dos maneras:

* A través de la **IU de Privacy Service**. Consulte la documentación [aquí](https://experienceleague.adobe.com/es/docs/experience-platform/privacy/ui/user-guide#_blank).
* Mediante la **API de Privacy Service**. Consulte la documentación [aquí](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#_blank) y la información de la API [aquí](https://developer.adobe.com/experience-platform-apis/#_blank).

Privacy Service admite dos tipos de solicitudes: **acceso a datos** y **eliminación de datos**.

>[!NOTE]
>
>Este artículo se centra en realizar solicitudes de privacidad para [!DNL Commerce]. Si planea realizar solicitudes de privacidad para [el lago de datos de Platform](https://experienceleague.adobe.com/es/docs/experience-platform/catalog/privacy), [el perfil del cliente en tiempo real](https://experienceleague.adobe.com/es/docs/experience-platform/profile/privacy) o [el servicio de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/privacy), consulte sus respectivas guías de usuario. Tenga en cuenta que las solicitudes de eliminación y acceso deben realizarse en cada sistema de forma individual, ya que una solicitud de privacidad a Commerce no elimina los datos de todos estos sistemas.

## Acceso a datos

Para **solicitudes de acceso**, especifique &quot;Commerce (Personalization)&quot; desde la interfaz de usuario (o `commerceMarketingData` como código de producto en la API).

## Eliminación de datos

Para las solicitudes de eliminación, Privacy Service elimina los datos de [!DNL Commerce] almacenados en los servicios SaaS de Commerce con fines de marketing, lo que significa que los perfiles y los pedidos de los interesados ya no se envían a las aplicaciones de marketing de Adobe para su uso en campañas y recorridos de clientes. Sin embargo, Privacy Service no elimina datos en la aplicación [!DNL Commerce], ya que podrían ser necesarios para las necesidades transaccionales de los comerciantes. Los comerciantes son responsables de cualquier solicitud de eliminación/acceso de datos en la aplicación [!DNL Commerce]. Consulte [Modelo operativo y de seguridad de responsabilidad compartida](https://experienceleague.adobe.com/es/docs/commerce-operations/security-and-compliance/shared-responsibility) para obtener más información.

[!DNL Commerce] notificará a los comerciantes sobre las solicitudes de eliminación enviándoles información sobre los interesados que soliciten la eliminación de determinados datos.

## Creación de solicitudes de acceso y eliminación

### Requisitos previos

Para realizar solicitudes de acceso y eliminación de datos para Adobe [!DNL Commerce], debe contar con:

* un ID de organización de IMS
* un identificador de identidad de la persona sobre la que desea actuar y las áreas de nombres correspondientes. Para obtener más información sobre áreas de nombres de identidad en Adobe [!DNL Commerce] y Experience Platform, vea la [descripción general del área de nombres de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces).

### Ejemplo de acceso de solicitud/eliminación de RGPD:

Para **solicitudes de acceso**, especifique &quot;Commerce (Personalization)&quot; desde la interfaz de usuario (o &quot;commerceMarketingData&quot; como código de producto en la API).

Para **eliminar solicitudes**, asegúrese de que la casilla &quot;Commerce (Personalization)&quot; esté habilitada. Además, si los datos de perfil de cliente y pedido ya se han enviado de [!DNL Commerce] a Adobe Experience Platform, debe enviar solicitudes de eliminación a los siguientes servicios descendentes.

* Perfil (código de producto: &quot;profileService&quot;)
* Lago de datos de AEP (código de producto: &quot;AdobeCloudPlatform&quot;)
* Identidad (código de producto: &quot;identidad&quot;)

Para enviar solicitudes de acceso y eliminación a través de la API de privacidad, debe autenticar y administrar permisos para Privacy Service:

* [Autenticar y acceder a la API de Privacy Service](https://experienceleague.adobe.com/es/docs/experience-platform/privacy/api/getting-started)
* [Administrar permisos para Privacy Service](https://experienceleague.adobe.com/es/docs/experience-platform/privacy/permissions)

**Encabezados obligatorios**

```bash
curl --location --request POST 'https://platform.adobe.io/data/core/privacy/jobs' \
--header 'Content-Type: application/json' \
--header 'x-api-key: {{CLIENT_ID}}' \
--header 'x-gw-ims-org-id: {{IMS_ORGID}}' \
--header 'Authorization: Bearer {{ACCESS_TOKEN}}' \
```

**Solicitud**

```json
{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{{IMS_ORGID}}"
      }
    ],
    "users": [
      {
        "key": "sampleUserKey1",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@sample.com",
            "type": "standard"
          }
        ]
      },
      {
        "key": "sampleUserKey2",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@sample.com",
            "type": "standard"
          }
        ]
      }
    ],
    "include": ["commerceMarketingData"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "gdpr"
}
```

**Respuesta**

```json
{
    "requestId": "17284033173196154RX-223",
    "totalRecords": 3,
    "jobs": [
        {
            "jobId": "a52ca032-858e-11ef-bbb4-27391388a0a6",
            "customer": {
                "user": {
                    "key": "sampleUserKey1",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "dsmith@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca034-858e-11ef-bbb4-d5d952d69769",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "delete"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca033-858e-11ef-bbb4-8361a5022341",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        }
    ]
}
```
