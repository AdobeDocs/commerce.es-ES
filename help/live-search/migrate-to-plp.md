---
title: Migración del adaptador de búsqueda al widget PLP
description: Obtenga información sobre cómo migrar del adaptador de búsqueda obsoleto al widget de página de lista de productos  [!DNL Live Search] .
source-git-commit: 8811f0f271928fbc827e5a0164542da473c57224
workflow-type: tm+mt
source-wordcount: '2053'
ht-degree: 0%

---

# Migración del adaptador de búsqueda al widget PLP

El adaptador de búsqueda ha sido [obsoleto](release-notes.md#live-search-400) a partir de [!DNL Live Search] 4.0.0 y solo recibirá actualizaciones de seguridad. El widget de la página de lista de productos [Product Listing Page (PLP)](plp-styling.md) es la solución compatible con todas las implementaciones de [!DNL Live Search] a partir de ahora. Esta guía le ayuda a comprender cuándo la migración es sencilla y cuándo se requiere trabajo adicional.

## Requisitos previos

Asegúrese de que su entorno cumpla estos requisitos antes de iniciar el proceso de migración.

Antes de iniciar la migración:

**Requisitos técnicos**:

- Adobe Commerce 2.4.4 o superior.
- Extensión [!DNL Live Search] instalada.
- Acceso a la línea de comandos (CLI).
- Acceso al administrador de Commerce.
- Entorno de ensayo o control de calidad para pruebas.

**Copia de seguridad y preparación**:

1. Haga una copia de seguridad de la base de datos y del código.
1. Documentar las personalizaciones actuales.
1. Revise [Límites y límites](boundaries-limits.md) para asegurarse de que el widget PLP satisfaga sus necesidades.
1. Programar migración durante un período de poco tráfico.
1. Notificar a las partes interesadas de posibles cambios en el comportamiento de la tienda.

**Revisar la implementación actual**:

- Compruebe su versión actual de [!DNL Live Search].
- Documente qué facetas están en uso y su configuración.
- Pruebe toda la funcionalidad de búsqueda y documente los comportamientos esperados.
- Captura capturas de pantalla de la presentación de resultados de búsqueda actuales.

**Compatibilidad de versiones**:

- Ejecución de Adobe Commerce 2.4.4 o posterior.
- Listo para actualizar a [!DNL Live Search] 4.0.0 o superior.

## Escenarios de migración

### Migración directa (no se requiere trabajo adicional)

Puede migrar directamente al widget PLP si su implementación cumple TODOS los criterios siguientes:

**Tienda estándar basada en Luma**:

- Utiliza la temática de Luma o una que hereda de Luma con personalizaciones mínimas.
- No ha realizado modificaciones personalizadas en los diseños o plantillas PLP.
- No ha creado extensiones de JavaScript personalizadas que interactúen con los resultados de búsqueda.

**Catálogo de productos estándar**:

- Todos los atributos de producto utilizan modelos de origen estándar (no modelos de origen personalizados).
- No hay tipos de producto personalizados que requieran una lógica de procesamiento especial.
- El catálogo solo utiliza facetas y filtros estándar.

**Integraciones estándar**:

- No utiliza Google Tag Manager (GTM) para Analytics.
- No utiliza extensiones de terceros que modifiquen el comportamiento de búsqueda.

Si su implementación coincide con estos criterios, continúe con [Pasos de migración estándar](#standard-migration-steps).

### Migración que requiere trabajo adicional

Se requiere trabajo adicional si la implementación presenta CUALQUIERA de los siguientes elementos:

**Modificaciones de tema personalizadas**:

- Diseños PLP personalizados que anulan las plantillas de Luma.
- CSS o JavaScript personalizados que segmentan elementos específicos de adaptadores de búsqueda.
- Modificaciones de plantilla personalizadas al PLP o archivos relacionados.
- La temática no hereda de Luma (por ejemplo, la temática personalizada desde cero).

**Atributos de producto personalizados**:

- Atributos de producto con modelos de origen personalizados utilizados como facetas.
- Tipos de productos personalizados con requisitos especiales de visualización.
- Atributos programáticos con `"is_user_defined": false`.

**Integraciones avanzadas**:

- Google Tag Manager (GTM) se utiliza activamente para el seguimiento.
- Herramientas de personalización o análisis de terceros integradas con la búsqueda.
- Implementación de capa de datos o seguimiento de eventos personalizado.
- Integración con motores de búsqueda o recomendación externos.

**Implementaciones sin encabezado o PWA**:

- Usar la arquitectura sin encabezado (por ejemplo, PWA Studio, Vue Storefront).
- Marco de front-end personalizado (React, Vue, Angular).
- Uso de GraphQL exclusivamente para consultas de catálogo.
- Implementación de eventos de tienda personalizados.

**Código de widget personalizado**:

- Previamente se personalizó el código del adaptador de búsqueda.
- Alojar versiones personalizadas de widgets en su propia CDN.
- Extensiones de JavaScript personalizadas para la funcionalidad de búsqueda.

Si su implementación presenta alguno de estos escenarios, consulte [Escenarios de migración complejos](#complex-migration-scenarios).

## Pasos de migración estándar

Para implementaciones sin personalizaciones especiales, siga estos pasos:

### Paso 1: Actualización [!DNL Live Search]

Actualice la extensión [!DNL Live Search] a la versión 4.0 o superior para acceder al widget PLP.

**Rol**: Comerciante o socio

1. Compruebe su versión actual de [!DNL Live Search]:

   ```bash
   composer show magento/live-search | grep version
   ```

1. Si está en la versión 3.x o anterior, habilite el módulo AdvancedSearch antes de actualizar:

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

1. Actualizar `composer.json` para requerir [!DNL Live Search] 4.0 o superior:

   ```json
   "require": {
      "magento/live-search": "^4.0"
   }
   ```

1. Ejecute la actualización:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. Ejecute la actualización y recompilación de la instalación:

   ```bash
   bin/magento setup:upgrade
   bin/magento setup:di:compile
   ```

1. Implemente contenido estático, si es necesario:

   ```bash
   bin/magento setup:static-content:deploy
   ```

### Paso 2: Habilitar el widget PLP

Configure el widget PLP en el administrador de Commerce.

**Rol**: Comerciante

El widget PLP está habilitado de manera predeterminada para las nuevas instalaciones de [!DNL Live Search] 4.0.0+. Si actualiza desde una versión anterior:

1. Vaya a **[!UICONTROL Stores]** > Configuración > **[!UICONTROL Configuration]**.
1. Vaya a **[!UICONTROL Live Search]** > **[!UICONTROL Storefront Features]**.
1. Expanda la sección **[!UICONTROL Storefront Features]**.
1. Establezca **[!UICONTROL Enable Product Listing Widgets]** en **Sí**.
1. Haga clic en **[!UICONTROL Save Config]**.
1. Vaciar la caché: **[!UICONTROL System]** > Herramientas > **[!UICONTROL Cache Management]** > **[!UICONTROL Flush Magento Cache]**.

### Paso 3: Prueba del ensayo

Valide la migración en un entorno que no sea de producción antes de activarla.

**Rol**: Comerciante/Socio

Antes de implementar en producción, pruebe exhaustivamente la funcionalidad de búsqueda:

**Pruebas funcionales**:

- Compruebe que los resultados de la búsqueda aparecen correctamente.
- Pruebe todas las facetas configuradas.
- Verifique que funcione la navegación por categorías.
- Pruebe la paginación con resultados.
- Compruebe que las opciones de ordenación funcionan según lo esperado.
- Pruebe la funcionalidad de complementos al carro de compras para productos simples.

**Pruebas visuales**:

- Confirme que las imágenes del producto se muestran correctamente.
- Compruebe que los nombres y precios de los productos se representan correctamente.
- Muestras de color de prueba (si se utilizan).
- Compruebe el comportamiento interactivo en dispositivos móviles.
- Compruebe que el estilo coincida con su marca.

**Pruebas de rendimiento**:

- Mida los tiempos de carga de la página.
- Prueba con un tamaño de catálogo realista.
- Monitorizar el uso de recursos del servidor.
- Compruebe si hay errores de JavaScript en la consola del explorador.

### Paso 4: Implementación en producción

Mueva la configuración validada a su tienda en vivo.

**Rol**: Comerciante/Socio

1. Programe la implementación durante la ventana de mantenimiento, si es posible.
1. Siga el proceso de implementación estándar.
1. Habilite el widget PLP en producción mediante [Paso 2: Habilite el widget PLP](#step-2-enable-the-plp-widget).
1. Supervise cualquier problema inmediatamente después de la implementación.
1. Tenga un plan de reversión listo si surgen problemas críticos.

### Paso 5: Validación y monitorización

Realice un seguimiento del rendimiento de búsqueda y de la experiencia del cliente después de la migración.

**Rol**: Comerciante

Después de la implementación, monitorice las métricas clave:

- Tasa de búsqueda de resultados cero
- Tasa de conversión de búsqueda a carro
- Rendimiento de carga de página
- Comentarios de clientes o tickets de asistencia
- Errores de JavaScript en la consola del explorador

## Situaciones de migración complejas

Los siguientes escenarios requieren planificación adicional, desarrollo personalizado o soporte especializado más allá de los pasos de migración estándar.

### Tema personalizado con modificaciones de diseño

En esta situación, tiene plantillas o diseños personalizados que anulan el comportamiento predeterminado de la lista de productos.

**Rol**: Desarrollador/Socio

1. **Personalizaciones de auditoría**:
   - Documentar todos los archivos XML de diseño personalizado de la temática.
   - Revise las modificaciones de la plantilla personalizada en las páginas de la lista de productos o en los archivos relacionados.
   - Identifique las clases CSS personalizadas que se utilizan para el estilo.
   - Documente las interacciones personalizadas de JavaScript.

1. **Migrar a personalizaciones basadas en CSS**:
   - El widget PLP utiliza clases CSS específicas (consulte [Guía de estilo PLP](plp-styling.md)).
   - Vuelva a crear personalizaciones visuales con clases CSS de widget PLP.
   - Compruebe que los estilos personalizados se aplican correctamente.

1. **Quitar personalizaciones en conflicto**:
   - Elimine el XML de diseño que modifica la estructura de la lista de productos.
   - Limpie JavaScript que se dirija a elementos específicos del adaptador de búsqueda.
   - La plantilla de actualización anula los conflictos con el procesamiento de widgets.

1. **Realizar pruebas exhaustivas**:
   - Verifique que todas las personalizaciones visuales funcionen con el widget PLP.
   - Asegúrese de que no haya conflictos de diseño.
   - Realizar pruebas en todos los puntos de interrupción y dispositivos.

### Atributos de producto con modelos de origen personalizados

En esta situación, hay facetas que utilizan atributos de producto con modelos de origen personalizados que no son compatibles con el adaptador de búsqueda pero que sí con el widget PLP.

**Rol**: Comerciante (configuración de administración)

1. **Identificar atributos afectados**:
   - Revise los atributos de producto utilizados como facetas.
   - Identificar qué utilizan modelos de origen personalizados.
   - Documentar la configuración de faceta actual.

1. **Actualizar y habilitar el widget PLP**:
   - Siga [pasos de migración estándar](#standard-migration-steps).
   - El widget PLP admite atributos del modelo de origen personalizados.

1. **Volver a configurar facetas**:
   - Vaya a **[!UICONTROL Marketing]** > SEO y busque > **[!UICONTROL Live Search]**.
   - Revise la configuración de facetas para los atributos afectados.
   - Las facetas de prueba funcionan correctamente con los modelos de origen personalizados.

1. **Validar**:
   - Pruebe el filtrado con facetas del modelo de origen personalizadas.
   - Compruebe que todos los valores de atributo aparecen correctamente.
   - Asegúrese de que el rendimiento sea aceptable.

### Integración de Google Tag Manager (GTM)

En esta situación, hay un problema conocido en el que habilitar el widget PLP puede provocar que GTM falle.

**Función**: Desarrollador/Socio + Ingeniería de clientes

**Opción 1: continuar con el adaptador de búsqueda (sólo provisional)**

- Mantenga el adaptador de búsqueda habilitado si GTM es esencial para la empresa.
- Tenga en cuenta que solo recibirá actualizaciones de seguridad.
- Planifique la migración cuando se resuelva la compatibilidad con GTM.
- Póngase en contacto con el Soporte técnico de Adobe para obtener actualizaciones sobre la compatibilidad con GTM.

**Opción 2: migrar el seguimiento de GTM a un enfoque alternativo**

1. **Implementar una colección de eventos personalizada**:

   - Usar [SDK de eventos de tienda](https://developer.adobe.com/commerce/services/shared-services/storefront-events/).
   - Capture eventos de interacción de productos y búsquedas.
   - Insertar eventos manualmente en la capa de datos de GTM.

1. **Complete los pasos siguientes**:

   - Auditar los requisitos actuales de seguimiento de GTM.
   - Asigne eventos de GTM a eventos de tienda.
   - Implemente detectores de eventos personalizados.
   - Pruebe el flujo de datos a GTM.
   - Validar informes de análisis.

**Opción 3: reemplazar GTM por Adobe Analytics**

- Considere migrar a [Adobe Analytics](https://business.adobe.com/es/products/adobe-analytics.html) si corresponde.
- Póngase en contacto con Ingeniería de clientes para obtener ayuda.

**Con quién ponerte en contacto**: envía un ticket de asistencia para recibir actualizaciones de compatibilidad con GTM o ayuda de ingeniería de clientes.

### Escenario: implementación sin encabezado o de PWA

En esta situación, tiene una tienda sin encabezado o de PWA que requiere una recopilación de eventos personalizada y no puede utilizar la IU del widget PLP estándar.

**Rol**: Desarrollador/Socio

1. **Revisar implementaciones de referencia**:
   - Estudie el [código fuente del widget PLP](https://github.com/adobe/storefront-product-listing-page).
   - Revise la documentación de la API de [[!DNL Live Search] GraphQL](graphql.md).
   - Comprender las [consultas del servicio de catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/).

1. **Implementar una IU personalizada**:
   - Usar la API de GraphQL [!DNL Live Search] para las consultas.
   - Crear componentes de lista de productos personalizados.
   - Implemente la interfaz de usuario de para facetear.
   - Controlar la paginación y la ordenación.

1. **Implementar colección de eventos**:
   - Revise [Documentación de eventos de tienda](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search).
   - Implemente los eventos necesarios:
      - `search-request-sent`
      - `search-response-received`
      - `search-results-view`
      - `product-page-view`
      - `add-to-cart`
   - Prueba de flujos de datos de evento en Adobe Commerce.

1. **Configurar ordenación de facetas**:
   - En implementaciones sin encabezado, las facetas se pueden ordenar por recuento.
   - Configurar en el espacio de trabajo **[!UICONTROL Live Search]** > **[!UICONTROL Facets]**.
   - Establezca **[!UICONTROL Sort Type]** en **Count** para una mejor experiencia de usuario.

1. **Probar y validar**:
   - Compruebe la precisión de los resultados de búsqueda.
   - Probar la funcionalidad de faceta.
   - Confirme que los eventos se rastrean correctamente.
   - Supervisar las métricas de rendimiento.
   - Validar el funcionamiento de las funciones inteligentes de comercialización.

### Escenario: modificaciones del código de un widget personalizado

En esta situación, ha personalizado anteriormente el adaptador de búsqueda o el código del widget y necesita migrar las personalizaciones.

**Rol**: Desarrollador/Socio

1. **Personalizar documentos existentes**:
   - Enumerar todas las personalizaciones realizadas en el adaptador de búsqueda.
   - Identifique los requisitos empresariales que impulsan cada personalización.
   - Determine si las personalizaciones siguen siendo necesarias.

1. **Compruebe si las características integradas satisfacen sus necesidades**:
   - Revisar [características del widget PLP](plp-styling.md#widget-features).
   - Compruebe si la personalización basada en CSS es suficiente.
   - Pruebe el comportamiento predeterminado del widget PLP.

1. **Si todavía se necesita código personalizado**:
   - Clone el [repositorio de widget PLP](https://github.com/adobe/storefront-product-listing-page).
   - Implementar las personalizaciones.
   - Host en su propia CDN.
   - Actualice la configuración de Commerce para utilizar el widget personalizado.

   >[!WARNING]
   >
   >Si personaliza el widget PLP mediante el código del repositorio, usted es responsable del mantenimiento y las actualizaciones. Las nuevas funciones del widget PLP de Adobe pueden ser incompatibles con las personalizaciones.

1. **Realizar pruebas exhaustivas**:
   - Pruebe todas las funciones personalizadas.
   - Compruebe que las actualizaciones de Commerce no rompen las personalizaciones.
   - Documente su implementación personalizada.
   - Plan de mantenimiento continuo.

## Limitaciones y casos extremos conocidos

Tenga en cuenta estas limitaciones al migrar:

**limitaciones del widget PLP**:

- **Dirección del orden**: cuando el widget PLP está habilitado, no se puede cambiar la dirección del orden en las páginas de la lista de productos (ascendente/descendente).
- **Agregar al carro**: Los botones Agregar al carro solo están disponibles para productos simples en el widget.
- **Precio de nivel**: No compatible con el widget PLP.
- **Visualización de IVA**: Los precios incluyen IVA, pero el IVA no se puede mostrar como un valor separado.

**Diferencias de características del adaptador de búsqueda**:

- **Muestras de color**: el atributo `color` debe escribirse exactamente como `color` (no como &quot;color&quot; o nombres personalizados) para que las muestras funcionen correctamente.
- **Estilo de tema**: el widget no hereda las clases de tema personalizadas; deben segmentarse en clases CSS específicas del widget.
- **Tipos de productos personalizados**: no compatible con el widget.

**Consideraciones de rendimiento**:

- Los catálogos grandes (más de 50 000 productos) pueden experimentar cargas de página iniciales más largas.
- Varias facetas con muchos valores pueden afectar al rendimiento.
- El rendimiento del dispositivo móvil puede variar en función del tamaño del catálogo.

**Problemas de compatibilidad**:

- Problema de compatibilidad del Administrador de etiquetas de Google (consulte [Escenario de GTM](#google-tag-manager-gtm-integration)).
- Algunas extensiones de terceros pueden entrar en conflicto con el widget PLP.
- Es posible que las extensiones de cierre de compra personalizadas necesiten actualizaciones.

## Obtención de ayuda

Póngase en contacto con el recurso adecuado según sus necesidades específicas.

**Soporte de Adobe** puede ayudarle con lo siguiente:

- Procedimientos de migración estándar de Live Search
- Problemas de configuración del widget PLP
- Problemas de indexación de facetas o atributos
- Problemas de rendimiento con implementaciones predeterminadas
- Errores de actualización

Se debe contactar con **socios de desarrollo/integradores de sistemas** para:

- Modificaciones de temas personalizadas
- Implementaciones de código de widget personalizadas
- Compatibilidad con extensiones de terceros
- Implementaciones sin encabezado o de PWA
- Seguimiento de eventos personalizado

Para ponerse en contacto con el soporte técnico de Adobe, consulte la [Guía del usuario del Centro de ayuda](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

## FAQ

Encuentre respuestas a preguntas comunes sobre la migración del adaptador de búsqueda al widget PLP.

**Q: ¿Recibirá el adaptador de búsqueda correcciones de errores o actualizaciones de características?**

R: No. El adaptador de búsqueda está obsoleto y solo recibirá actualizaciones de seguridad. Las correcciones de errores, las mejoras de rendimiento y las nuevas funciones solo están disponibles en el widget PLP. Si tiene problemas con el adaptador de búsqueda, la migración al widget PLP es la solución recomendada.

**Q: ¿La migración afectará mi tienda?**

R: Si sigue los procedimientos de prueba adecuados en ensayo, la migración debería ser perfecta. Tenga un plan de reversión listo para la implementación de producción.

**Q: ¿Cuánto tiempo tarda la migración?**

R: Para implementaciones estándar: de 1 a 2 horas. Para implementaciones personalizadas: de 1 a 4 semanas según la complejidad.

**Q: ¿Seguirán funcionando mis reglas de comercialización de búsqueda?**

R: Sí, todas las reglas, sinónimos y facetas de comercialización de búsqueda configurados en el espacio de trabajo [!DNL Live Search] siguen funcionando con el widget PLP.

**Q: ¿Debo volver a configurar mis facetas?**

R: Por lo general, no, pero si estaba limitado por atributos del modelo de origen personalizados con el adaptador de búsqueda, ahora puede utilizarlos con el widget PLP.

**Q: ¿Qué sucede con mi CSS personalizado?**

R: Debe actualizar CSS para segmentar las clases de widgets PLP. Consulte la [referencia de clases CSS](plp-styling.md#css-classes).

**Q: ¿Afectará esto mi rendimiento de búsqueda?**

R: El widget PLP está diseñado para ser funcional. La mayoría de los comerciantes ven un rendimiento igual o mejor. Los catálogos grandes deben probarse en el entorno de ensayo.
