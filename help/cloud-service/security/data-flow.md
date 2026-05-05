---
title: Arquitectura de seguridad y flujo de datos
description: Obtenga información sobre la arquitectura de seguridad y el flujo de datos para Adobe Commerce as a Cloud Service.
role: Admin, Architect, Leader
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 0343c4f3ecc182145a97e08eca2790bd1512aa27
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---


# Arquitectura de seguridad y flujo de datos

El siguiente ejemplo ilustra cómo los datos fluyen normalmente en [!DNL Adobe Commerce as a Cloud Service]:

![Diagrama del flujo de datos de Adobe Commerce as a Cloud Service](../assets/data-flow-1.png)

## Narrativa del flujo de datos

**Paso 1**: El comprador escribe la dirección URL de la tienda del comerciante en su explorador, que envía la dirección URL a la red de distribución de contenido (CDN externa) de la Tienda Commerce.

**Paso 2**: si la dirección URL del sitio está en la caché, la CDN de Storefront la devuelve al comprador. Si aún no se ha almacenado en caché, lo que podría suceder si esta es la primera solicitud de un recurso, la CDN externa reenvía la solicitud del comprador a la CDN interna y almacena en caché la respuesta de las solicitudes posteriores.

**Paso 2a**: si la solicitud es para imágenes o vídeos, se envía a [!DNL Product Visuals] para su cumplimiento y se devuelve a la tienda.

**Paso 3**: Si la dirección URL del sitio se almacena en caché en la CDN interna, se devuelve desde esa caché. Si no es así, se envía a [!DNL API Mesh] y la respuesta se almacena en caché para solicitudes posteriores.

**Paso 4**: [!DNL API Mesh] actúa como la capa de orquestación y determina si se debe enviar la solicitud a [!DNL Adobe Commerce as a Cloud Service] o a un sistema de terceros para cumplir con la solicitud.

>[!NOTE]
>
>[!DNL API Mesh] solo enviará solicitudes a sistemas de terceros si ha personalizado la configuración de malla para hacerlo.

**Paso 5**: las solicitudes enviadas a [!DNL Adobe Commerce as a Cloud Service] pasan a través de un firewall de aplicaciones web (WAF) que bloquea las solicitudes sospechosas o malintencionadas. Si la dirección URL solicitada se almacena en caché en la CDN [!DNL Commerce], se enviará desde esa caché. Si no se almacena en caché, se devuelve desde uno o más microservicios de [!DNL Adobe Commerce as a Cloud Service] (por ejemplo, foundation, search y recommendations) y luego se almacena en caché para solicitudes futuras.

**Paso 5a**: Si la solicitud se envía a un sistema de terceros, la respuesta se devolverá a [!DNL API Mesh].

**Paso 5b**: Si la solicitud es para procesamiento de pagos, el proveedor de pagos procesa un iframe en la tienda para que el comprador introduzca de forma segura la información de la tarjeta de crédito y complete la transacción de pago.

**Paso 6**: Una vez que [!DNL API Mesh] recibe las respuestas de [!DNL Adobe Commerce as a Cloud Service] o de servicios de terceros, se unen en un gráfico unificado y se devuelven a [!DNL Commerce Storefront] para servir la solicitud del comprador.
