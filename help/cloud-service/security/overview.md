---
title: Información general de seguridad
description: Obtenga información acerca de las funciones de seguridad de Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: feb48068137c6a63e6594167fe969c3aa4b044c4
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---


# Información general de seguridad

[!DNL Adobe Commerce as a Cloud Service] está diseñado con seguridad en su núcleo, ofreciendo una plataforma de comercio moderna y nativa de SaaS que ofrece protección de nivel empresarial, resiliencia operativa y tranquilidad para empresas de todos los tamaños.

A diferencia de los modelos tradicionales PaaS, el modelo SaaS elimina la carga de aplicar parches manualmente, realizar el mantenimiento de la infraestructura y realizar ciclos de actualización. La seguridad está integrada en todos los niveles de la plataforma, desde la infraestructura administrada por Adobe y las canalizaciones de implementación automatizadas hasta la administración de identidades y acceso a través de [!DNL Adobe IMS].

[!DNL Adobe Commerce as a Cloud Service] aprovecha el marco de cumplimiento y seguridad global de Adobe, lo que garantiza la alineación con los estándares del sector, como ISO 27001, SOC 2 y RGPD. Los clientes se benefician de un [modelo de responsabilidad compartida](./shared-responsibility.md) que define claramente la función de Adobe en la protección de la plataforma y la función del cliente en la administración de datos y acceso.

Con protecciones integradas como el firewall de aplicaciones web (WAF), la mitigación de DDoS, el aprovisionamiento seguro y el análisis continuo de vulnerabilidades, [!DNL Adobe Commerce as a Cloud Service] permite a las empresas innovar más rápido sin poner en riesgo la seguridad.

Este documento describe la arquitectura de seguridad, las protecciones operativas y la postura de cumplimiento de [!DNL Adobe Commerce as a Cloud Service], lo que permite a los clientes tomar decisiones informadas y escalar con confianza sus operaciones de comercio digital.

## Red de entrega de contenido (CDN) y cortafuegos de aplicaciones web (WAF)

### CDN de tienda

Los comerciantes pueden optar por implementar una CDN administrada por Adobe o comprar su propia solución de CDN para proteger su tienda basada en Commerce.

>[!IMPORTANT]
>
>Si los clientes eligen implementar CDN administrada por Adobe, no pueden configurar las reglas de CDN. Los clientes pueden configurar reglas de almacenamiento en caché personalizadas o reglas de WAF cuando traen su propia CDN para proteger sus tiendas.

### [!DNL API Mesh for Adobe Developer App Builder] CDN

La capa CDN de [!DNL API Mesh] termina TLS, ejecuta la puerta de enlace de GraphQL como Workers, proporciona almacenamiento en caché perimetral global y DDoS/WAF automático, y expone `edge‑graph.adobe.io`/`edge‑sandbox‑graph.adobe.io` como extremos de malla pública; los clientes pueden agregar su propia CDN delante, pero la CDN de [!DNL API Mesh] se corrige y administra mediante Adobe y los clientes no pueden configurar sus propias reglas de WAF.

Para obtener más información sobre las características de seguridad de [!DNL API Mesh], consulte la [documentación de API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/security/){target="_blank"}.

### CDN back-end

Una CDN integrada protege a [!DNL Adobe Commerce as a Cloud Service].

Debido a la arquitectura de [!DNL Adobe Commerce as a Cloud Service], cuando un comerciante aprovisiona una instancia en una celda compuesta, como `na1`, `eu1`, `au1` u otras regiones geográficas, se exponen tres superficies públicas:

| Superficie | Ejemplo de patrón de URL |
| --- | --- |
| IU de administración | `https://<region>.admin.commerce.adobe.com/<tenant-id>/admin/` |
| API DE REST | `https://<region>.api.commerce.adobe.com/<tenant-id>/<endpoint>` |
| API de GraphQL | `https://na1.api.commerce.adobe.com/<tenant_id>/graphql/` |

[!DNL Adobe Commerce as a Cloud Service] usa una red de distribución de contenido (CDN) y WAF combinadas:

- **WAF**: protección del firewall de aplicaciones web para todas las [!DNL Adobe Commerce as a Cloud Service] superficies públicas.
- **CDN**: almacenamiento en caché de Edge para recursos estáticos y respuestas de GraphQL almacenables en caché.

La plataforma [!DNL Adobe Commerce as a Cloud Service] administra WAF y CDN, y los clientes no pueden configurarlos.

### Protección DDoS

La CDN y WAF integrados proporcionan protección DDoS en la capa de red y en la capa HTTP. [!DNL Adobe Commerce as a Cloud Service] no expone esos registros de WAF o DDoS directamente a los comerciantes.

## Almacenamiento y cifrado de datos

Si los datos se almacenan en [!DNL App Builder], un comerciante puede consultar las [!DNL App Builder] [opciones de almacenamiento](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/). [!DNL App Builder] aplica el aislamiento de inquilinos y el acceso a los datos almacenados en estos servicios está restringido al espacio de nombres de tiempo de ejecución en el que se ejecuta la acción. No hay cifrado de datos en el almacenamiento.

Al usar [!DNL API Mesh], los secretos deben almacenarse en el archivo `secrets.yaml` de la configuración de mesh. [!DNL API Mesh] cifra estos secretos usando el cifrado AES-256 ([https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/](https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/)).

Cualquier dato almacenado en [!DNL Adobe Commerce as a Cloud Service] se cifra en reposo usando el cifrado AES de 256 bits y todos los datos se cifran a través de HTTPS usando TLS 1.2 o superior en tránsito.
