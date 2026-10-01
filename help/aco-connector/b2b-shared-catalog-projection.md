---
title: Proyección de catálogo compartido B2B
description: Conozca cómo el conector B2B proyecta los catálogos compartidos Adobe Commerce B2B en las vistas de catálogo protegidas de Commerce Optimizer y cómo las tiendas resuelven y autorizan el acceso de los compradores.
feature: Integration, Configuration
role: Admin, Developer
level: Intermediate
TQID: 'https://experienceleague.adobe.com/b37PBjcVQXRSLrB6c7nEf3A3U5cuLs1lQzwPUbp9fdA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
feature_v2:
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: 3c398179-d35a-51ba-b317-6c5b95feef5e
    internal-label: Logs
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%
---
# Proyección del catálogo compartido B2B

Los [!DNL Adobe Commerce Optimizer Connector for B2B] proyectos [!DNL Adobe Commerce] compartieron catálogos y asignaciones de la compañía en vistas de catálogo [!DNL Adobe Commerce Optimizer] protegidas.

## Sincronización base y proyección B2B

La base [!DNL Adobe Commerce Optimizer Connector] sincroniza las fuentes de catálogo y de precios, asignando vistas de tienda a orígenes de catálogo, sitios web a libros de precios y grupos de clientes a libros de precios.

[!DNL Adobe Commerce Optimizer Connector for B2B] proyecta el surtido y los precios de cada catálogo compartido personalizado en una vista protegida. Adobe Commerce selecciona la vista utilizando la asignación de empresa del comprador. La clave de acceso restringido verifica las solicitudes firmadas, pero no determina el acceso al catálogo. Adobe Commerce es el sistema de registro de datos de catálogo, precios y proyección B2B administrados por conectores. Administre el descubrimiento de productos y las recomendaciones en la configuración de [!DNL Adobe Commerce Optimizer].

## Asignación de datos

La proyección B2B combina el contenido de catálogo sincronizado y los precios con el surtido de catálogos compartidos y el contexto de asignación de la empresa.

![Asignación de diagrama [!DNL Adobe Commerce] a vistas de tienda, precios, catálogos compartidos y asignaciones de la compañía a vistas de catálogo privado proyectadas en [!DNL Adobe Commerce Optimizer]](./assets/b2b-catalog-projection-mapping.svg){width="800"}

| [!DNL Adobe Commerce] datos | [!DNL Adobe Commerce Optimizer] resultado | Finalidad |
| --- | --- | --- |
| Vista de tienda y datos de productos habilitados | Origen del catálogo | Proporciona contenido de producto localizado. |
| Precios de sitios web y grupos de clientes | Libro de precios | Suministra los precios aplicables pero no autoriza el acceso |
| Surtido de catálogos compartidos personalizados | Política | Filtra la vista de catálogo en el surtido de catálogos compartidos. |
| Catálogo compartido personalizado y vista de tienda habilitada | Vista de catálogo privado | Crea una vista protegida para cada combinación, con el origen del catálogo, la política y el libro de precios aplicables. |
| Asignación de la compañía a un catálogo compartido | Contexto del comprador resuelto | Permite que el servidor autenticado resuelva la vista de catálogo asociada a la compañía del comprador. |
| Clave de acceso restringido asignada a una vista protegida | Protección de catálogo | Autoriza las solicitudes a la vista de catálogo protegido, pero no selecciona los precios. |

Cada vista de catálogo privado sólo puede hacer referencia a un libro de precios. Las vistas de tienda con el mismo sitio web y contexto de precios del grupo de clientes pueden compartir un libro de precios al mismo tiempo que utilizan diferentes fuentes de catálogo localizadas. El conector no crea un libro de precios por catálogo compartido.

El catálogo compartido predeterminado no se proyecta como una vista de catálogo privado B2B.

## Autorización de tiempo de ejecución

Una vez que el comprador inicia sesión, el backend de Commerce autentica la sesión y utiliza la asignación de empresa y la vista de tienda del comprador para resolver la vista de catálogo y el libro de precios adecuados.

La tienda envía el ID de vista de catálogo, el ID de libro de precios y el token firmado con cada solicitud de API de comercialización. [!DNL Adobe Commerce Optimizer] verifica la firma RS256 para el JWT con las claves de acceso restringido asignadas a la vista de catálogo. Devuelve los datos del catálogo solo cuando el token y la clave son válidos y no han caducado.

![Flujo de autorización en tiempo de ejecución para solicitudes de catálogo B2B de un comprador a través de una tienda y el back-end de Commerce a [!DNL Adobe Commerce Optimizer]](./assets/b2b-catalog-runtime-authorization.svg){width="700"}

Para solicitudes de catálogo privadas, envíe estos encabezados:

| Header | Finalidad |
| --- | --- |
| `AC-View-ID` | Identifica la vista de catálogo. |
| `AC-Price-Book-ID` | Identifica el libro de precios que se va a utilizar. |
| `AC-Catalog-View-Access-Token` | Lleva el JWT firmado que autoriza el acceso a la vista de catálogo protegido. |

Para conocer todos los requisitos de solicitud y token, consulte [Autenticación de la API de comercialización](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication) y [Verificar el acceso a una vista de catálogo privado](/help/optimizer/setup/private-catalog-view.md#verify-access-is-enforced).

## Límite de protección

La protección del catálogo cubre únicamente las solicitudes de catálogo y búsqueda. No protege el carro de compras, el cierre de compra ni las operaciones de pedidos. Haga cumplir la idoneidad de la compra en Adobe Commerce o en el sistema de transacciones conectado.

## Configuración y monitorización de las proyecciones

El conector B2B proyecta vistas de catálogo privado, directivas, referencias de libro de precios y configuración de clave de acceso restringido desde [!DNL Adobe Commerce]. No es necesario crear manualmente estos objetos de proyección gestionados por el conector. Para obtener instrucciones de configuración, consulte [Introducción al conector B2B](get-started-b2b-shared-catalogs.md).

Para supervisar las vistas de catálogo proyectadas y reconciliar la desviación de la configuración, consulte [Supervisar la sincronización de la vista de catálogo](catalog-view-sync-status.md). Para administrar las claves asignadas, consulte [Administrar claves de acceso restringido para catálogos compartidos B2B](restricted-access-keys.md).
