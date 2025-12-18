---
title: Servicio RAG de documentación
description: Aprenda a utilizar el servicio de búsqueda de documentación con tecnología de IA para el desarrollo de Adobe Commerce.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 28396828516645abec3b42a2c6874afe9134dfb8
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# Servicio de documentación de RAG (Beta)

>[!NOTE]
>
>El servicio RAG de documentación está actualmente en Beta y la experiencia está sujeta a cambios.

El servicio de documentación RAG (Retrieval-Augmented Generation) proporciona funciones de búsqueda semánticas basadas en IA para la documentación de Adobe Commerce y App Builder.

Este RAG proporciona una interfaz IDE para hacer preguntas sobre Adobe Commerce y puede aconsejarle sobre las prácticas recomendadas para desarrollar aplicaciones y otras tareas de migración.

El servicio RAG forma parte del servidor [Commerce extensibility tools](./coding-tools.md) MCP (Model Context Protocol), que se integra con el cursor y otros asistentes de IA compatibles con MCP.

## Documentación disponible

En la tabla siguiente se describe qué documentación está indexada actualmente por el servicio RAG y las palabras clave que puede utilizar para almacenar en déclencheur la búsqueda en el índice asociado. La documentación incluida seguirá ampliándose a medida que desarrollemos el servicio RAG.

