---
title: Responsabilidad compartida
description: Conozca las responsabilidades de seguridad de cada parte involucrada en su  [!DNL Adobe Commerce Optimizer] proyecto.
role: Admin, Developer, Leader
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
exl-id: 9e09790f-832d-43ab-b2df-6389ad52b43d
TQID: https://experienceleague.adobe.com/lOn0WJYdUi5qMX7OlRKeNAIc-TA29OFWWSqN3yQzt30
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: d095671a-1355-40aa-8b5f-06c33c68080bid: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 278
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
| Acceder a Dynamics para [!DNL Adobe Commerce Optimizer] | R | C |
| Solución de problemas de seguridad del cliente back-end | RA | I |
| Solución de problemas de seguridad de CDN back-end | RA | |
| Asistencia a Adobe en la investigación de seguridad (análisis/auditorías) | RA | |
| Realización de exploraciones ASV PCI | RA | I |
| Remediando análisis PCI de infraestructura [!DNL Adobe Commerce Optimizer] | R | |
| Administración de secretos de plataforma y sistema operativo | RA | |
| Supervisión de registros de seguridad back-end | RA | |
| Control de la asistencia al cliente y acceso | A | R |
| Pruebas y documentación anuales del plan de recuperación ante desastres de Adobe, así como de las copias de seguridad y restauración | RA | |
| Pruebas y documentación anuales del plan de recuperación ante desastres | RA | |
| Depuración y aislamiento de problemas | R | R |
| Compatibilidad oportuna con la depuración y el proceso de aislamiento de problemas | R | R |
| Instalando actualizaciones y revisiones en [!DNL Adobe Commerce Optimizer] | RA | I |
| Calidad de aplicación principal [!DNL Adobe Commerce Optimizer] | RA | |
