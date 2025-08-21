---
title: Eventos de comportamiento
description: Descubra qué datos captura cada evento de comportamiento.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: bcabccc9-8a2e-4045-9306-1d999bb75624
source-git-commit: 631dfacd26a333e70a70f354d191d256d90d946f
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# [!DNL Data Connection] eventos de comportamiento

A continuación se enumeran los eventos de comportamiento de Commerce disponibles al instalar la extensión [!DNL Data Connection]. Los datos que estos eventos recopilan se envían a Adobe Experience Platform. También puede crear [eventos personalizados](custom-events.md) para recopilar datos adicionales que no se proporcionen de forma predeterminada.

Además de los datos que recopilan los eventos siguientes, también recibirá [otros datos](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=es) proporcionados por Adobe Experience Platform Web SDK.

Los eventos de comportamiento recopilan datos de comportamiento anónimos de los compradores a medida que navegan por el sitio. Puede utilizar los datos que recopilan estos eventos para crear promociones y campañas dirigidas a un conjunto específico de compradores.

>[!NOTE]
>
>Todos los eventos de comportamiento incluyen el campo [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=es), que incluye la dirección de correo electrónico del comprador, cuando está disponible, y el ECID.

## Eventos de tienda

Los eventos de tienda capturan datos de las interacciones de los compradores en el sitio e incluyen eventos como `addToCart`, `pageView`, `createAccount`, `editAccount`, `startCheckout`, `completeCheckout`, `signIn`, `signOut`, etc. Los eventos de tienda solo se aplican a productos simples y configurables.

Consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) para obtener más información sobre los eventos de tienda.

## Eventos de perfil de cliente

Los eventos de perfil capturados desde la tienda incluyen información de la cuenta, como `signIn`, `signOut`, `createAccount` y `editAccount`. Estos datos se utilizan para rellenar los detalles clave del cliente que se necesitan para definir mejor los segmentos o ejecutar campañas de marketing, como enviar ofertas de descuento de suscripción, confirmaciones de cambio de cuenta, etc.

Consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) para obtener más información sobre los eventos de perfil del cliente.

## Buscar eventos

Los eventos de búsqueda proporcionan datos relevantes para la intención del comprador. Insight en la intención de un comprador ayuda a los comerciantes a ver cómo buscan los compradores los artículos, en qué hacen clic y, finalmente, cómo compran o abandonan. Un ejemplo de cómo puede utilizar estos datos es si desea dirigirse a compradores existentes que buscan su producto principal, pero nunca compran el producto. Debe instalar la extensión [[!DNL Live Search]](../live-search/install.md) para tener acceso a estos eventos.

Utilice los campos `searchRequest.id` y `searchResponse.id` encontrados en los eventos `searchRequestSent` y `searchResponseReceived` para hacer referencia a una solicitud de búsqueda con la respuesta de búsqueda correspondiente.

Consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) para obtener más información sobre los eventos de búsqueda.

## Eventos B2B

![B2B para Adobe Commerce](../assets/b2b.svg) Para los comerciantes B2B, debe [instalar](install.md#install-the-b2b-extension) la extensión `experience-platform-connector-b2b` para acceder a estos eventos.

Los eventos B2B contienen [información de lista de solicitudes](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html?lang=es), como si se hubiera creado, agregado o eliminado una lista de solicitudes de. Mediante el seguimiento de eventos específicos de las listas de solicitudes, puede ver los productos que sus clientes compran con frecuencia y crear campañas basadas en esos datos.

Consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) para obtener más información sobre los eventos B2B.
