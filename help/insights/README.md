---
title: Administración de documentación de Commerce
description: 'Obtenga información acerca del modelo de gobernanza interna para Commerce Insights. No se publica en Experience League: se mantiene fuera de TOC.md intencionadamente.'
source-git-commit: 1da6d9753acbeadf3a0df5fae86a9386643c6d6d
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Gobernanza de documentación de Commerce

Esta es una referencia interna del equipo de documentación. No aparece en `TOC.md`, por lo que no se ha creado ni publicado en Experience League. Manténgalo aquí para que permanezca cerca del contenido que controla.

## Propiedad

Los artículos de Commerce Insights son propiedad del autor o equipo de publicación, que es responsable de mantener la precisión y la actualidad del artículo. Estos artículos se encuentran hospedados actualmente en el repositorio `commerce.en`. El equipo de documentación de Commerce ayuda a garantizar la calidad del contenido y a publicar el artículo en producción.

## Qué pertenece a Commerce Insights

- **Pertenece a este sitio**: Directrices estratégicas y documentos técnicos para soluciones de Commerce que abarcan instrucciones de implementación basadas en escenarios reales. Incluya vínculos a páginas de documentación de Commerce relevantes para obtener asistencia.

- **Pertenece al repositorio de productos**: configuración paso a paso, tutoriales, material de referencia (referencia de API/CLI/config) y solución de problemas. Si una publicación empieza a acumular ese tipo de detalles, muévala a la guía del producto correspondiente y vincúlala a ella.

## Adición de nuevo contenido

Cree un ticket COMDOX JIRA para que se publique el artículo. Copie `[templates/comdox-intake-template.md](templates/comdox-intake-template.md)` en la descripción del vale y rellénela; pide al solicitante que identifique la audiencia, marque si el contenido es temporal (con fecha de caducidad) y confirme que pertenece a la Guía de perspectivas y no a la documentación del producto de Commerce.

Una vez creado el ámbito del vale, inicie el artículo desde una plantilla en `templates/` (`whitepaper-template.md`, `security-guidance-template.md`, `insight-perspective-template.md`; sin publicar, copie el artículo correspondiente en el archivo de destino y elimine los comentarios del marcador de posición de la plantilla). Agregue una entrada `TOC.md` una vez que el contenido esté listo para publicarse.

- **La nueva sección de nivel superior** (por ejemplo, Información > Administración de catálogos) requiere revisión de IA antes de agregarla, ya que cambia la forma de exploración de la guía. Conéctese a la persona que posea la revisión de Commerce IA para ver la historia o la tarea.

- **Agregar al índice**: agregue un nuevo tema al índice antes de publicar. Si es necesario, utilice Ocultar metadatos para publicar un artículo oculto accesible solo para las personas que tengan el vínculo. Consulte [Ocultar contenido](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/hiding-files) en la Guía del autor de ExL.

## Revisar cadencia

Revise el contenido del artículo cuando se cambien de nombre o se actualicen las nuevas soluciones de Commerce o cuando las perspectivas ya no sean relevantes.
