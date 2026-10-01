---
title: Vistas de catálogo privado
description: Descubra cómo las vistas de catálogo privado restringen el acceso a los datos del catálogo, creados automáticamente para catálogos compartidos B2B o configurados manualmente con la protección de catálogo.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y a [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
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
source-git-commit: f93bd673624c58050696da772ce733874ce594e5
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 0%
---
# Vistas del catálogo privado

De manera predeterminada, [la vista de catálogo](catalog-view.md) es pública. Restrinja el acceso a una vista de catálogo para que solo las solicitudes con un token firmado válido puedan recuperar sus datos.

Una vista de catálogo se vuelve privada de una de las dos maneras siguientes:

- [!BADGE Private Beta]{type=Caution tooltip="Requiere la extensión B2B del conector de Adobe Commerce Optimizer, que actualmente se encuentra en versión beta privada."} **De forma automática, para los catálogos compartidos B2B**: para las implementaciones de Commerce que usan la integración de [!DNL Adobe Commerce Optimizer Connector] con la extensión B2B, las vistas de catálogo privado se crean y configuran automáticamente, según la configuración de catálogo compartido en [!DNL Adobe Commerce]. Consulte [Vistas automáticas de catálogo privado para catálogos compartidos B2B](#automatic-private-catalog-views-for-b2b-shared-catalogs).

- **Manualmente, para cualquier vista de catálogo**: para restringir el acceso a una vista de catálogo que de otra manera sería pública, incluida una vista de catálogo B2C, siga los pasos de [Proteger una vista de catálogo](#protect-a-catalog-view). Consulte [Casos de uso de claves de acceso restringido](restricted-access-keys.md#restricted-access-key-use-cases) para ver ejemplos, como portales de socios y vistas previas al lanzamiento.

La protección del catálogo solo se aplica a la vista de catálogo seleccionada. No cambia las políticas ni las capas de la vista. Restringe la vista a un único libro de precios; consulte [Restricción del libro de precios en vistas de catálogo privado](#price-book-restriction-on-private-catalog-views).

## Comprender el límite de protección

La protección del catálogo solo se aplica a la vista de catálogo en la que está activada. Protege las solicitudes de catálogo y de búsqueda, pero no cambia las directivas ni las capas de la vista, protege otras vistas de catálogo ni protege el carro de compras, las operaciones de cierre de compra o de pedido.

El backend de comercio conectado debe aplicar de forma independiente la idoneidad de la compra.

## Restricción de libro de precios en vistas de catálogo privado

Una vista de catálogo privado sólo puede hacer referencia a un libro de precios. Esto difiere de una vista de catálogo público, que puede utilizar varios libros de precios.

Cuando se habilita [!UICONTROL Catalog Protection], el selector de libro de precios del formulario de vista de catálogo cambia de un control de selección múltiple a un control de selección única (botón de opción).

![Restricción del libro de precios de vista de catálogo privado](../assets/catalog-view-private-pricebook-restrictions.png)

- Si activa [!UICONTROL Catalog Protection] en una vista de catálogo que tiene varios libros de precios asignados, no podrá guardar la vista hasta que elimine todos los libros de precios excepto uno.
- Si anteriormente ha guardado una vista de catálogo privado con varias asignaciones de libro de precios antes de que existiera esta restricción, la configuración de la vista de catálogo no cambia automáticamente. Sin embargo, la próxima vez que edite la vista, deberá eliminar todos los libros de precios excepto uno para poder guardar las actualizaciones.

En cada uno de estos casos, [!DNL Adobe Commerce Optimizer] muestra el siguiente mensaje de validación: `A protected catalog view can use only one price book. Select 'Single price book only' to continue.`

Las vistas de catálogo público no se ven afectadas por esta restricción y pueden seguir haciendo referencia a varios libros de precios.

## Vistas automáticas de catálogos privados para catálogos compartidos B2B

[!BADGE Private Beta]{type=Caution tooltip="Requiere la extensión B2B del conector de Adobe Commerce Optimizer, que actualmente se encuentra en versión beta privada."}

Para implementaciones integradas con [!DNL Adobe Commerce Optimizer Connector for B2B] que admitan catálogos compartidos, la extensión crea y configura vistas de catálogo privado automáticamente, según la configuración de catálogo compartido en [!DNL Adobe Commerce]. Esta configuración incluye la vista de catálogo, la directiva, una clave de acceso inicial restringida y una referencia del libro de precios. Con esta configuración, administra las claves de acceso restringido desde la página Administrador de Commerce **Claves de acceso restringido** (**Sistema** > **Transferencia de datos**). Para obtener más información, consulte [Cambios en el catálogo compartido B2B](/help/aco-connector/get-started.md#monitor-b2b-shared-catalog-changes) en la *[!DNL Adobe Commerce Optimizer Connector]Guía de integración*.

Si no usa catálogos compartidos B2B, por ejemplo, para proteger una vista del catálogo para un portal de socio o una vista previa al lanzamiento, use las instrucciones de [Proteger una vista del catálogo](#protect-a-catalog-view) para configurar una manualmente.

## Proteger una vista de catálogo

>[!NOTE]
>
>Omita este procedimiento para las vistas de catálogo asociadas con catálogos compartidos B2B administrados por [!DNL Adobe Commerce Optimizer Connector for B2B]. Consulte [Vistas automáticas de catálogo privado para catálogos compartidos B2B](#automatic-private-catalog-views-for-b2b-shared-catalogs).

Antes de empezar, [cree una clave de acceso restringido](restricted-access-keys.md) a partir de la clave pública que genere su aplicación cliente.

1. En el formulario de creación o edición de la vista de catálogo, cambie **[!UICONTROL Catalog Protection]** a **[!UICONTROL Enabled]**.

1. En **[!UICONTROL Restricted Access Keys]**, seleccione hasta tres [claves de acceso restringido](restricted-access-keys.md) para asignarlas a esta vista de catálogo.

   ![Protección de catálogo habilitada en el formulario de edición de vista de catálogo, con una clave de acceso restringido asignada](../assets/catalog-view-protected.png){width="70%" zoomable="yes"}

1. Haga clic en **[!UICONTROL Save catalog view]**.

   La vista de catálogo está ahora protegida. Solo las solicitudes que llevan un token firmado válido de una clave asignada pueden recuperar sus datos.

   >[!NOTE]
   >
   >Espere hasta cinco minutos para que los cambios de configuración de Protección de catálogos entren en vigor.

## Verificar que el acceso sea obligatorio

Para confirmar que una vista de catálogo privado rechaza solicitudes no autorizadas, llame a su [extremo GraphQL](../get-started.md#get-instance-details) con y sin un token firmado, utilizando estos encabezados:

| Header | Finalidad |
| --- | --- |
| `AC-View-ID` | La vista de catálogo que se va a consultar. |
| `AC-Price-Book-ID` | El libro de precios que aplicar. |
| `AC-Catalog-View-Access-Token` | El JWT firmado que prueba la autorización para la vista de catálogo. |

Una solicitud sin un token válido devuelve un error de GraphQL en lugar de datos de catálogo, por ejemplo:

```json
{
  "errors": [
    {
      "message": "Access key validation failed: Missing token",
      "extensions": { "x-commerce-exception": "access-key-invalid" }
    }
  ]
}
```

Una solicitud que lleva un token firmado por una clave asignada no caducada devuelve los datos del catálogo según lo esperado. Para obtener más información sobre cómo firmar un JWT y llamar a la API de comercialización, consulta la [documentación para desarrolladores](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication).

## Administrar claves de acceso restringido

Si [!UICONTROL Catalog Protection] está habilitado y todas las claves asignadas caducan, no se podrá obtener acceso a la vista de catálogo. Las tiendas que dependen de esta vista de catálogo no pueden servir datos de ella. Asigne una clave nueva que no haya caducado para restaurar el acceso. Para obtener instrucciones, vea [Rotar claves](restricted-access-keys.md#rotate-a-key).

>[!NOTE]
>
>Para implementaciones integradas con la extensión [!DNL Adobe Commerce Optimizer Connector for B2B], administra las claves de acceso desde la página Administrador de Commerce **Claves de acceso restringido** (**Sistema** > **Transferencia de datos**). Para obtener más información, consulte [Administración restringida de claves de acceso](../../aco-connector/restricted-access-keys.md) en la *[!DNL Adobe Commerce Optimizer Connector]Guía de integración*.

## Más parecido a esto

- [Vistas de catálogo](catalog-view.md): aprenda cómo las vistas de catálogo organizan el catálogo de productos según la estructura empresarial, las directivas y los precios.
- [Claves de acceso restringido](restricted-access-keys.md): cree, asigne y gire las claves utilizadas para firmar tokens para la protección del catálogo.
