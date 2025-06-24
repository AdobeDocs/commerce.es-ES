---
title: Responsabilidad compartida
description: Conozca las responsabilidades de seguridad de cada parte involucrada en su  [!DNL Adobe Commerce Optimizer] proyecto.
role: Admin, Architect, Leader
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 7c407bfc2becfb0ba6babe5958bcb790c178f406
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Modelo operativo y de seguridad de responsabilidad compartida

>[!BEGINSHADEBOX]

Las siguientes tablas de resumen utilizan el modelo RACI para mostrar las responsabilidades de seguridad compartidas entre Adobe y los clientes.

**R** — Responsable
**A** — Responsable
**C** — Consultado
**I** — Informado

>[!ENDSHADEBOX]

| Tarea | Adobe | Cliente |
| --- | --- | --- |
| Aplicación de parches de infraestructura de Adobe Commerce | RA | |
| Aplicación de parches a servicios de soporte | RA | |
| Definición de reglas WAF de origen back-end | RA | |
| Definición de reglas de WAF de CDN back-end | RA | |
| Implementación de reglas WAF de plataforma back-end | RA | |
| Implementación de reglas WAF de CDN back-end | RA | |
| Corrigiendo errores en [!DNL Adobe Commerce Optimizer] | RA | I |
| Publicando [!DNL Adobe Commerce Optimizer]parches de infraestructura | RA | |
| Escalado (infraestructura) | RA | I |
| Integración de aplicaciones externas | | RA |
| Instalación de aplicaciones de App Builder | | RA |
| Prueba del rendimiento de todas las aplicaciones de App Builder | | RA |
| Temática y diseño de aplicaciones de App Builder personalizadas | | RA |
| Configuración del DNS back-end | RA |  |
| Incorporación de CDN back-end | RA |  |
| Compatibilidad con CDN back-end | RA |  |
| Obtención de un proveedor DNS back-end | RA | |
| Aprovisionamiento de los entornos de producción y de zona protegida | A | R |
| Acceso a Dynamics para Adobe Commerce Optimizer | R | C |
| Solución de problemas de seguridad del cliente back-end | RA | I |
| Solución de problemas de seguridad de CDN back-end | RA | |
| Asistencia a Adobe en la investigación de seguridad (análisis/auditorías) | RA | |
| Realización de exploraciones ASV PCI | RA | I |
| Remediación de exploraciones PCI de infraestructura de Adobe Commerce Optimizer | R | |
| Administración de secretos de plataforma y sistema operativo | RA | |
| Supervisión de registros de seguridad back-end | RA | |
| Control de la asistencia al cliente y acceso | A | R |
| Pruebas y documentación anuales del plan de recuperación ante desastres de Adobe, así como de las copias de seguridad y restauración | RA | |
| Pruebas y documentación anuales del plan de recuperación ante desastres | RA | |
| Depuración y aislamiento de problemas | R | R |
| Compatibilidad oportuna con la depuración y el proceso de aislamiento de problemas | R | R |
| Instalación de actualizaciones y parches en Adobe Commerce Optimizer | RA | I |
| Calidad de aplicación principal de Adobe Commerce Optimizer | RA | |
