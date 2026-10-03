---
title: Claves de acceso restringido
description: Descubra cómo las claves de acceso restringido protegen las vistas de catálogo en [!DNL Adobe Commerce Optimizer], creadas automáticamente para catálogos compartidos B2B o administradas manualmente.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y a [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
nudge: true
source-git-commit: f93bd673624c58050696da772ce733874ce594e5
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%
---
# Claves de acceso restringido

Las claves de acceso restringidas permiten que las aplicaciones cliente autorizadas tengan acceso a una [vista de catálogo privado](catalog-view.md); solo las solicitudes que lleven un token firmado válido de una clave asignada pueden recuperar datos de catálogo. Todas las demás solicitudes son denegadas, incluidas las de los compradores a los que no se ha concedido acceso explícito a esta vista de catálogo y las secuencias de comandos que sondean la API.

Las claves de acceso restringido se aprovisionan de una de las dos maneras siguientes:

- [!BADGE Private Beta]{type=Caution tooltip="Requiere la extensión B2B del conector de Adobe Commerce Optimizer, que actualmente se encuentra en versión beta privada."} **Automáticamente, para catálogos compartidos B2B**: para implementaciones integradas con [!DNL Adobe Commerce Optimizer Connector for B2B], el conector aprovisiona y asigna la clave inicial. A continuación, administre las claves y la asignación de claves desde el administrador de Commerce. Consulte [Autenticación de vista de catálogo](https://experienceleague.adobe.com/es/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage) en la *Guía de administración de Commerce**.

- **Manualmente, para cualquier vista de catálogo**—Para proteger una vista de catálogo usted mismo (por ejemplo, para un portal de socio o una vista previa al lanzamiento), siga los pasos de este tema a partir de [Crear una clave de acceso restringido](#create-a-restricted-access-key).

## Casos de uso de claves de acceso restringido

En [!DNL Adobe Commerce Optimizer], **[!UICONTROL Price Book ID]** determina los precios que ve una solicitud; determina los precios, no quién puede realizar la solicitud. Cualquier cliente que conozca el ID de la vista de catálogo y el ID del libro de precios puede recuperar esos datos a través de la API de comercialización. Las claves de acceso restringidas agregan un control independiente y complementario: tienen el alcance de quién puede acceder a una vista de catálogo en absoluto, independientemente de qué libro de precios se aplique.

Las claves de acceso restringido se utilizan normalmente para:

- **Asignación de precios B2B basada en contrato**: restringe una vista de catálogo vinculada a un libro de precios negociado para que sólo el comprador al que se aplica pueda consultarla. Otras organizaciones compradoras y el público no pueden. Esto se configura automáticamente en los catálogos compartidos B2B. Consulte [Rotación y administración de claves](#key-management-and-rotation).
- **Portales de socios y revendedores**: limite un subconjunto del catálogo a los socios aprobados que se integren directamente con la API de comercialización.
- **Previsualizaciones previas al lanzamiento**: permita que un sistema interno o de socio de confianza obtenga una vista previa de los próximos productos antes de que sean visibles para el público.

## Funcionamiento de las claves de acceso restringido

Una clave de acceso restringido es el componente público de un par de claves RSA. La aplicación cliente genera y utiliza esta clave para demostrar que está autorizado a leer una vista de catálogo privado. En este contexto, _aplicación cliente_ hace referencia al sistema backend que autentica a los compradores (por ejemplo, lógica personalizada en [!DNL Adobe Commerce] o un back-end de terceros), nunca al propio front-end de la tienda.

Los siguientes pasos describen cómo un par de claves y un token firmado pasan de la creación a la validación para las vistas de catálogo que no forman parte de un catálogo compartido B2B.

1. La aplicación cliente genera un par de claves RSA y mantiene la clave privada.
1. La clave **public** se registra en [!DNL Commerce Optimizer] como clave de acceso restringido.
1. La aplicación cliente firma un token web JSON (JWT) con la clave privada y lo incluye con cada solicitud a una vista de catálogo privado.
1. [!DNL Commerce Optimizer] valida la firma del token con la clave pública registrada y, si es válida, devuelve los datos del catálogo solicitado.

## Creación de una clave de acceso restringido

>[!NOTE]
>
>Esta sección y las tres siguientes describen el flujo manual de [!DNL Adobe Commerce Optimizer] Studio. Si usa catálogos compartidos B2B con [!DNL Adobe Commerce Optimizer Connector B2B extension], administre claves desde el administrador de Commerce. Consulte [Claves de acceso restringido](../../aco-connector/restricted-access-keys.md) en la documentación de _Conector de Adobe Commerce Optimizer_.

Para la prueba inicial de vistas de catálogo privado, genere un par de claves con una herramienta como [!DNL OpenSSL]. Guarde la clave privada en secreto. Solo se cargó la clave pública en [!DNL Commerce Optimizer].

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

Una clave de acceso restringido solo autentica el acceso después de asignarla a una vista de catálogo con **[!UICONTROL Catalog Protection]** habilitado. Consulte [Proteger una vista de catálogo](private-catalog-view.md#protect-a-catalog-view) para ver los pasos de configuración.

## Eliminación de una clave

1. En la página **[!UICONTROL Restricted access keys]**, busque la clave que desea quitar y haga clic en **[!UICONTROL Delete]**.

   Si la clave se asigna a una o varias vistas de catálogo, una advertencia explica que las aplicaciones cliente que dependen de esa clave pierden el acceso. Las vistas del catálogo en sí permanecen protegidas y no se puede acceder a ellas públicamente.

1. Confirme la eliminación.

## Administración y rotación de claves

Las claves de acceso restringido se administran de una de las dos maneras siguientes, en función de cómo utilice la protección del catálogo:

- **De forma automática, para catálogos compartidos B2B**—[!BADGE Private Beta]{type=Caution tooltip="Requiere la extensión B2B del conector de Adobe Commerce Optimizer, que actualmente se encuentra en versión beta privada."} Para implementaciones integradas con [!DNL Adobe Commerce Optimizer Connector for B2B], el servicio genera y asigna automáticamente la primera clave de acceso restringido cuando se crea una vista de catálogo. Cada vista del catálogo obtiene su propia clave. Después, puede administrar cada clave desde las páginas Catálogo compartido o Cuenta de compañía. También puede ver y administrar claves desde la página Administrador de Commerce **Claves de acceso restringido** (**Sistema** > **Transferencia de datos**). Consulte [Administrar configuración de vista de catálogo](https://experienceleague.adobe.com/es/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage).

  Cada combinación de un catálogo compartido y una vista de tienda a la que está asignado se proyecta como una vista de catálogo independiente. Una proyección es la vista de catálogo, la directiva, la referencia del libro de precios y los datos de configuración de clave de acceso restringido que el conector exporta a [!DNL Adobe Commerce Optimizer] para esa combinación. Por lo tanto, un catálogo compartido asignado a varias vistas de tienda produce varias vistas de catálogo, cada una con su propia clave. Edite o gire una clave para una vista de catálogo sin afectar a las demás.

  Las claves tienen de forma predeterminada un periodo de caducidad largo. Si necesita girar una clave, añada la sustitución en el Admin y mantenga ambas activas hasta que elimine la anterior. Ver [cambios en el catálogo compartido B2B](/help/aco-connector/get-started.md#monitor-b2b-shared-catalog-changes).

- **Manualmente, para cualquier vista de catálogo**: para las vistas de catálogo que no están asociadas con un catálogo compartido B2B en el backend de Adobe Commerce, la generación de claves, la firma de tokens y la rotación están administradas por completo por la aplicación cliente backend que autentica a los compradores. [!DNL Adobe Commerce Optimizer] no genera ni gira estas claves en su nombre. Siga los pasos descritos anteriormente en este tema para crear, agregar y eliminar claves. Para girar una clave, vea [Rotar una clave](#rotate-a-key).

### Rotar una clave

Para girar una clave sin interrumpir el acceso, tenga en cuenta que una vista de catálogo puede tener hasta tres claves asignadas a la vez:

1. Genere un nuevo par de claves y añada la nueva clave pública como nueva clave de acceso restringido.
1. Asigne la nueva clave a la vista de catálogo junto con la clave existente.
1. Inicie la firma de nuevos tokens con la nueva clave privada para completar la sustitución de claves.
1. Una vez que todas las aplicaciones cliente estén confirmadas en la nueva clave, elimine la clave antigua.

## Límites

Ver [límites de directivas y vistas de catálogo](../boundaries-limits.md#catalog-views-and-policies).

## Más parecido a esto

- [Vistas de catálogo privado](private-catalog-view.md): aprenda a proteger una vista de catálogo con claves de acceso restringido.
- [Cambios en el catálogo compartido B2B](/help/aco-connector/get-started.md#monitor-b2b-shared-catalog-changes): descubra cómo [!DNL Adobe Commerce Optimizer Connector] automatiza la administración de claves para los catálogos compartidos B2B.

