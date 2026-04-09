---
title: Iniciar lista de comprobación
description: Obtenga información sobre cómo validar la configuración, la tienda, la SEO, la CDN, las integraciones, la seguridad, el análisis y las pruebas para la producción de  [!DNL Adobe Commerce Optimizer] .
solution: Commerce
feature: Integration, Storefront, Search, Catalog Management, Personalization
feature-set: Commerce
role: Admin, Developer
level: Intermediate
topic: Administration
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
source-git-commit: 37b8b8a334ca11daacfd3da03b0441e77329e2e1
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 0%

---


# Iniciar lista de comprobación

Utilice esta lista de comprobación para comprobar que el proyecto de producción [!DNL Adobe Commerce Optimizer] está configurado, probado y listo para su lanzamiento. Trabaje en cada sección con su equipo y realice un seguimiento de la finalización en su propio plan de proyecto o rastreador. Para obtener las funcionalidades del producto y las áreas de IU a las que se hace referencia a continuación, consulte la [[!DNL Adobe Commerce Optimizer] documentación](../overview.md).

## Caso de uso y arquitectura {#use-case}

Utilice esta lista de comprobación cuando ofrezca una experiencia B2C que combine [!DNL Adobe Commerce Optimizer] y Edge Delivery Services (EDS) con una instancia de Adobe Commerce en la nube existente.

La solución suele incluir estos componentes:

- **Cloud**: Adobe Commerce en Cloud administra los datos del catálogo, los clientes, los activos y los flujos de compra (cierre de compra, administración de pedidos, envío, etc.).
- **Optimizer**—[!DNL Adobe Commerce Optimizer] ofrece experiencias de comercialización.
- **Tienda**: Adobe Commerce Storefront en Edge Delivery Services proporciona la interfaz de usuario.
- **Servicios de terceros**: proveedores de pago, envío e impuestos.
- **App Builder**: extensibilidad.
- **Mesh de API**: Solicitar enrutamiento.

## Verificar Adobe Commerce en la nube {#verify-cloud}

Confirme que su entorno de Adobe Commerce en la nube está listo para la producción.

