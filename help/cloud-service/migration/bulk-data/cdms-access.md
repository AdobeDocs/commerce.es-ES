---
title: Verificar acceso al servicio de migración
description: Obtenga información sobre cómo comprobar el acceso completo a la API del servicio de migración de datos de Commerce, confirmando la accesibilidad de la red, la autenticación IMS y la autorización de inquilinos.
feature: Cloud
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:18:53.554Z'
TQID: 'https://experienceleague.adobe.com/csDq2Bbha2IieqxsDDG0iS1IHhAJ02fD-cwd8KFIsSk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 452
ht-degree: 1%

---

# Verificar acceso al servicio de migración

{{bulk-data-early-access}}

Utilice esta guía para verificar el acceso completo a la API del servicio de migración de datos (CDMS) de Commerce desde su entorno. Una llamada correcta valida simultáneamente la accesibilidad de la red desde las direcciones IP de salida (inclusión en la lista de permitidos IP), la autenticación IMS y la autorización de inquilinos.

Complete esta guía después de finalizar todos los elementos de la [lista de comprobación de preparación para clientes](readiness-checklist.md) y antes de ejecutar la migración descrita en la [guía de migración](migration-guide.md).

## Requisitos previos

- Credencial de servidor a servidor OAuth 2.0 (ID de cliente y secreto de cliente) creada en [Adobe Developer Console](https://developer.adobe.com/console/).
- Su ID de organización de IMS con el formato `<org>@AdobeOrg`. La organización debe ser propietaria del inquilino de destino.
- El destino `tenantId`, un identificador de inquilino de IMS alfanumérico de 22 caracteres.
- Direcciones IP de salida enviadas a y incluidas en la lista de permitidos por Adobe para la puerta de enlace de CDMS. Si no está seguro de las direcciones IP o de su estado, póngase en contacto con el equipo de Adobe.
- El host de servicio específico de la región de [Service hospeda por entorno y región](#service-hosts-by-environment-and-region).

## Generación de un token de acceso de IMS

Genere un token de acceso usando sus credenciales de servidor a servidor OAuth 2.0 con la concesión `client_credentials`. El host de IMS en este paso es el mismo para todas las regiones de datos. Solo cambia el host de CDMS por región.

```bash
curl -X POST "https://ims-na1.adobelogin.com/ims/token/v3" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "x-org-id:<your-org-id>@AdobeOrg" \
  -d "grant_type=client_credentials" \
  -d "client_id=<your-ims-client-id>" \
  -d "client_secret=<your-ims-client-secret>" \
  -d "scope=AdobeID,openid,read_organizations,additional_info.projectedProductContext,additional_info.roles,adobeio_api,read_client_secret,manage_client_secrets"
```

## Llame a la API List Migrations

La siguiente solicitud recupera la lista de migraciones para el inquilino y requiere el token de acceso del paso anterior. Seleccione el host de su región en la tabla [Hosts de servicio por entorno y región](#service-hosts-by-environment-and-region). El indicador `-i` imprime la línea de estado HTTP y los encabezados de respuesta para que pueda confirmar el resultado.

```bash
curl -i "https://<host>/<tenantId>/v1/migrations" \
  -H "Authorization: Bearer <your IMS access token>"
```

## Interpretación de la respuesta

| código HTTP | Significado | Cuerpo de respuesta de ejemplo |
| --- | --- | --- |
| 200 | Correcto. Se pasó la conectividad, la autenticación y la autorización del inquilino. El cuerpo de respuesta contiene la lista de migraciones para el inquilino. | `{"migrations":[...]}` |
| 401 | Falta el token de portador o no es válido, se rechazó antes de llegar al servicio. [Volver a generar el token](#generate-an-ims-access-token). | Varía (generado por puerta de enlace) |
| 403 | El usuario autenticado no tiene permisos de migración para este usuario. | `{"error":"access_denied","message":"You do not have permission to access this tenant"}` |
| 500 | Error interno del servidor. | `{"error":{"message":"Internal Server Error","status":500}}` |

>[!NOTE]
>
>Si se agota el tiempo de espera de la solicitud o se rechaza la conexión y no se devuelve ningún estado HTTP, es probable que la IP de salida no esté incluida en la lista de permitidos o que esté utilizando un host incorrecto. Confirme el host de región en la siguiente tabla y sus IP incluidas en la lista de permitidos.

## Hosts de servicio por entorno y región

| Región o entorno | Host |
| --- | --- |
| Zona protegida o preproducción | `https://na1-sandbox.api.commerce.adobe.com` |
| América del Norte | `https://na1.api.commerce.adobe.com` |
| Europa | `https://eu1.api.commerce.adobe.com` |
| India | `https://in1.api.commerce.adobe.com` |
| RU | `https://uk1.api.commerce.adobe.com` |
| Australia y Nueva Zelanda | `https://au1.api.commerce.adobe.com` |

## Pasos siguientes

Después de confirmar el acceso, continúe con la [guía de migración](migration-guide.md) para comenzar la configuración del entorno y la ejecución de la migración.
