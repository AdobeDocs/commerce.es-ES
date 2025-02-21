---
title: Verificar colección de eventos
description: Obtenga información sobre cómo comprobar que los datos de comportamiento se envían a Adobe Commerce.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# Verificar colección de eventos

Después de [instalar y configurar](install-configure.md) el módulo `magento/product-recommendations`, puede comprobar que los datos de comportamiento se envían a Adobe Commerce. Puede utilizar las herramientas para desarrolladores disponibles en Chrome o instalar la extensión Snowplow Chrome. Si necesita ayuda adicional, consulte [Solucionar problemas [!DNL Product Recommendations] módulo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce.html) en la Base de conocimiento de asistencia.

## Verificación mediante herramientas para desarrolladores en Chrome

Para asegurarse de que el archivo JS del recopilador de eventos se está cargando en todas las páginas del sitio:

1. En Chrome, elija **Personalizar y controlar Google Chrome** y, a continuación, seleccione **Más herramientas** > **Herramientas para desarrolladores**.
1. Elija la pestaña **Red** y luego seleccione el tipo **JS**.
1. Filtrar por `ds.`
1. Vuelva a cargar la página.
1. Debería ver `ds.js` o `ds.min.js` en la columna **Nombre**.

![Recopilador de eventos JS](assets/filter-ds.png)
_Recopilador de eventos JS_

Para asegurarse de que los eventos se activan en las páginas de su sitio (inicio, producto, cierre de compra, etc.):

1. Asegúrese de desactivar cualquier bloqueador de anuncios en su navegador y aceptar las cookies en el sitio.
1. En Chrome, elija **Personalizar y controlar Google Chrome** (los tres puntos verticales en la esquina superior derecha del explorador) y, a continuación, seleccione **Más herramientas** > **Herramientas para desarrolladores**.
1. Elija la ficha **Red** y filtre para `tp2`.
1. Vuelva a cargar la página.
1. Debería ver las llamadas en `tp2` en la columna **Nombre**.

![Desencadenando eventos](assets/filter-tp2.png)
_Compruebe que se están activando eventos_

## Verificar con la extensión Snowplow Chrome

Instale la extensión [Snowplow Analytics Debugger para Chrome](https://chrome.google.com/webstore/detail/snowplow-analytics-debugg/jbnlcgeengmijcghameodeaenefieedm). Esta extensión muestra los eventos que se recopilan y envían a Adobe Commerce.

1. Asegúrese de desactivar cualquier bloqueador de anuncios en su navegador y aceptar las cookies en el sitio.

1. En Chrome, elija **Personalizar y controlar Google Chrome** (los tres puntos verticales en la esquina superior derecha del explorador) y, a continuación, seleccione **Más herramientas** > **Herramientas para desarrolladores**.

1. Elija la pestaña **Snowplow Analytics Debugger**.

1. En la columna **Evento**, seleccione **Evento estructurado**.

1. Desplácese hacia abajo hasta que vea **Datos de contexto _n_**. Busque la instancia de tienda en el **Esquema**.

1. Compruebe que el [ID de espacio de datos SaaS](https://experienceleague.adobe.com/docs/commerce-admin/config/services/saas.html) esté configurado correctamente.

![Filtro Snowplow](assets/snowplow-filter.png)
_Filtro Snowplow_

>[!NOTE]
>
> El valor `Data validity : NOT FOUND` en Debugger indica un esquema interno. El complemento Snowplow Chrome no puede validar los eventos con un esquema interno. Esto no afecta a la funcionalidad real.

## Compruebe que los eventos se activan correctamente

Para comprobar que los eventos utilizados para las métricas se activan correctamente, busque los eventos `impression-render`, `view` y `rec-click` en Snowplow Analytics Debugger. Ver la [lista completa de eventos](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/events.html).

>[!NOTE]
>
> Si el [Modo de restricción de cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html) está habilitado, Adobe Commerce no recopilará datos de comportamiento hasta que el comprador dé su consentimiento. Si el modo de restricción de cookies está desactivado, los datos de comportamiento se recopilan de forma predeterminada.
