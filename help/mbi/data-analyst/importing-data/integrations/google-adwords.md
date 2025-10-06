---
title: Conectar Google AdWords
description: Aprenda a medir el ROI de la campaña combinando el coste de la publicidad con el valor de duración del cliente (CLV) de los usuarios adquiridos de las campañas.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Conectar [!DNL Google Adwords]

>[!NOTE]
>
>Requiere [permisos de administrador](../../../administrator/user-management/user-management.md).

![Logotipo de Google AdWords](../../../assets/Google_Adwords_logo.png)

Usted hizo su investigación, creó sus anuncios, lanzó su campaña [!DNL Google]. Ahora es el momento de analizar los datos de gasto en publicidad y ver si el dinero se está gastando de forma eficaz. Con los datos de gasto en publicidad, puede [medir el retorno de la inversión de la campaña combinando el costo de publicidad con el valor de duración del cliente (CLV)](../../analysis/roi-ad-camp.md) de los usuarios adquiridos de sus campañas.

Comience escribiendo sus credenciales de [!DNL Google Adwords] en [!DNL Commerce Intelligence].

1. Vaya a la página `Connections` en **Administrar datos > Integraciones**.
1. Haga clic en **Agregar integración**, ubicado en la parte superior derecha de la pantalla.
1. Haga clic en el icono **[!DNL Google Adwords]**. Se abre la página de credenciales [!DNL Google Adwords].
1. Escriba sus credenciales de [!DNL Google Analytics]. Una vez completado el proceso de autorización, se le redirigirá a [!DNL Commerce Intelligence].
1. Se muestra una lista de ID de perfil. Compruebe los perfiles con los que desea conectarse a [!DNL Commerce Intelligence].

   ![Cuadro de diálogo de conexión de Google AdWords que muestra la selección de perfiles](../../../assets/cnnct-profile.png)

1. Los cambios se guardan automáticamente, por lo que debe hacer clic en **[!UICONTROL Back to Connections]** cuando haya terminado.

Si tiene varios perfiles y necesita ayuda para identificar cuál es cuál, consulte la sección `Connecting Multiple Google Analytics profiles` a continuación.

## Conectando varios perfiles [!DNL Google Analytics]

Es posible que tenga varios sitios web conectados a una sola cuenta de [!DNL Google Analytics], identificada por su propio identificador de perfil [!DNL Google Analytics]. En este caso, tiene la opción de incluir todos los identificadores de perfil en [!DNL Commerce Intelligence]. Compruebe los ID de perfil que desea incluir durante el paso de selección de perfiles.

**Para identificar el identificador de perfil de Google Analytics de un sitio web en particular:**

1. Iniciar sesión en [!DNL Google Analytics]
1. Vaya al panel [!DNL Google Analytics] del sitio web en particular
1. Observe la dirección URL: el ID de perfil corresponde a los ocho números que siguen a `p` al final de la línea:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Desconectando [!DNL Google Adwords]

1. Visite la página [!DNL Google] [configuración de la cuenta](https://www.google.com/account/about/?hl=en).
1. En la sección `Security`, haga clic en **[!UICONTROL edit]** junto a `Authorizing` aplicaciones y sitios.
1. Haga clic en **[!UICONTROL revoke access]**.

## Relacionado

* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=es)
* [Rastrear origen de referencia de pedido mediante  [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Rastrear origen de referencia de usuario en la base de datos](../../analysis/google-track-user-acq.md)
* [Descubra sus fuentes y canales de adquisición más valiosos](../../analysis/most-value-source-channel.md)
* [Aumente el retorno de la inversión en sus campañas publicitarias](../../analysis/roi-ad-camp.md)
* [¿Cómo funciona la atribución de  [!DNL Google Analytics] UTM?](../../analysis/utm-attributes.md)