| Categoría | Índice | Contenido incluido | Palabras clave |
|-------|---------|---------|------------------------|
| [Tienda](https://experienceleague.adobe.com/developer/commerce/storefront/) | commerce-storefront-docs | Edge Delivery Services, complementos, componentes de tienda | tienda, lista desplegable, EDS, lista de productos, cierre de compra |
| [Extensibilidad](https://developer.adobe.com/commerce/extensibility/) | commerce-extensibility-docs | Webhooks, eventos, extensiones, integraciones | webhook, evento, extensión, API mesh, GraphQL |
| [Commerce](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview) | commerce-core-docs | Commerce principal (catálogo, clientes, pedidos) | catálogo, producto, cliente, pedido, inventario |
| [App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/) | app-builder-docs | App Builder, acciones en tiempo de ejecución, extensiones de IU | creador de aplicaciones, acción de tiempo de ejecución, React Spectrum |

Para obtener más información sobre la selección de índices, consulte [Selección automática de índices](#automatic-index-selection-recommended) y [Selección explícita de índices](#explicit-index-selection).

Para obtener información detallada sobre la documentación incluida en cada índice, consulte la [lista de fuentes ingeridas](https://github.com/adobe-commerce/azure-commerce-documentation-agent/blob/develop/docs/INGESTED_SOURCES.md).

## Seguridad y privacidad

* **Autenticación IMS**: todas las llamadas a la API utilizan tokens OAuth2 de Adobe IMS.
* **Sin almacenamiento de datos**: el servidor MCP no almacena credenciales ni datos.
* **Ejecución local**: todas las herramientas se ejecutan localmente en el equipo.
* **Comunicación segura**: la búsqueda en la documentación usa HTTPS con validación de tokens.

El extremo de producción está protegido por [Azure Front Door](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview), que incluye las siguientes protecciones:

* Firewall de aplicaciones web (WAF) con conjunto de reglas predeterminado de Microsoft 2.1 y conjunto de reglas de Bot Manager 1.0
* Bloqueo geográfico para regiones sujetas a embargo por Estados Unidos (Cuba, Irán, Corea del Norte, Siria, Crimea, Luhansk, Donetsk)
* Protección DDoS en el borde
* Servidor de administración de API bloqueado para aceptar solo el tráfico de la puerta principal

Para diferentes requisitos de seguridad, puede utilizar un punto de conexión personalizado. Consulte [Extremo personalizado de la puerta principal](#custom-front-door-endpoint) para obtener más información.

## Requisitos previos

Antes de instalar, asegúrese de que dispone de lo siguiente:

* [Node.js](https://nodejs.org/en/download){target="_blank"} 18+ (se recomienda LTS)
* [IDE de cursor](https://cursor.com/download){target="_blank"} (recomendado) u otro IDE compatible con MCP

  >[!NOTE]
  >
  >Aunque se admiten otros IDE compatibles con MCP, Cursor es el IDE recomendado para obtener la mejor experiencia. Si está utilizando otro IDE, deberá modificar las solicitudes y otros pasos de la documentación para que funcionen con el IDE seleccionado.

## Instalación

1. Instalar [Adobe I/O CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/) globalmente:

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Autenticar con Adobe IMS:

   ```bash
   aio auth login
   ```

1. Clone el repositorio de herramientas de extensibilidad de Commerce y vaya al directorio:

   ```bash
   git clone https://github.com/adobe-commerce/commerce-extensibility-tools.git
   cd commerce-extensibility-tools
   ```

1. Instalar dependencias:

   ```bash
   npm install
   ```

1. Cree o actualice `.cursor/mcp.json` en el directorio de proyectos de Commerce (no globalmente) para incluir el servidor MCP `commerce-extensibility-tools`:

   ```json
   {
     "mcpServers": {
       "commerce-extensibility-tools": {
         "command": "node",
         "args": [
           "/<your-project-directory>/commerce-extensibility-tools/index.js"
         ],
         "env": {
           "NODE_ENV": "production"
         }
       }
     }
   }
   ```

   Asegúrese de reemplazar `<your-project-directory>` con la ruta real donde clonó el repositorio.

   >[!NOTE]
   >
   >En Windows, si encuentra problemas al proporcionar la ruta al directorio del proyecto, consulte [Resolución de problemas de ruta](#path-issues-windows).

1. Reinicie el IDE del cursor para cargar el servidor MCP.

1. Compruebe la instalación preguntando al asistente de IA:

   ```shell-session
   Can you show me the available Adobe Commerce tools?
   ```

## Uso

Una vez instalado, puede llamar a los índices [automáticamente](#automatic-index-selection-recommended) o [explícitamente](#explicit-index-selection). También puede usar el comando [`/search-commerce-docs` ](#command-based-search).

>[!NOTE]
>
>El servicio RAG devuelve los 5 resultados más relevantes.

### Selección automática de índices (recomendado)

Al hacer preguntas en lenguaje natural sobre su proyecto de Commerce, la herramienta buscará automáticamente el índice de documentación adecuado y proporcionará información relevante:

>[!BEGINSHADEBOX]

El siguiente mensaje selecciona automáticamente el índice `commerce-storefront-docs`:

```shell-session
"How do I use Edge Delivery Services drop-ins for product listing?"
```

El siguiente mensaje selecciona automáticamente el índice `commerce-extensibility-docs`:

```shell-session
"How do I create a webhook in Adobe Commerce?"
```

El siguiente mensaje selecciona automáticamente el índice `commerce-core-docs`:

```shell-session
"How to configure product catalog settings?"
```

El siguiente mensaje selecciona automáticamente el índice `app-builder-docs`:

```shell-session
"What are App Builder runtime action best practices?"
```

>[!ENDSHADEBOX]

### Selección de índice explícita

También puede especificar el índice que desee utilizar en el mensaje.

```shell-session
Search commerce-storefront-docs for authentication drop-in
```

```shell-session
Using app-builder-docs, how do I deploy runtime actions?
```

### Búsqueda basada en comandos

Si desea asegurarse de que se utiliza el servicio RAG, puede invocar manualmente el comando Cursor `/search-commerce-docs` para buscar documentación con el símbolo del sistema:

```shell-session
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## Extremo personalizado de la puerta delantera

De manera predeterminada, la búsqueda de documentación usa el extremo de producción [Azure Front Door](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview) con protección WAF. Para fines de prueba o desarrollo, puede anular esto con la variable de entorno `FRONT_DOOR_URL`.

Para utilizar un punto de conexión personalizado, agréguelo a la configuración de MCP de cursor:

```json
{
  "mcpServers": {
    "commerce-extensibility-tools": {
      "command": "node",
      "args": ["/<your-project-directory>/commerce-extensibility-tools/index.js"],
      "env": {
        "NODE_ENV": "production",
        "FRONT_DOOR_URL": "https://<custom-endpoint>.azurefd.net"
      }
    }
  }
}
```

>[!NOTE]
>
>La mayoría de los desarrolladores deben utilizar el extremo de producción predeterminado y no necesitan establecer la variable `FRONT_DOOR_URL`.

## Resolución de problemas

En las siguientes secciones se proporcionan sugerencias para la resolución de problemas comunes que podrían producirse al utilizar el servicio RAG de documentación.

### Errores de autenticación

La herramienta de búsqueda de documentación requiere la autenticación IMS de Adobe. Si encuentra errores de autenticación, siga los siguientes pasos para solucionar el problema.

1. Compruebe que ha iniciado sesión:

   ```bash
   aio where
   ```

1. Compruebe que puede ver el token de IMS:

   ```bash
   aio auth login --bare
   ```

1. Si persisten los errores de autenticación, intente cerrar la sesión y volver a iniciarla:

   ```bash
   aio auth logout
   aio auth login
   ```

### El servidor MCP no se carga

Si el servidor MCP no se está conectando, o si el agente indica que no se puede conectar al RAG, siga los siguientes pasos para solucionar el problema.

1. Abra la configuración del cursor usando **Cmd ,** (macOS) o **Ctrl ,** (Windows y Linux).

1. Busque &quot;MCP&quot; y verifique que `commerce-extensibility-tools` esté en la lista y habilitado.

1. Compruebe si hay mensajes de error en el panel de configuración de MCP.

1. Compruebe que el archivo `mcp.json` existe en el proyecto:

   ```bash
   cat .cursor/mcp.json
   ```

1. Compruebe que la ruta sea correcta y absoluta:

   ```bash
   ls -la /<your-project-directory>/commerce-extensibility-tools/index.js
   ```

### Herramienta no encontrada

1. Salga del cursor y vuelva a abrirlo.

1. Compruebe los registros del servidor MCP en la consola del desarrollador del cursor usando **Cmd+Shift+P** (macOS) o **Ctrl+Mayús+P** (Windows/Linux) y buscando &quot;Desarrollador: Abrir carpeta de registros&quot;.

1. Compruebe la instalación:

   ```bash
   cd commerce-extensibility-tools
   npm install
   node index.js
   ```

   El servidor debe iniciarse sin errores.

### Problemas de ruta (Windows)

En Windows, use las barras diagonales `/` o las barras invertidas de escape `\\`:

```json
{
  "args": ["C:/Users/yourname/projects/commerce-extensibility-tools/index.js"]
}
```

```json
{
  "args": ["C:\\Users\\yourname\\projects\\commerce-extensibility-tools\\index.js"]
}
```

## Recursos adicionales

* [Documentación para desarrolladores de Adobe Commerce](https://developer.adobe.com/commerce/docs/){target="_blank"}
* [Documentación de App Builder](https://developer.adobe.com/app-builder/docs/){target="_blank"}
* [Protocolo de contexto de modelo](https://modelcontextprotocol.io/){target="_blank"}
* [IDE de cursor](https://cursor.sh/docs){target="_blank"}
