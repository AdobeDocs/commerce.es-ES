---
source-git-commit: b6b737220a6dadf55b03da54e8d74226ed578cd0
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 0%
---
# Claves de acceso restringido

Las claves de acceso restringidas permiten que las aplicaciones cliente autorizadas tengan acceso a una [vista de catálogo privado](private-catalog-view.md); solo las solicitudes que lleven un token firmado válido de una clave asignada pueden recuperar datos de catálogo. El resto de las solicitudes se deniegan, incluidas las de los compradores que no tienen acceso explícito a esta vista de catálogo y las secuencias de comandos que sondean la API de Adobe Commerce Merchandising Services.

Las claves de acceso restringido se aprovisionan de una de las dos maneras siguientes:

- **Automáticamente, para catálogos compartidos B2B**: el sistema aprovisiona y asigna la clave inicial para las vistas de catálogo asociadas a un catálogo compartido B2B. A continuación, administre las claves y la asignación de claves desde el administrador de Commerce. Consulte [Autenticación de vista de catálogo](https://experienceleague.adobe.com/es/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage) en la *Guía de administración de Commerce*. El aprovisionamiento automático está disponible en las siguientes implementaciones:

  - **Adobe Commerce as a Cloud Service con CCDM** para Adobe Commerce B2B.
  - **Adobe Commerce en la nube o local** integrado con Adobe Commerce Optimizer a través de [!DNL Adobe Commerce Optimizer Connector for B2B]. Se requiere la extensión B2B para el conector.

- **Manualmente, para cualquier vista de catálogo**—Para proteger una vista de catálogo usted mismo (por ejemplo, para un portal de socio o una vista previa al lanzamiento), siga los pasos de este tema a partir de [Crear una clave de acceso restringido](#create-a-restricted-access-key).

## Casos de uso de claves de acceso restringido

**[!UICONTROL Price Book ID]** determina los precios que ve una solicitud, determina los precios y no quién puede realizar la solicitud. Cualquier cliente que conozca el ID de la vista de catálogo y el ID del libro de precios puede recuperar esos datos a través de la API de servicios de comercialización. Las claves de acceso restringidas agregan un control independiente y complementario: tienen el alcance de quién puede acceder a una vista de catálogo en absoluto, independientemente de qué libro de precios se aplique.

Las claves de acceso restringido se utilizan normalmente para:

- **Asignación de precios B2B basada en contrato**: restringe una vista de catálogo vinculada a un libro de precios negociado para que sólo el comprador al que se aplica pueda consultarla. Otras organizaciones compradoras y el público no pueden. Esto se configura automáticamente en los catálogos compartidos B2B. Consulte [Rotación y administración de claves](#key-management-and-rotation).
- **Portales de socios y revendedores**: limita un subconjunto del catálogo a los socios aprobados que se integren directamente con la API de Servicios de comercialización.
- **Previsualizaciones previas al lanzamiento**: permita que un sistema interno o de socio de confianza obtenga una vista previa de los próximos productos antes de que sean visibles para el público.

## Funcionamiento de las claves de acceso restringido

Una clave de acceso restringido es el componente público de un par de claves RSA. La aplicación cliente genera y utiliza esta clave para demostrar que está autorizado a leer una vista de catálogo privado. En este contexto, _aplicación cliente_ hace referencia al sistema backend que autentica a los compradores (por ejemplo, lógica personalizada en [!DNL Adobe Commerce] o un back-end de terceros), nunca al propio front-end de la tienda.

Los siguientes pasos describen cómo un par de claves y un token firmado pasan de la creación a la validación para las vistas de catálogo que no forman parte de un catálogo compartido B2B.

1. La aplicación cliente genera un par de claves RSA y mantiene la clave privada.
1. La clave **public** se registra en el sistema como clave de acceso restringido.
1. La aplicación cliente firma un token web JSON (JWT) con la clave privada y lo incluye con cada solicitud a una vista de catálogo privado.

   El sistema valida la firma del token con la clave pública registrada y, si es válida, devuelve los datos de catálogo solicitados.

## Acceso al espacio de trabajo de claves de acceso restringido

La forma de abrir el espacio de trabajo de claves de acceso restringido depende del producto que utilice:

- **Administrador de Adobe Commerce** (Adobe Commerce as a Cloud Service)—Seleccione *Sistema* > *Transferencia de datos* > **Claves de acceso restringido**.
- **Adobe Commerce Optimizer Studio**—Seleccione *Configuración de tienda* > **Claves de acceso restringidas**.

## Creación de una clave de acceso restringido

>[!NOTE]
>
>Esta sección y las dos siguientes describen el proceso manual para administrar las claves de acceso restringido. Para los catálogos compartidos B2B con el aprovisionamiento automático de claves, administre las claves desde el administrador de Commerce. Ver [Claves de acceso restringido](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys).

### Añadir una clave de acceso restringido

Seleccione la pestaña de la herramienta que utiliza para administrar claves: Commerce Admin o Adobe Commerce Optimizer Studio.

>[!BEGINTABS]

>[!TAB Administrador de Adobe Commerce]

Los clientes que utilizan Adobe Commerce as a Cloud Service con CCDM o Adobe Commerce Optimizer conectado a Adobe Commerce a través del conector pueden generar pares de claves RSA desde el administrador de Commerce. Ver [Administrar claves de acceso restringido](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys).

>[!TAB Adobe Commerce Optimizer Studio: administración manual de claves]

Los clientes que utilizan Adobe Commerce Optimizer Studio deben generar y administrar sus propios pares de claves RSA y luego agregar la clave pública al sistema. Este es el flujo de trabajo necesario para Adobe Commerce Optimizer con un back-end de terceros. Los clientes que utilizan el conector también pueden utilizar este flujo de trabajo en lugar del administrador de Commerce.

**Generar un par de claves RSA**

Para la prueba inicial de vistas de catálogo privado, genere un par de claves con una herramienta como [!DNL OpenSSL]. Guarde la clave privada en secreto. Solo la clave pública se carga en el sistema como clave de acceso restringido.

```bash
openssl genrsa -out private-key.pem 2048
openssl rsa -in private-key.pem -pubout -out public-key.pem
```

El tamaño de la clave debe estar entre 2048 y 8192 bits. `public-key.pem` contiene el valor que pega en el campo **[!UICONTROL Public key]** siguiente.

**Agregar la clave pública al sistema**

1. En el área de trabajo Clave de acceso restringido, haga clic en **[!UICONTROL Add Restricted Access Key]**.

   ![Lista de claves de acceso restringido, con el botón Agregar clave de acceso restringido](/help/assets/ccdm-shared/setup/restricted-access-keys.png){width="70%" zoomable="yes"}

1. Introduzca los detalles de la clave:

   ![Agregar formulario con clave de acceso restringido, con los campos Título, Fecha de caducidad y Clave pública](/help/assets/ccdm-shared/setup/restricted-access-keys-add.png){width="70%" zoomable="yes"}

   - **[!UICONTROL Title]**: una etiqueta para identificar la clave, que se muestra en la lista de claves y en el selector de claves de la vista de catálogo, por ejemplo `ACME Corp wholesale portal — Tier 1 pricing`.
   - **[!UICONTROL Expiration date]**: fecha y hora (UTC) tras las cuales la clave deja de respetarse, incluso para un token que aún no ha caducado.
   - **[!UICONTROL Public key]**: la clave pública RSA con codificación PEM en el formato de información de clave pública del sujeto (SPKI), incluidos los marcadores `-----BEGIN PUBLIC KEY-----` y `-----END PUBLIC KEY-----`. Debe ser único en todo el entorno.

1. Haga clic en **[!UICONTROL Save]**.

>[!ENDTABS]

Las claves son inmutables después de la creación. Para cambiar cualquier valor, elimine la clave y cree uno nuevo. Ver [Rotar una clave](#rotate-a-key) para hacerlo sin interrumpir el acceso.

## Asignación de una clave a una vista de catálogo

Una clave de acceso restringido solo autentica el acceso después de asignarla a una vista de catálogo con **[!UICONTROL Catalog Protection]** habilitado. Consulte [Proteger una vista de catálogo](private-catalog-view.md#protect-a-catalog-view) para ver los pasos de configuración.

## Eliminación de una clave

1. En el área de trabajo **[!UICONTROL Restricted access keys]**, busque la clave que desea quitar y elimínela.

   Si la clave se asigna a una o varias vistas de catálogo, una advertencia explica que las aplicaciones cliente que dependen de esa clave pierden el acceso. Las vistas del catálogo en sí permanecen protegidas y no se puede acceder a ellas públicamente.

1. Confirme la eliminación.

## Administración y rotación de claves

Las claves de acceso restringido se administran de una de las dos maneras siguientes, en función de cómo utilice la protección del catálogo:

- **De forma automática, para los catálogos compartidos B2B**: para las implementaciones B2B de Adobe Commerce que usan Servicios de comercialización con CCDM y para las implementaciones de Adobe Commerce Optimizer integradas a través de [!DNL Adobe Commerce Optimizer Connector for B2B] (que requiere la extensión B2B), el servicio genera y asigna automáticamente la primera clave de acceso restringido cuando se crea una vista de catálogo. Cada vista del catálogo obtiene su propia clave. Después, puede administrar cada clave desde las páginas Catálogo compartido o Cuenta de compañía. También puede ver y administrar claves desde la página Administrador de Commerce **Claves de acceso restringido** (**Sistema** > **Transferencia de datos**). Consulte [Administrar configuración de vista de catálogo](https://experienceleague.adobe.com/es/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage).

  Cada combinación de un catálogo compartido y una vista de tienda se proyecta como una vista de catálogo independiente. Una proyección es la vista de catálogo, la directiva, la referencia del libro de precios y los datos de configuración de clave de acceso restringido que se exportan a la capa de datos de Servicios de comercialización para esa combinación. Por lo tanto, un catálogo compartido asignado a varias vistas de tienda produce varias vistas de catálogo, cada una con su propia clave. Edite o gire una clave para una vista de catálogo sin afectar a las demás.

  Las claves tienen de forma predeterminada un periodo de caducidad largo. Si necesita girar una clave, añada la sustitución en el Admin y mantenga ambas activas hasta que elimine la anterior.

- **Manualmente, para cualquier vista de catálogo**: la forma de generar y administrar claves depende del contexto del producto. En cualquier caso, el cliente backend que autentica a los compradores firma los tokens.

  - **Administrador de Commerce (Adobe Commerce as a Cloud Service con CCDM o Adobe Commerce Optimizer con el conector)**: genere pares de claves RSA en el administrador de Commerce y cree, asigne y elimine claves en la página **Claves de acceso restringido**. Adobe Commerce no gira las teclas automáticamente. Para girar una clave, vea [Rotar una clave](#rotate-a-key).
  - **Adobe Commerce Optimizer Studio**: Studio no genera claves. Este es el flujo de trabajo necesario para Adobe Commerce Optimizer con un back-end de terceros, y los clientes de conectores también pueden utilizarlo. Utilice la aplicación cliente para generar el par de claves RSA, conservar la clave privada y agregar la clave pública como clave de acceso restringido. Siga los pasos descritos anteriormente en este tema para crear, agregar y eliminar claves. Para girar una clave, vea [Rotar una clave](#rotate-a-key).

### Rotar una clave

Para girar una clave sin interrumpir el acceso, tenga en cuenta que una vista de catálogo puede tener hasta tres claves asignadas a la vez:

Seleccione la pestaña de la herramienta que utiliza para administrar claves: Commerce Admin o Adobe Commerce Optimizer Studio.

>[!BEGINTABS]

>[!TAB Administrador de Adobe Commerce]

Ver [Selección y rotación de clave](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys#key-selection-and-rotation). Esto se aplica a Adobe Commerce as a Cloud Service con CCDM y a los proyectos de Adobe Commerce integrados con Adobe Commerce Optimizer a través del conector de Adobe Commerce Optimizer.

>[!TAB Adobe Commerce Optimizer Studio (administración manual de claves)]

Este procedimiento es necesario para Adobe Commerce Optimizer con un servidor de terceros. Los clientes que utilizan el conector también pueden utilizarlo en lugar del administrador de Commerce.

1. Genere un nuevo par de claves y añada la nueva clave pública como nueva clave de acceso restringido.
1. Asigne la nueva clave a la vista de catálogo junto con la clave existente.
1. Inicie la firma de nuevos tokens con la nueva clave privada para completar la sustitución de claves.
1. Una vez que todas las aplicaciones cliente estén confirmadas en la nueva clave, elimine la clave antigua.

>[!ENDTABS]

## Límites

Ver [límites de directivas y vistas de catálogo](https://experienceleague.adobe.com/es/docs/commerce/optimizer/boundaries-limits).

## Más parecido a esto

- [Vistas de catálogo privado](private-catalog-view.md): aprenda a proteger una vista de catálogo con claves de acceso restringido.
