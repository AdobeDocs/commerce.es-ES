---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%
---
<!--This shared include file contains the conceptual and architecture overview of catalog views for Adobe Merchandising Services-->

Una vista de catálogo define los productos y los precios que un cliente puede recuperar. Combina fuentes de catálogo, capas de catálogo, directivas y libros de precios para admitir diferentes marcas, regiones, unidades de negocio o canales.

## ¿Qué son las vistas de catálogo?

Las vistas de catálogo definen cómo se organiza y muestra el catálogo de productos. Actúan como filtros que determinan lo siguiente:

- **Qué productos son visibles** según la estructura de la empresa (marcas, regiones, distribuidores)
- **Qué precios se muestran** a través de los libros de precios vinculados
- **Cómo se filtran los productos** mediante directivas (atributos como marca, modelo y categoría)
- **El [origen del catálogo](/help/optimizer/setup/catalog-sources.md) que se usa** según atributos como la configuración regional
- **Quién puede tener acceso a los datos de la vista** mediante [Protección de catálogo](private-catalog-view.md) y [claves de acceso restringido](restricted-access-keys.md)

Por ejemplo, puede crear vistas de catálogo independientes para:

- Una marca o unidad de negocio
- Una región geográfica
- Un distribuidor o canal de socios
- Un segmento de clientes con precios específicos

## Descripción general de arquitectura

Las vistas de catálogo forman parte del marco de servicios de Adobe Merchandising, que sustituye al marco de sitio web, tienda y vista de tienda utilizado en los cimientos de Adobe Commerce por un modelo más flexible:

![[!DNL Merchandising Services] arquitectura](/help/assets/ccdm-shared/setup/merchandising-svcs-architecture.png)

### Cómo funciona

**1. Ingesta de datos**
Los datos de catálogo de un servidor de Adobe Commerce u otro servidor de terceros (por ejemplo, PIM o ERP) y otros sistemas se incorporan a la capa de datos de los servicios de Adobe Merchandising. Cada SKU contiene información de configuración regional y atributos de producto que se asignan a vistas de catálogo, políticas y configuraciones regionales. El proceso de ingesta de datos depende del sistema de origen y del método de integración:

- **backend de Adobe Commerce**: el sistema exporta fuentes de catálogo de Commerce, las asigna al formato esperado por la API de REST de ingesta de datos y sincroniza los datos de fuente con la capa de datos de Adobe Merchandising Services. En este modelo, Adobe Commerce administra la sincronización inicial y las actualizaciones posteriores. Las fuentes incluyen productos, categorías, atributos de productos, precios y libros de precios.

- **Sistema de origen o back-end de terceros**: un conector o servicio de integración recupera datos de catálogo de la fuente a través de API, eventos o fuentes de exportación, y luego los asigna y valida con el esquema del modelo de datos de catálogo maquetable (CCDM), y sincroniza los datos con la capa de servicios de Adobe Merchandising a través de la API de ingesta de datos. La integración es responsable de la carga inicial y de enviar los cambios posteriores. Un conector específico de la plataforma, como [Salesforce Commerce Connector](https://experienceleague.adobe.com/es/docs/commerce/optimizer/developer/salesforce-connector) de Adobe, puede proporcionar un punto de partida.

**2. Catálogo base unificado**
Los datos introducidos crean un catálogo base unificado en la canalización de datos del servicio de catálogo. Esta fuente única elimina la duplicación de datos entre unidades empresariales.

**3. Vistas de catálogo**
Varias vistas de catálogo representan diferentes unidades de negocio (por ejemplo, Texas Retail, Texas Retail Seasonal). Las configuraciones regionales, las directivas y los libros de precios se pueden compartir en las vistas de catálogo para mayor flexibilidad.

**4. Entrega multicanal**
Los datos del catálogo filtrado se envían a destinos como Edge Delivery Services, mercados, plataformas publicitarias y microtiendas personalizadas. Para obtener más información sobre la entrega de datos del catálogo, consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/services/optimizer/).

Cuando una vista de catálogo tiene **[!UICONTROL Catalog Protection]** habilitado, la entrega a ese destino requiere un token firmado válido de una [clave de acceso restringido](restricted-access-keys.md) asignada; se deniegan las solicitudes no autorizadas en lugar de recibir los datos del catálogo.

### Componentes clave

| Componente | Finalidad | Ejemplo |
|---|---|---|
| **Vista de catálogo** | Unidad de negocio o canal de distribución | Red de distribuidores, Tienda regional |
| **Directiva** | Filtro de productos basado en atributos | Marca, modelo y categoría |
| **Configuración regional** | Configuración de idioma/región | en-US, fr-CA, es-MX |
| **Libro de precios** | Estructura de precios | Comercial, Mayorista, Empleado |
| **Clave de acceso restringido** | Credencial de token firmado que comunica el acceso a una vista de catálogo protegida | Clave del portal de socios, clave de precios B2B |

### Flujo de datos

1. **Ingesta** - datos de catálogo del backend de Adobe Commerce
2. **Proceso**: aplicar vistas de catálogo, directivas y precios
3. **Entregar**: sirve el catálogo filtrado a tiendas, mercados, etc

## Características principales

| Función | Beneficio |
|---|---|
| **Catálogo base único** | Eliminar la duplicación de datos entre unidades empresariales |
| **Precios flexibles** | Varios libros de precios por SKU para diferentes segmentos de clientes |
| **Escalable** | Gestione más de 200 millones de SKU de forma eficaz |
| **Canal múltiple** | Ofrecer catálogos a tiendas, mercados y plataformas publicitarias. |
| **Actualizaciones en tiempo real** | Actualización rápida de los datos de catálogo para promociones y campañas |
| **Vistas del catálogo privado** | Restringir una vista de catálogo a clientes autorizados mediante la validación de token firmado |

## Casos de uso

### Conglomerado multimarca

**Desafío**: administra varias marcas, países e idiomas<br>
**Solución**: catálogo único con vistas de catálogo para cada combinación de marca y región

### Distribuidor de piezas de automóviles

**Desafío**: 3.000 distribuidores con los mismos productos pero precios diferentes<br>
**Solución**: Un catálogo con vistas de catálogo y libros de precios específicos del distribuidor

### Retailer con varias ubicaciones

**Desafío**: Diferentes precios e inventarios por ubicación<br>
**Solución**: vistas de catálogo basadas en ubicación con directivas específicas de región

>[!NOTE]
>
>Para obtener información detallada acerca de la ingesta y entrega de datos de catálogo, consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/services/optimizer/).