▢: La instancia de nube está [aprovisionada](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/start/new-project).
▢: los datos de prueba y ficticios se han eliminado de la instancia.
▢ Los datos de producción se han cargado en la instancia.
▢ Usted conoce el [extremo de GraphQL](https://developer.adobe.com/commerce/webapi/graphql/).
▢: la instancia cumple los requisitos de [lista para el lanzamiento](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/launch/checklist).

## Verificar instancia de Commerce Optimizer {#verify-optimizer}

Confirme que la instancia de producción [!DNL Adobe Commerce Optimizer] esté configurada correctamente.

▢: la instancia de producción está activa. Consulte [Introducción](../get-started.md) para saber cómo aprovisionarlo.
▢: la instancia se encuentra en la región correcta.
▢: el tipo de entorno es Producción.
▢: conoce el ID de organización, el ID de cliente, la URL de ingesta y la URL de Commerce Optimizer. Consulte [Introducción](../get-started.md).
▢ Los límites y limitaciones configurados coinciden con los valores confirmados por el asesor técnico del cliente de Adobe (CTA).
▢ Se han eliminado de la instancia los artefactos de prueba y los datos de prueba.

## Verificar sitio de tienda {#verify-storefront-site}

Confirme que el sitio de tienda de Edge Delivery Services existe y que el acceso está restringido.

▢: el sitio de tienda existe. Ver [Crear una tienda](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/).
▢ Usted conoce el nombre del sitio.
▢ Solo las personas autorizadas tienen [permiso para publicar](https://tools.aem.live/tools/user-admin/index.html).
▢ Solo las personas autorizadas tienen [permiso para crear](https://docs.da.live/administrators/guides/permissions).

## Verificar la integración de Cloud y Optimizer {#cloud-optimizer-integration}

Confirme que Adobe Commerce en la nube y [!DNL Adobe Commerce Optimizer] intercambian datos correctamente.

### En Adobe Commerce

Complete estas comprobaciones en el proyecto de Cloud.

▢: el conector Commerce Optimizer está [instalado y configurado](../../aco-connector/get-started.md).
▢ El comando CLI `aco:conf:show` confirma la conexión con la instancia de producción de Commerce Optimizer. El ID de organización, el ID de cliente, la URL de ingesta y la URL de Commerce Optimizer coinciden con la producción.
▢ Los ámbitos de sincronización de [Exportar configuración](../../aco-connector/get-started.md) coinciden con sus requisitos.
▢ [Estado de sincronización de fuentes de datos](../../aco-connector/get-started.md) confirma la exportación de datos desde la instancia de Cloud.

### En Commerce Optimizer

Complete estas comprobaciones en la IU de [!DNL Adobe Commerce Optimizer].

▢: el [panel de sincronización de datos](../setup/data-sync.md) muestra los datos recibidos. Los productos, precios y atributos aparecen para Servicio de catálogo, Descubrimiento de productos y Recomendaciones.
▢ [Los libros de precios](../setup/pricebooks.md) se crean automáticamente a partir de los grupos de clientes en la nube.
▢ [Existen vistas de catálogo](../setup/catalog-view.md) y usted conoce sus identificadores.
▢ [Políticas](../setup/policies.md) existen y usted conoce sus ID.
Se han configurado ▢ [facetas](../merchandising/facets/overview.md).
▢ [Sinónimos](../merchandising/synonyms/overview.md) configurados.
▢ [reglas de comercialización](../merchandising/rules/overview.md) configuradas.
▢ [El facetado de precios y el idioma de búsqueda](../settings.md) coinciden con sus requisitos cuando utiliza esas características.
▢ [Las recomendaciones de productos](../merchandising/recommendations/create.md) existen y se comportan según lo esperado en la vista previa.
▢ [Los datos de rendimiento de búsqueda](../manage-results/search-performance.md) aparecen en *Admin*.
▢ [Los datos de rendimiento de Recommendations](../manage-results/recommendation-performance.md) aparecen en el *Administrador*.

## Verificar la integración de tienda y nube {#storefront-cloud-integration}

Confirme que la tienda lee el punto de conexión correcto de Adobe Commerce GraphQL.

### En Adobe Commerce

▢ paquetes de compatibilidad de tienda están [instalados](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/).

### En la tienda

▢: la configuración de la tienda `commerce-core-endpoint` apunta a tu [extremo de Cloud GraphQL](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/).
▢ Si utiliza API Mesh como proxy para Cloud GraphQL, `commerce-core-endpoint` señala al extremo de API Mesh en lugar del extremo de Cloud GraphQL.

## Verificar la integración de Storefront y Optimizer {#storefront-optimizer-integration}

Confirme la configuración de Commerce Optimizer en la configuración de la tienda.

▢ Tu tienda usa la [configuración de Commerce Optimizer](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/) correcta.
▢ `adobe-commerce-optimizer` es `true`.
▢ `commerce-endpoint` señala al extremo de producción de Commerce Optimizer GraphQL o al extremo de API Mesh cuando utiliza API Mesh.
▢ `headers.cs.AC-view-ID` contiene el identificador de vista de catálogo de su instancia de producción de Commerce Optimizer.

## Verificar servicios de terceros en la nube {#third-party-services}

Confirme las integraciones que se ejecutan en el sistema de comercio del host (no en [!DNL Adobe Commerce Optimizer]).

▢ **Pagos:** La puerta de enlace de pago está activa y probada (Stripe, PayPal, Adyen, etc.).
▢ **Envío:** Las conexiones de la API de envío funcionan (UPS, FedEx, etc.).
▢ **Envío:** La plataforma de cumplimiento está conectada y probada (por ejemplo, ShipStation).
▢ **Impuesto:** Se ha validado la integración del cálculo de impuestos (Avalara, TaxJar, etc.).
▢ **Impuesto:** La sincronización de software de contabilidad funciona (QuickBooks, etc.).
▢ **Inventario:** Se ha probado y sincronizado la integración de PIM, ERP o administración de inventario.
▢ **Arquitectura:** El sistema de comercio host administra el pago, el envío, los impuestos y el inventario (no [!DNL Adobe Commerce Optimizer]).
▢ **Arquitectura:** API Mesh y App Builder permanecen sincronizados entre el sistema de comercio del host y [!DNL Adobe Commerce Optimizer].
▢ **Correo electrónico:** La entrega por correo electrónico transaccional funciona (confirmación de pedido, envío, etc.).
▢ **Correo electrónico:** Las plantillas de correo electrónico coinciden con su marca y utilizan vínculos correctos.

## Verificar la malla de App Builder y API {#app-builder-mesh}

Confirme la configuración de extensibilidad para producción.

### App Builder

▢ El área de trabajo de producción incluye todas las configuraciones y servicios necesarios.
▢: la aplicación de producción pasa pruebas entre escenarios de compilación.
Se han revisado y confirmado ▢ límites y límites del producto según la [descripción del producto de Adobe Developer App Builder](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html){target="_blank"} y la [configuración y limitaciones del sistema App Builder](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings){target="_blank"}.
▢: la aplicación de producción utiliza extremos de producción de App Builder.
▢: las extensiones de panel *Admin* personalizadas se han implementado en el espacio de trabajo de producción.

### API Mesh

Las configuraciones y orígenes de ▢ están listos para la producción.

### Eventos

Se configuraron ▢ Adobe I/O Events y se verificaron las suscripciones.

## Finalizar experiencia de tienda {#finalize-storefront}

Contenido, SEO, rendimiento, seguridad y comportamiento de CDN polacos antes del lanzamiento.

### Contenido y creación

Confirme la creación de componentes de flujo de trabajo y tienda.

▢: se ha completado la revisión de la lista de comprobación de lanzamiento de [AEM/EDS](https://www.aem.live/docs/go-live-checklist).
▢: el origen de creación está basado en documentos o es Editor universal (y configurado).
▢ El contenido se ha publicado mediante el ciclo de vista previa → publicación.
▢ Se ha completado el control de calidad del contenido y el diseño en el dominio `.aem.live`.
▢ El sitio ha configurado y servido correctamente un icono de favoritos.
▢ da.live e imágenes de producto usan [configuradas](https://docs.da.live/administrators/guides/permissions) credenciales dedicadas.
▢ mensajes de inclusión (carrito, cierre de compra, PDP, PLP, autenticación, cuenta) se han [personalizado](../storefront.md) y se han probado.
▢ La marca de la tienda refleja tokens, tipografía y colores de diseño CSS.

### SEO e indexación

Confirme los metadatos, las direcciones URL y rastree el comportamiento.

▢ Los metadatos de título de documento están presentes para las páginas clave (especialmente PDP y PLP). Consulte [metadatos SEO](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} en la documentación de _Adobe Commerce Storefront_.
▢ PDP incluyen [metadatos y datos estructurados](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} (por ejemplo, JSON-LD).
Los formatos de URL del producto ▢ son coherentes (por ejemplo, `domain/product-name`).
▢ URL mnemónicas redirigen a URL canónicas.
▢ El proyecto incluye `robots.txt`, que permite la indización donde corresponda, hace referencia a mapas del sitio y bloquea las rutas de acceso que no desea indizar (por ejemplo, `/drafts`).
▢ [Los archivos de redireccionamiento](https://www.aem.live/docs/redirects) cubren los cambios de URL de la migración (por ejemplo, después de quitar `.html`).
▢ mapa del sitio existe y se envía a la consola de búsqueda de Google según sea necesario.
▢ URL canónicas devuelven el estado `2xx` (no `3xx` ni `4xx`).
▢ sitios multilingües incluyen etiquetas `hreflang` en el mapa del sitio.
▢: el informe de cobertura de la consola de búsqueda de Google está actualizado.

### Procesamiento previo

Confirme el procesamiento del lado del servidor donde lo habilita.

▢ La representación previa está activada para las páginas clave. Ver [Renderización previa para AEM](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-prerender/){target="_blank"} en la documentación de _Adobe Commerce Storefront_.
Las direcciones URL de ▢ están en minúsculas, por lo que el procesamiento previo no interrumpe los vínculos.
▢ El origen de HTML incluye metadatos y contenido del cuerpo que confirman que la representación previa funciona.
▢ configuraciones regionales muestran las páginas traducidas correctas donde corresponda.
▢ El marcado adicional de HTML está [configurado](https://www.aem.live/docs/redirects) según sea necesario.

### Rendimiento y monitorización

Confirme las líneas de base de rendimiento y el cableado de Analytics.

▢ Tu tienda sigue [las prácticas recomendadas de rendimiento](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/performance/){target="_blank"} en la documentación de _Adobe Commerce Storefront_.
▢ (opcional) Google Analytics y Google Tag Manager están configurados.
La implementación de ▢ [eventos de tienda](https://github.com/adobe/commerce-events/tree/main/examples/events/snowplow-debugger) es válida y los datos aparecen en los paneles de [!DNL Live Search] y [!DNL Product Recommendations] en Adobe Commerce *Admin*.
▢: el parámetro de análisis `environment` en la [configuración de Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/){target="_blank"} es `"Testing"` durante el desarrollo y `"Production"` en el lanzamiento. Consulte [Instrumentación de Analytics](https://experienceleague.adobe.com/developer/commerce/storefront/setup/analytics/instrumentation/){target="_blank"}.
▢ Las puntuaciones de Lighthouse cumplen con sus objetivos (por ejemplo, `100` en páginas clave) según las directrices de este tema.

### Seguridad y acceso

Confirme los permisos y secretos.

▢ Se han configurado los permisos adecuados para el contenido de DA y los sitios de EDS. Ver [DA.permisos activos](https://da.live/docs/administration/permissions) y [Configuración de autenticación para la creación](https://www.aem.live/docs/authentication-setup-authoring).
▢: se ha aprovisionado la integración de imágenes del producto. Consulte [Información general sobre el acceso a AEM Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview#).
▢ Los vínculos para restablecer la contraseña de las plantillas de correo electrónico coinciden con la configuración de Edge Delivery Services. Ver las preguntas frecuentes sobre la tienda: [¿Qué debo hacer si mis vínculos de plantillas de correo electrónico se rompen después de migrar a Edge Delivery Services o Helix?](https://experienceleague.adobe.com/developer/commerce/storefront/troubleshooting/faq/#what-should-i-do-if-my-email-template-links-are-broken-after-migrating-to-edge-delivery-services-or-helix){target="_blank"}.
▢: las claves de producción para las integraciones y los proveedores de pago ya están establecidas.
Los dominios de ▢ están incluidos en la lista de permitidos y funcionan los webhooks back-end.

### CDN y almacenamiento en caché

Confirme el comportamiento de CDN, DNS y caché.

▢: la configuración de CDN utiliza el extremo de GraphQL de producción (`yourproject.com/graphql`) para las extensiones y scripts de Sidekick (por ejemplo, la generación de mapas del sitio y el importador de imágenes).
▢ Cuando usa Adobe Commerce Fastly, hay disponible un token de purga de CDN y [la configuración del sitio](https://tools.aem.live/tools/cdn-setup/index.html) incluye `authToken` y `serviceId`.
▢ [La configuración de CDN](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/content-delivery-network/){target="_blank"} valida el almacenamiento en caché y la invalidación.
▢ Para [configuraciones de varias tiendas](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/indexing/#multi-store-setups){target="_blank"}, el servicio de catálogo y las solicitudes [!DNL Live Search] incluyen una eliminación de caché específica de la tienda (por ejemplo, un parámetro de consulta o una regla de CDN).
▢ La invalidación push funciona de extremo a extremo (publique un cambio y verifique en el dominio de producción).
▢ TTL de DNS es lo suficientemente bajo antes de la migración.
Los registros A y CNAME de DNS ▢ son correctos para todos los dominios y nombres de host.
▢: el certificado SSL/TLS se ha aprovisionado y verificado para el dominio de producción.
▢ `www` y las redirecciones de Apex se comportan correctamente.

## Seguridad y cumplimiento {#security-compliance}

Confirme la postura de seguridad y las tareas de cumplimiento.

▢ **SSL:** Hay instalado un certificado SSL/TLS de confianza.
▢ **SSL:** HTTPS se aplica en todo el sitio.
▢ **Acceso:** Se han cambiado las contraseñas predeterminadas de *Administrador* y se ha implementado una directiva de contraseñas segura. Ver [!DNL Adobe Commerce Optimizer] [Administración de usuarios e identidades](../user-management.md).
▢ **Acceso:** La dirección URL de *Admin* no es la predeterminada.
▢ **Acceso:** La autenticación de doble factor está habilitada para todos los usuarios de *Admin*.
▢ **Acceso:** Ningún usuario administrador inactivo o sin usar está asociado con el proyecto.
▢ **Firewall:** El firewall de aplicaciones web (WAF) está configurado y verificado.
▢ **PCI:** Las pruebas de penetración de seguridad en producción (ámbito PCI) han finalizado.
▢ **Análisis:** La herramienta de análisis de seguridad de Adobe está registrada y se ha completado un análisis inicial.
▢ **Acceso:** CORS solo permite orígenes aprobados.
▢ **Cumplimiento:** El [modelo de responsabilidad compartida](../shared-responsibility.md) para [!DNL Adobe Commerce Optimizer] está actualizado y define claramente Adobe en comparación con las responsabilidades del cliente.
▢ **Cumplimiento:** Se han verificado la política de privacidad, el consentimiento de cookies y los requisitos del RGPD o de la CCPA.

## Análisis y monitorización {#analytics-monitoring}

Confirmar medición y líneas de base.

▢ **RUM:** Real User Monitoring (RUM) está instrumentado para la comparación antes y después.
▢ **Analytics:** La recopilación de datos de Adobe Experience Platform está configurada (si corresponde).
▢ **Analytics:** Comprobó que las etiquetas de MarTech se activan en el nombre de host de producción.
▢ **Analytics:** Los análisis de línea de base están documentados; se esperan fluctuaciones después del inicio (vistas de página, tasa de salida hacia otro sitio, etc.).
▢ **Eventos:** El seguimiento de conversiones funciona de extremo a extremo (se agrega al carro → cierre de compra → confirmación).

## Pruebas {#testing}

Confirmar la calidad antes y después del lanzamiento.

▢ **Funcional:** Los flujos principales trabajan de extremo a extremo: busque → filtro de → de búsqueda → agregue al carro de compras → cierre de compra → creación de cuentas.
▢ **Funcional:** Las puertas de enlace de pago aceptan transacciones reales y de prueba.
▢ **Funcional:** Trabajo de colocación de pedidos, correo electrónico de confirmación y seguimiento de pedidos.
▢ **Funcional:** Las opciones de envío y los cálculos de impuestos son precisos.
▢ **Funcionales:** Los cupones, los descuentos y los programas de fidelidad se comportan según lo esperado.
▢ **UAT:** La prueba de aceptación del usuario se ha completado en el ensayo y la producción.
▢ **Rendimiento:** Las pruebas de carga y esfuerzo se han completado y Adobe CTA o CSE tienen los resultados.
▢ **Rendimiento:** El tiempo de carga de la página es inferior a tres segundos en equipos de escritorio y móviles.
▢ **Rendimiento:** Las puntuaciones de Lighthouse cumplen los objetivos en páginas clave (por ejemplo, a través de PageSpeed Insights).
▢ **Rendimiento:** Las imágenes, los scripts y los recursos están optimizados.
▢ **Compatibilidad:** Chrome, Firefox, Safari y Edge se comportan según lo esperado.
▢ **Compatibilidad:** Los diseños adaptables funcionan en dispositivos móviles, tabletas y de escritorio.
▢ **Compatibilidad:** El rendimiento es aceptable en 3G, 4G y Wi-Fi.
▢ **Accesibilidad:** Se ha completado una auditoría de accesibilidad (WCAG, lector de pantalla, navegación mediante el teclado).
▢ **Funcional:** Hay un plan de supervisión 404 posterior al lanzamiento.
▢ **UAT:** Existe un plan de reversión que pasa la prueba si se producen problemas de inicio.

## Día de lanzamiento y posterior al lanzamiento {#launch-post-launch}

Confirme las tareas de comunicación, asistencia y seguimiento.

▢ **Coordinación del inicio:** Adobe tiene su fecha de inicio confirmada; se ha notificado a CTA por correo electrónico.
▢ **Asistencia técnica:** El número de línea directa P1 está registrado: US (+1) 800-497-0335, luego presione 6 para Commerce.
▢ **Soporte técnico:** Su equipo está capacitado para abrir una incidencia de soporte técnico **antes de** llamar a la línea directa P1.
▢ **Lanzamiento posterior:** Compruebe las puntuaciones de Lighthouse en el dominio de producción.
▢ **Después del inicio:** supervise la consola de búsqueda de Google para detectar errores de indexación y rastrea.
▢ **Después del lanzamiento:** Supervise los informes 404 y agregue redirecciones para las URL heredadas de alto tráfico.
▢ **Después del lanzamiento:** Confirme los datos de MarTech y Analytics en la producción.
▢ **Después del inicio:** Pida a su CTA, CSE o AEM que habilite la supervisión de alto SLA.
▢: existe un plan de recuperación ante desastres y se superan las pruebas.
▢: existe un proceso para realizar el seguimiento y actualizar los paquetes de plantillas y extensiones a las versiones actuales.
