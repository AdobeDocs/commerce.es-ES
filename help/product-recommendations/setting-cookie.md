---
title: Controlar restricciones de cookies
description: Descubra cómo las recomendaciones de productos administran las restricciones de cookies y el cumplimiento de la privacidad.
exl-id: 7e7342db-b903-4105-93c0-e4022c81673b
source-git-commit: dbb36b9fa800e128f1aea795a891ffbfb751aa76
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# Controlar restricciones de cookies

Tanto Adobe Commerce como Magento Open Source solicitan consentimiento antes de almacenar los datos en las cookies del explorador. Para obtener más información, consulte [Modo de restricción de cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html).

## Cómo gestionan las recomendaciones de productos las restricciones de cookies

Cuando implementa el módulo `magento/product-recommendations` en producción, comienza a recopilar eventos de interacción de compradores en la tienda. Estos datos se pueden almacenar en cookies del explorador o en almacenamiento local para activar los algoritmos de recomendación.

>[!IMPORTANT]
>
>Las Recomendaciones de productos ahora respetan el modo de restricción de cookies al no recopilar ni almacenar datos en cookies o el almacenamiento local cuando las restricciones de cookies están habilitadas. Esto incluye datos de comportamiento utilizados para recomendaciones personalizadas.

### Datos afectados por restricciones de cookies

Los siguientes datos de recomendaciones de productos no se recopilan cuando el modo de restricción de cookies está habilitado:

- **Datos de comportamiento**: vistas de productos, acciones de complementos al carro de compras, compras y otras interacciones del comprador.
- **Datos de sesión**: Interacciones entre la unidad de recomendación y la información de sesión del comprador.
- **Datos de Personalization**: Datos usados para tipos de recomendaciones como &quot;Vistos recientemente&quot; y &quot;Más comprados&quot;.

### Impacto en los tipos de recomendación

Cuando el modo de restricción de cookies está habilitado y los compradores no han aceptado cookies, es posible que algunos tipos de recomendaciones no se muestren o que muestren resultados limitados:

- **Productos vistos recientemente**: Requiere datos de sesión almacenados en cookies o almacenamiento local.
- **Recomendado para usted**: Requiere datos de comportamiento para la personalización.
- **Compró esto, compró aquello**: Requiere datos del historial de compras.

>[!NOTE]
>
>Los tipos de recomendación que no dependen de datos de comportamiento, como &quot;Más visitados&quot; y &quot;Similitud visual&quot;, seguirán funcionando normalmente incluso con las restricciones de cookies habilitadas.

## Soluciones de consentimiento de cookies de terceros

Las recomendaciones de productos pueden no integrarse automáticamente con las soluciones de consentimiento de cookies de terceros. Es responsabilidad del comerciante garantizar que la recopilación de datos cumpla con las leyes y regulaciones de privacidad aplicables.

Si utiliza una solución de consentimiento de cookies personalizada, puede implementar el mecanismo de cookie de no seguimiento para controlar la recopilación de datos.

### Implementación de cookies de no seguimiento

Puede usar la cookie `mg_dnt` para controlar mediante programación la recopilación de datos:

#### Nombre de cookie

```javascript
const DNT_COOKIE = "mg_dnt";
```

#### Deshabilitar la recopilación de datos

Establezca la cookie de no seguimiento cuando los usuarios rechacen las cookies:

```javascript
$.mage.cookies.set(DNT_COOKIE, true);
```

#### Habilitar la recopilación de datos

Borre la cookie de no seguimiento cuando los usuarios acepten cookies:

```javascript
$.mage.cookies.clear(DNT_COOKIE);
```

## Probando modo de restricción de cookie

Para probar cómo se comportan las recomendaciones de productos con las restricciones de cookies:

1. Habilite el modo de restricción de cookies en la configuración de Adobe Commerce.
1. Visita tu tienda sin aceptar cookies.
1. Compruebe que las unidades de recomendación muestran el contenido de reserva adecuado.
1. Acepte las cookies y compruebe que las recomendaciones comienzan a recopilar datos.

## Cumplimiento de privacidad

La recopilación de datos de Recommendations del producto no incluye información de identificación personal (PII). Todos los identificadores de usuario, como los ID de cookie y las direcciones IP, se anonimizan. Para obtener más información, consulte la [Política de privacidad de Adobe](https://www.adobe.com/privacy/policy.html).

>[!TIP]
>
>Para los clientes del sector sanitario que utilizan la extensión HIPAA de servicios de datos, puede ser necesaria una configuración adicional. Consulte [Preparación para HIPAA](../data-connection/hipaa-readiness.md) para obtener más información.
