---
title: Responsabilidad compartida
description: Conozca las responsabilidades de seguridad de cada parte involucrada en su proyecto de Adobe Commerce as a Cloud Service.
role: Admin, Architect, Leader
source-git-commit: 19c49b2b9d630898353addd778e062d3208505c1
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---


# Modelo operativo y de seguridad de responsabilidad compartida

Adobe Commerce as a Cloud Service es un servicio bajo demanda que se basa en un modelo operativo y de seguridad de responsabilidad compartida. Estas responsabilidades las comparten Adobe y los clientes. Cada parte tiene la responsabilidad distinta de proteger y operar la aplicación de Adobe Commerce.

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
| Aplicación de parches a servicios de soporte (por ejemplo, Nginx o MySQL) | RA | |
| Definición de reglas WAF de origen back-end | RA | |
| Definición de reglas de WAF de CDN back-end | RA | |
| Implementación de reglas WAF de plataforma back-end | RA | |
| Implementación de reglas WAF de CDN back-end | RA | |
| Corrección de errores principales en Adobe Commerce as a Cloud Service | RA | I |
| Lanzamiento de parches de infraestructura de Adobe Commerce as a Cloud Service | RA | |
| Escalado (infraestructura) | RA | |
| Escala (aplicación principal) | RA | |
| Integración de aplicaciones externas | | RA |
| Instalación de aplicaciones de App Builder | | RA |
| Prueba del rendimiento de todas las aplicaciones de App Builder | | RA |
| Temática y diseño de aplicaciones de App Builder personalizadas | | RA |
| Configuración del DNS back-end | RA | I |
| Incorporación de CDN back-end | RA | I |
| Compatibilidad con CDN back-end | RA | I |
| Obtención de un proveedor DNS back-end | RA | |
| Aprovisionamiento de los entornos de producción y de zona protegida | A | R |
| Acceso a Dynamics for Adobe Commerce en la infraestructura en la nube | R | C |
| Solución de problemas de seguridad del cliente back-end | RA | I |
| Solución de problemas de seguridad de CDN back-end | RA | |
| Asistencia a Adobe en la investigación de seguridad (análisis/auditorías) | RA | |
| Realización de exploraciones ASV PCI | RA | I |
| Remediación de exploraciones PCI de infraestructura de Adobe Commerce | R | |
| Administración de secretos de plataforma y sistema operativo | RA | |
| Supervisión de registros de seguridad back-end | RA | |
| Control de la asistencia al cliente y acceso | A | R |
| Pruebas y documentación anuales del plan de recuperación ante desastres de Adobe, así como de las copias de seguridad y restauración | RA | |
| Pruebas y documentación anuales del plan de recuperación ante desastres | RA | |
| Depuración y aislamiento de problemas | R | R |
| Compatibilidad oportuna con la depuración y el proceso de aislamiento de problemas | R | R |
| Publicación de actualizaciones y parches en Adobe Commerce Core | RA | I |
| Instalación de actualizaciones y parches en Adobe Commerce Core | RA | I |
| Calidad de aplicación principal de Adobe Commerce | RA | |
