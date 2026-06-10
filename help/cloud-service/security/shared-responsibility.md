---
title: Responsabilidad compartida
description: Conozca las responsabilidades de seguridad de cada parte involucrada en su  [!DNL Adobe Commerce as a Cloud Service] proyecto.
feature: Cloud, Security
role: Admin, Developer, Leader
level: Intermediate
exl-id: 424fe5cd-5d54-425d-97ce-024476d18dde
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
TQID: 'https://experienceleague.adobe.com/ZjR9eFTVz8RIrYIN1CxyEgegGoZljXJKrtWZStx-ln0'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: ef32511703a96b5f4db32d54229e9a7cbe961f12
workflow-type: tm+mt
source-wordcount: 340
ht-degree: 0%

---

# Modelo operativo y de seguridad de responsabilidad compartida

[!DNL Adobe Commerce as a Cloud Service] es un servicio bajo demanda que depende de un modelo operativo y de seguridad de responsabilidad compartida. Adobe y los clientes comparten estas responsabilidades, y cada parte asume una responsabilidad distinta por garantizar y operar la aplicación de Adobe Commerce.

>[!BEGINSHADEBOX]

Las siguientes tablas de resumen utilizan el modelo RACI para mostrar las responsabilidades de seguridad compartidas entre Adobe y los clientes.

**R** — Responsable
**A** — Responsable
**C** — Consultado
**I** — Informado

>[!ENDSHADEBOX]

| Tarea | Adobe | Cliente |
| --- | --- | --- |
| Definición de reglas WAF de origen back-end | RA | |
| Definición de reglas de WAF de CDN back-end | RA | |
| Implementación y mantenimiento de [!DNL Adobe Developer App Builder] aplicaciones | | RA |
| Implementación de reglas WAF de plataforma back-end | RA | |
| Implementación de reglas WAF de CDN back-end | RA | |
| Corrigiendo errores principales en [!DNL Adobe Commerce as a Cloud Service] | RA | I |
| Publicando [!DNL Adobe Commerce as a Cloud Service] parches de infraestructura | RA | |
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
