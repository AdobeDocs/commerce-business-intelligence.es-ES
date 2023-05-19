---
title: 'Google Analytics: Rastree los datos de los dispositivos de usuario y los exploradores en la base de datos'
description: Descubra cuántos usuarios inician sesión realmente a través de dispositivos móviles y cómo afecta esto al valor de duración de esos usuarios.
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# [!UICONTROL Google Analytics] Seguimiento

Con [!UICONTROL Google Analytics] usted puede [guardar información de origen de referencia](../analysis/google-track-user-acq.md) para comprender de dónde provienen los usuarios más valiosos. En este tema se describe la plataforma (por ejemplo, el dispositivo o el explorador) en la que están trabajando los usuarios. Con esto, podrá comprender cuántos usuarios inician sesión realmente a través de dispositivos móviles y cómo afecta esto al valor de duración de esos usuarios.

## Guardar datos de dispositivos de usuario y exploradores

Cada vez que se realiza una solicitud al sitio web, el explorador del usuario envía una cadena de agente de usuario con información sobre la plataforma que realiza la solicitud. Estos son algunos ejemplos de la cadena del agente de usuario:

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.
` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

Si observa atentamente, verá que la cadena contiene información sobre el sistema operativo del usuario, el explorador y el nombre del dispositivo que está utilizando (si tiene un nombre). Aunque las cadenas del agente de usuario varían ampliamente entre plataformas e incluso versiones de la misma plataforma, generalmente es cierto que el nombre de la plataforma existirá en algún lugar dentro de. Por ejemplo, #1 anterior es un Mac con el navegador Chrome, #2 anterior es un equipo Windows con el navegador Firefox, #3 es un iPhone, #4 es un iPad y #5 es un dispositivo Android.

El servidor puede acceder a esta información cada vez que se realiza una solicitud. En PHP, la cadena del agente de usuario se almacena en `$_SERVER['HTTP_USER_AGENT']`. En Ruby on Rails, se almacena en `request.env['HTTP_USER_AGENT']`. Otros lenguajes y entornos le permitirán acceder a él de formas similares.

### ¿Cuándo se deben registrar estos datos?

[!DNL Adobe] recomienda añadir un nuevo campo llamado `Platform` o `User-Agent` a su `Customers` y `Orders` tablas de base de datos para almacenar esta información cada vez que se crea un usuario o se realiza un pedido. Si utiliza una base de datos SQL, este campo debe ser un `VARCHAR(255)`. 

>[!NOTE]
>
>El `User-Agent` se permite que la cadena sea mucho más larga que esto, pero en la práctica rara vez supera esta longitud.

### ¿Cómo analizo los segmentos útiles?

Existen varias bibliotecas que le ayudarán a analizar el `User-Agent` cadena en componentes como sistema operativo, dispositivo, etc. Consulte la [proyecto ua-parser](https://github.com/tobie/ua-parser) para obtener más información.

Con esta nueva información, puede comprender mejor cómo acceden los usuarios al sitio. A continuación, puede adaptar su experiencia o crear campañas de marketing para determinados grupos.

## Relacionado

* [Rastrear origen de referencia de pedido mediante [!DNL Google Anaytics] Comercio electrónico](../importing-data/integrations/google-ecommerce.md)
* [Rastrear origen de referencia de usuario en la base de datos](../analysis/google-track-user-acq.md)
* [Descubra sus fuentes y canales de adquisición más valiosos](../analysis/most-value-source-channel.md)
* [Conecte su [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Aumente el retorno de la inversión en sus campañas publicitarias](../analysis/roi-ad-camp.md)
* [¿Cómo? [!DNL Google Analytics] ¿Trabajo de atribución de UTM?](../analysis/utm-attributes.md)
