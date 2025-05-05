---
title: Controlar restricciones de cookies
description: Descubra cómo las recomendaciones de productos administran las restricciones de cookies.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Controlar restricciones de cookies

Tanto Adobe Commerce como Magento Open Source solicitan consentimiento antes de almacenar los datos en las cookies del explorador. Para obtener más información, consulte [Modo de restricción de cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=es).

Cuando implementa el módulo `magento/product-recommendations` en producción, comienza a recopilar eventos de interacción de compradores en la tienda. Dado que los datos de estos eventos se pueden almacenar en cookies del explorador o en el almacenamiento local, la función admite el modo de restricción de cookies al no recopilar eventos hasta que el comprador haya dado su consentimiento para la cookie.

Esto puede no funcionar con soluciones de consentimiento de cookies de terceros. Es responsabilidad de cada comerciante asegurarse de que la recopilación de datos no se produzca antes de que se haya dado el consentimiento de las cookies, como suele requerir la ley. Si administra el consentimiento de cookies con código personalizado, puede utilizar una cookie de no seguimiento denominada `mg_dnt` para restringir la recopilación de datos.

- Nombre de la cookie:

  ```text
  `const DNT_COOKIE = "mg_dnt";`
  ```

- Establezca la cookie do-not-track para deshabilitar la recopilación de datos:

  ```text
  `$.mage.cookies.set(DNT_COOKIE, true);`
  ```

- Para borrar la cookie cuando el usuario ha aceptado cookies:

  ```text
  `$.mage.cookies.clear(DNT_COOKIE);`
  ```
