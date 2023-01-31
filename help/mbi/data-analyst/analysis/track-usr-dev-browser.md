---
title: 'Google Analytics: Rastrear datos de dispositivos y exploradores de usuario en la base de datos'
description: Aprenda cuántos usuarios están iniciando sesión realmente a través de dispositivos móviles y cómo afecta esto al valor de duración de esos usuarios.
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# [!UICONTROL Google Analytics] Seguimiento

con [!UICONTROL Google Analytics] puede [guardar información de origen de referencia](../analysis/google-track-user-acq.md) para comprender de dónde provienen los usuarios más valiosos. En este tema, aprenderá sobre la plataforma (por ejemplo, el dispositivo o el navegador) en la que están trabajando los usuarios. Con esto, podrá comprender cuántos usuarios están iniciando sesión realmente a través de dispositivos móviles y cómo esto afecta al valor de duración de esos usuarios.

## Almacenamiento de datos de dispositivos y exploradores de usuario

Cada vez que se realiza una solicitud a su sitio web, el navegador del usuario envía una cadena User-Agent con información sobre la plataforma que realiza la solicitud. A continuación se muestran algunos ejemplos de la cadena User-Agent:

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.
` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

Si observa con atención que la cadena contiene información sobre el sistema operativo del usuario, el explorador y el nombre del dispositivo que utiliza (si tiene un nombre). Aunque las cadenas User-Agent varían ampliamente entre plataformas e incluso versiones de la misma plataforma, es generalmente cierto que el nombre de la plataforma existirá en algún lugar dentro de. Por ejemplo, #1 anterior es una Mac con el navegador Chrome, #2 anterior es un equipo Windows con el navegador Firefox, #3 es una iPhone, #4 es una iPad y #5 es un dispositivo Android.

El servidor puede acceder a esta información cada vez que se realiza una solicitud. En PHP, la cadena User-Agent se almacena en `$_SERVER['HTTP_USER_AGENT']`. En Ruby on Rails, se almacena en `request.env['HTTP_USER_AGENT']`. Otros idiomas y entornos le permitirán acceder a ellos de formas similares.

### ¿Cuándo se deben registrar estos datos?

Le recomendamos que agregue un nuevo campo llamado `Platform` o `User-Agent` a su `Customers` y `Orders` tablas de base de datos para almacenar esta información cada vez que se crea un usuario o se realiza un pedido. Si utiliza una base de datos SQL, este campo debe ser un `VARCHAR(255)`. 

>[!NOTE]
>
>La variable `User-Agent` se permite que la cadena sea mucho más larga que esta, pero en la práctica rara vez supera esta longitud.

### ¿Cómo analizo los segmentos útiles?

Existen varias bibliotecas para ayudarle a analizar la variable `User-Agent` en componentes como sistema operativo, dispositivo, etc. Consulte la [proyecto ua-parser](https://github.com/tobie/ua-parser) para obtener más información.

Con esta nueva información, podrá comprender mejor cómo acceden al sitio los usuarios. A continuación, puede adaptar su experiencia o crear campañas de marketing para determinados grupos.

## Relacionado

* [Rastrear la fuente de referencia de pedidos a través de [!DNL Google Anaytics] Comercio electrónico](../importing-data/integrations/google-ecommerce.md)
* [Seguimiento del origen de referencia del usuario en la base de datos](../analysis/google-track-user-acq.md)
* [Descubra las fuentes y canales de adquisición más valiosos](../analysis/most-value-source-channel.md)
* [Conecte su [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Aumento del ROI en las campañas publicitarias](../analysis/roi-ad-camp.md)
* [¿Cómo [!DNL Google Analytics] ¿Funciona la atribución de UTM?](../analysis/utm-attributes.md)
