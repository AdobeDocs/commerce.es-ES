---
title: Claves de acceso restringido
description: Obtenga información sobre cómo crear, asignar y rotar claves de acceso restringido para proteger vistas de catálogo en  [!DNL Adobe Commerce Optimizer] con autenticación de token firmado.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e0eb8757-182f-49f3-94a4-1587d16f5094
nudge: true
source-git-commit: 688bc6e28a4c5a94b1fe55c84f7c05401dd651bc
workflow-type: tm+mt
source-wordcount: 791
ht-degree: 0%

---

# Claves de acceso restringido

Las claves de acceso restringidas permiten que las aplicaciones cliente autorizadas tengan acceso a una [vista de catálogo privado](catalog-view.md); solo las solicitudes que lleven un token firmado válido de una clave asignada pueden recuperar datos de catálogo. Todas las demás solicitudes son denegadas, incluidas las de compradores anónimos, compradores a los que no se les ha dado acceso explícito a esta vista de catálogo y scripts que sondean la API.

## Casos de uso de claves de acceso restringido

En [!DNL Adobe Commerce Optimizer], **[!UICONTROL Price Book ID]** determina los precios que ve una solicitud; determina los precios, no quién puede realizar la solicitud. Cualquier cliente que conozca el ID de la vista de catálogo y el ID del libro de precios puede recuperar esos datos a través de la API de comercialización. Las claves de acceso restringidas agregan un control independiente y complementario: tienen el alcance de quién puede acceder a una vista de catálogo en absoluto, independientemente de qué libro de precios se aplique.

Las claves de acceso restringido se utilizan normalmente para:

- **Asignación de precios B2B basada en contrato**: restringe una vista de catálogo vinculada a un libro de precios negociado para que sólo el comprador al que se aplica pueda consultarla. Otras organizaciones compradoras y el público no pueden.
- **Portales de socios y revendedores**: limite un subconjunto del catálogo a los socios aprobados que se integren directamente con la API de comercialización.
- **Previsualizaciones previas al lanzamiento**: permita que un sistema interno o de socio de confianza obtenga una vista previa de los próximos productos antes de que sean visibles para el público.

>[!IMPORTANT]
>
>Actualmente, la generación de claves, la firma de tokens y la rotación están administradas por completo por la aplicación cliente back-end que autentica a los compradores. [!DNL Adobe Commerce Optimizer] no genera ni gira estas claves en su nombre.

## Funcionamiento de las claves de acceso restringido

Una clave de acceso restringido es el componente público de un par de claves RSA. La aplicación cliente genera y utiliza esta clave para demostrar que está autorizado a leer una vista de catálogo privado. En este contexto, &quot;aplicación cliente&quot; significa el sistema backend que autentica a los compradores (por ejemplo, lógica personalizada en [!DNL Adobe Commerce] o un back-end de terceros) en vez del front-end de la tienda en sí.

Los siguientes pasos describen cómo un par de claves y un token firmado pasan de la creación a la validación:

1. La aplicación cliente genera un par de claves RSA y mantiene la clave privada.
1. La clave **public** se registra en [!DNL Commerce Optimizer] como clave de acceso restringido.
1. La aplicación cliente firma un token web JSON (JWT) con la clave privada y lo incluye con cada solicitud a una vista de catálogo privado.
1. [!DNL Commerce Optimizer] valida la firma del token con la clave pública registrada y, si es válida, devuelve los datos del catálogo solicitado.

## Creación de una clave de acceso restringido

Para la prueba inicial de vistas de catálogo privado, genere un par de claves con una herramienta como [!DNL OpenSSL]. Mantenga la clave privada en secreto: solo la clave pública se cargará en [!DNL Commerce Optimizer].

```bash
openssl genrsa -out private-key.pem 2048
openssl rsa -in private-key.pem -pubout -out public-key.pem
```

El tamaño de la clave debe estar entre 2048 y 8192 bits. `public-key.pem` contiene el valor que pega en el campo **[!UICONTROL Public key]** siguiente.

## Agregar una clave de acceso restringido a [!DNL Commerce Optimizer]

1. En el menú de la izquierda de [!DNL Adobe Commerce Optimizer Studio], vaya a **[!UICONTROL Store setup]** y haga clic en **[!UICONTROL Restricted access keys]**.

   ![Lista de claves de acceso restringido, con el botón Agregar clave de acceso restringido](../assets/restricted-access-keys.png){width="70%" zoomable="yes"}

1. Haga clic en **[!UICONTROL Add Restricted Access Key]**.

1. Introduzca los detalles de la clave:

   ![Agregar formulario con clave de acceso restringido, con los campos Título, Fecha de caducidad y Clave pública](../assets/restricted-access-keys-add.png){width="70%" zoomable="yes"}

   - **[!UICONTROL Title]**: una etiqueta para identificar la clave, que se muestra en la lista de claves y en el selector de claves de la vista de catálogo, por ejemplo `ACME Corp wholesale portal — Tier 1 pricing`.
   - **[!UICONTROL Expiration date]**: fecha y hora (UTC) tras las cuales la clave deja de respetarse, incluso para un token que aún no ha caducado.
   - **[!UICONTROL Public key]**: la clave pública RSA con codificación PEM en el formato de información de clave pública del sujeto (SPKI), incluidos los marcadores `-----BEGIN PUBLIC KEY-----` y `-----END PUBLIC KEY-----`. Debe ser único en todo el entorno.

1. Haga clic en **[!UICONTROL Save]**.

Las claves son inmutables después de la creación. Para cambiar cualquier valor, elimine la clave y cree uno nuevo. Ver [Rotar una clave](#rotate-a-key) para hacerlo sin interrumpir el acceso.

## Asignación de una clave a una vista de catálogo

Una clave de acceso restringido solo restringe el acceso una vez que se asigna a una vista de catálogo con **[!UICONTROL Catalog Protection]** habilitado. Consulte [Proteger una vista de catálogo](private-catalog-view.md#protect-a-catalog-view) para ver los pasos de configuración.

## Eliminación de una clave

1. En la página **[!UICONTROL Restricted access keys]**, busque la clave que desea quitar y haga clic en **[!UICONTROL Delete]**.

   Si la clave se asigna a una o varias vistas de catálogo, una advertencia explica que las aplicaciones cliente que dependen de esa clave pierden el acceso. Las vistas del catálogo en sí permanecen protegidas y no se puede acceder a ellas públicamente.

1. Confirme la eliminación.

## Rotar una clave

Para girar una clave sin interrumpir el acceso, tenga en cuenta que una vista de catálogo puede tener hasta tres claves asignadas a la vez:

1. Genere un nuevo par de claves y añada la nueva clave pública como nueva clave de acceso restringido.
1. Asigne la nueva clave a la vista de catálogo junto con la clave existente.
1. Inicie la firma de nuevos tokens con la nueva clave privada para completar la sustitución de claves.
1. Una vez que todas las aplicaciones cliente estén confirmadas en la nueva clave, elimine la clave antigua.

## Límites

Ver [límites de directivas y vistas de catálogo](../boundaries-limits.md#catalog-views-and-policies).

## Más parecido a esto

- [Vistas de catálogo privado](private-catalog-view.md): aprenda a proteger una vista de catálogo con claves de acceso restringido.

