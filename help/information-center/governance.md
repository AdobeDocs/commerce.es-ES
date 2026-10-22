---
title: Administración del centro de información de Commerce
description: Obtenga información acerca del modelo de gobernanza interna para el Centro de información de Commerce. No publicado en Experience League.
source-git-commit: a91925091da28cd0745923894a3faab0374f0a0c
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%
---

# Gobernanza del Centro de información de Commerce

Esta referencia interna para el equipo de documentación no aparece en `TOC.md`, por lo que no se ha publicado en Adobe Experience League.

## Propiedad

El Centro de información pertenece al equipo de documentación de Adobe Commerce. Se creó en `Adobe-Enterprise-Docs/commerce.en`, el repositorio mostrado como `git-repo` en `metadata.md`.

No es de propiedad de ningún equipo de producto único porque se trata de un producto cruzado. Envíe correcciones específicas del producto al contacto de documentos del equipo de productos propietario en lugar de corregirlas aquí.

## Qué pertenece al Centro de información

| Pertenece aquí | Pertenece al repositorio de productos |
| --- | --- |
| Contenido que abarca más de un producto o servicio, como directrices de selección de productos, recorridos de implementación entre productos, patrones arquitectónicos y documentos técnicos | Contenido de un solo producto, como configuración paso a paso, referencia de API/CLI/config y solución de problemas |
| Páginas de revisión cortas que se vinculan a documentos de productos autorizados | |

- Si una página de aquí acumula detalles de un solo producto, muévala a la guía del producto y vincúlala.
- El Centro de información no consolida ni migra la documentación del producto ni documenta las funciones individuales del producto. Vincule a contenido autorizado existente antes de escribir algo nuevo.

## Adición de nuevo contenido

### Artículos de una sección existente

1. Agregue el archivo a la carpeta que coincida con la sección.
1. Agregue una entrada a `TOC.md` en esa sección.

No se requiere aprobación más allá de la revisión PR normal.

| sección del índice | Carpeta |
| --- | --- |
| Explorar las plataformas y servicios de Commerce | `portfolio/`, `storefronts/`, `aem-assets/`, `apis/` |
| Introducción por función | `get-started/` |
| Perspectivas y directrices | `guidance-and-insights/` |
| Arquitectura | `architecture-options/` |
| Migración y adopción | `migration-adoption/` |
| Guías de implementación | `implementation-guides/` |

### Artículos de información y orientación

1. Copiar `whitepaper-template.md` o `security-guidance-template.md` de `guidance-and-insights/templates/` en `guidance-and-insights/`. Las plantillas no se publican. Para ver el proceso de creación completo, incluido el ticket de admisión COMDOX, consulte [readme.md](guidance-and-insights/readme.md).
1. Elimine los comentarios de marcador de posición de la plantilla.
1. Agregue una entrada `TOC.md` en Información e instrucciones cuando el contenido esté listo para publicarse.

### Secciones de nivel superior

Un nuevo grupo de nivel superior de `TOC.md` cambia la navegación de la guía, por lo que requiere una revisión de IA. Póngase en contacto con el propietario de la revisión de Commerce IA. Reutilice primero una sección existente, como Introducción por función para contenido de socio o de habilitación.

### URL publicadas

Las direcciones URL se crean a partir del identificador de guía, los identificadores de sección de `TOC.md` (por ejemplo, `{#insights-and-guidance}`) y el nombre de archivo. Los nombres de las carpetas no aparecen en la dirección URL. Asigne a cada sección un ID único y asegúrese de que dos artículos se resuelvan en la misma dirección URL.

## Revisar cadencia

- **Impulsado por eventos**: revise las secciones Explorar plataformas y servicios de Commerce, Introducción por función, Arquitectura, Migración y adopción y Guías de implementación cuando se cambie el nombre de un producto de Commerce, cuando este se inicie o quede obsoleto, o cuando cambie su disponibilidad. Por ejemplo, revíselos si Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer se integran. Primero, estas páginas quedan obsoletas.
- **Programado**: para detectar inexactitudes técnicas, de marca o terminología obsoleta, ejecute una auditoría de contenido automatizada y revise la información cada seis meses.

## Relación con la ayuda/aterrizaje/

`help/landing/` (&quot;Guías de servicios de Adobe Commerce&quot;) es una guía independiente que no forma parte del Centro de información. Se centra en servicios de Commerce como el servicio de catálogo, Live Search, recomendaciones de productos y servicios de pago, y el centro de información se vincula a ellos para obtener más detalles. El replanteamiento o la consolidación de ambos es una decisión de seguimiento que esta guía no resuelve.
