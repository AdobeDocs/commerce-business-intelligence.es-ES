---
title: Conectar Google Analytics
description: Aprenda a conectar Google Analytics con  [!DNL Commerce Intelligence].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Conectar [!DNL Google Analytics]

>[!NOTE]
>
>Requiere [permisos de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] es el servicio de análisis web más utilizado en Internet. La implementación de [!DNL Google Analytics] en el sitio web permite rastrear cómo los visitantes utilizan el sitio, qué contenido es atractivo, de dónde salen los visitantes, etc. El análisis de estas métricas en [!DNL Commerce Intelligence], junto con otros datos, mejora el estado general y la facilidad de uso del sitio.

Comience por escribir sus credenciales de [!DNL Google Analytics] en [!DNL Commerce Intelligence]:

1. Ir a **[!UICONTROL Manage Data** > **Integrations]**.

1. Haga clic en **[!UICONTROL Add Integration]**, ubicado en el lado derecho de la pantalla.

1. Haga clic en el icono [!DNL Google Analytics]. Se abre la página de credenciales [!DNL Google Analytics].

1. Escriba sus credenciales de [!DNL Google Analytics]. Al finalizar el proceso de autorización, se le redirigirá de nuevo a [!DNL Commerce Intelligence].

1. Se muestra una lista de ID de perfil. Compruebe los perfiles con los que desea conectarse a [!DNL Commerce Intelligence]. Si tiene varios perfiles y necesita ayuda para identificar cuál es cuál, consulte la sección Conexión de varios perfiles [!DNL Google Analytics] más abajo.

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. Los cambios se guardan automáticamente, así que haga clic en **Volver a Conexiones** cuando haya terminado.

## Conectando varios perfiles [!DNL Google Analytics]

Es posible que tenga varios sitios web conectados a una sola cuenta de [!DNL Google Analytics], identificada por su propio identificador de perfil [!DNL Google Analytics]. En este caso, tiene la opción de incluir todos los identificadores de perfil en [!DNL Commerce Intelligence]. Compruebe los ID de perfil que desea incluir durante el paso de selección de perfiles.

Para identificar el identificador de perfil [!DNL Google Analytics] de un sitio web en particular:

1. Iniciar sesión en [!DNL Google Analytics]
1. Vaya al panel [!DNL Google Analytics] del sitio web en particular
1. Observe la dirección URL: el ID de perfil corresponde a los ocho números que siguen a `p` al final de la línea:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconectando [!DNL Google Analytics] de [!DNL Commerce Intelligence] {#disconnect}

1. Visite la página [!DNL Google Analytics] [configuración de la cuenta](https://accounts.google.com/).
1. En la sección `Security` y haga clic en **[!UICONTROL edit]** junto a `Authorizing` aplicaciones y sitios.
1. Haga clic en **[!UICONTROL revoke access]** junto a [!DNL Commerce Intelligence].

## Relacionado:

* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Conectando [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Análisis de la actividad del sitio web y las tasas de conversión de clientes](../../analysis/web-act-cust-conversion.md)
* [Rastrear datos de adquisición de usuarios con  [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
