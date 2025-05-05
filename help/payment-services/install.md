---
title: Instalar [!DNL Payment Services]
description: Instale la extensión Servicios de pago.
role: Admin
feature: Payments, Checkout, Install, Upgrade
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# Instalar [!DNL Payment Services]

Para empezar a utilizar los servicios de pago para [!DNL Adobe Commerce] y [!DNL Magento Open Source], debe completar algunos pasos de incorporación.

>[!INFO]
>
> Vea nuestro vídeo [Configurar [!DNL Payment Services] para Adobe Commerce](https://experienceleague.adobe.com/es/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-payment-services) para obtener más información.

Descargar e instalar la extensión [!DNL Payment Services] para [!DNL Adobe Commerce] y [!DNL Magento Open Source] es un paso previo para usar [!DNL Payment Services].

## Descargar la extensión

Primero debe descargar la extensión de [Commerce Marketplace](https://experienceleague.adobe.com/docs/commerce-admin/start/resources/commerce-marketplace.html?lang=es) antes de instalarla.

1. Vaya a la extensión [Payment Services en Commerce Marketplace](https://commercemarketplace.adobe.com/magento-payment-services.html).
1. Para elegir la edición y la versión, cambie **[!UICONTROL Edition]** y **[!UICONTROL Your store version]** a sus selecciones preferidas.
1. Haga clic en **[!UICONTROL Add to Cart]**.
1. Complete el cierre de compra y haga clic en **[!UICONTROL Place Order]**.
1. Consulte el correo electrónico asociado a la descarga de Marketplace para obtener confirmación y detalles del pedido.

>[!NOTE]
>
> Para las versiones de Adobe Commerce 2.4.7 o posteriores, [!DNL Payment Services] está disponible de forma predeterminada.

## Instalación de la extensión

Puede instalar la extensión [!DNL Payment Services] tanto para [!DNL Adobe Commerce] en la infraestructura en la nube como para las instancias locales, que están vinculadas a su cuenta de Commerce [mageid](https://developer.adobe.com/commerce/marketplace/guides/sellers/profile-information/#access-keys) proporcionada en el proceso de registro.
[!DNL Magento Open Source] clientes utilizan las instrucciones locales.

Composer usa estas claves durante la instalación inicial de [!DNL Adobe Commerce] o en situaciones en las que las claves de Composer no se guardaron previamente en el archivo `auth.json`.

Consulte [Obtención de claves de autenticación](https://experienceleague.adobe.com/es/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) para obtener más información sobre la obtención de claves de Compositor.

Consulte [Instalar una extensión](https://experienceleague.adobe.com/es/docs/commerce-operations/installation-guide/tutorials/extensions) para obtener más información sobre qué considerar antes de descargar e instalar una extensión.

### [!DNL Adobe Commerce] en infraestructura de nube

Este método se utiliza para instalar la extensión [!DNL Payment Services] para una instancia de Commerce Cloud.

1. Actualizar el archivo de `composer.json`:

   ```bash
   composer require magento/payment-services --no-update
   ```

1. Actualice las dependencias e instale la extensión:

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Utilice el comando `composer update` para actualizar todas las dependencias raíz.

1. Confirme y envíe los cambios.

### Configuraciones locales y de otro tipo

Este método se usa para instalar la extensión [!DNL Payment Services] para una instancia local y [!DNL Magento Open Source] clientes.

1. Para obtener la extensión, ejecute estos comandos:

   ```bash
   composer require magento/payment-services --no-update
   ```

1. Actualice las dependencias e instale la extensión:

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Utilice el comando `composer update` para actualizar todas las dependencias raíz.

1. Actualice la instancia:

   ```bash
   bin/magento setup:upgrade
   ```

1. Borre la caché:

   ```bash
   bin/magento cache:clean
   ```

1. Confirme los cambios.
1. Para asegurarse de que el código confirmado esté implementado, actualice la instancia

>[!NOTE]
>
> [!DNL Payment Services] 1.6.1 es compatible con las versiones 7.x de PHP. Sin embargo, es muy recomendable actualizar a la última versión de [!DNL Payment Services].

## Actualización de la extensión

Cuando se publique una nueva versión de [!DNL Payment Services], podrá actualizar fácilmente la extensión.

1. Para obtener la versión más reciente del paquete:

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Utilice el comando `composer update` para actualizar todas las dependencias raíz.

1. Después de actualizar el compositor, ejecute:

   ```bash
   bin/magento setup:upgrade
   ```

1. Confirme y envíe los cambios.

## Resolución de problemas

Puede ver errores al intentar instalar la extensión [!DNL Payment Services]. Utilice los siguientes métodos de solución de problemas para resolver los errores.

### Lista de repositorios

Compruebe que `repo.magento.com` esté presente en su lista de repositorios.

### Claves de composición incorrectas

Si ve el siguiente error que indica que tiene las claves Compositor incorrectas:

```
Could not find a matching version of package magento/payment-services. Check the package spelling, your version constraint and that the package is available in a stability which matches your minimum-stability (stable).
```

Compruebe que las claves del Compositor son válidas y que tiene acceso a otros paquetes de Magento.

Para ver qué claves del Compositor están configuradas:

1. Buscar la ubicación del archivo `auth.json`:

   ```bash
   composer config --global home
   ```

1. Ver el archivo `auth.json`:

   ```bash
   cat /path/to/auth.json
   ```

1. Consulte [qué claves están asociadas con su cuenta de Commerce `MageID`](https://experienceleague.adobe.com/es/docs/commerce-operations/installation-guide/prerequisites/authentication-keys).

### Memoria insuficiente para PHP

Si ve el siguiente error que indica que no tiene suficiente memoria para PHP:

```
Fatal error: Allowed memory size of 2146435072 bytes exhausted (tried to allocate 4096 bytes) in phar:///usr/local/bin/composer/src/Composer/DependencyResolver/RuleWatchGraph.php on line 52
```

[Aumente el límite de memoria](https://experienceleague.adobe.com/es/docs/commerce-cloud-service/user-guide/configure/app/php-settings#increase-php-memory-limit) para PHP en su entorno en `php.ini`.

También puede especificar el límite de memoria mediante este comando: `php -d memory_limit=-1 [path to composer]/composer require magento/payment-services`.

Por ejemplo:

```bash
php -d memory_limit=-1 vendor/bin/composer require magento/payment-services
```
