---
title: Conectar Google Analytics
description: Aprenda a conectar Google Analytics con  [!DNL Commerce Intelligence].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/wSR5SWYSfmNZkzp5QxTUwv6QSsynXYofmRkKbvMsohs
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 283
ht-degree: 0%

---

# Conectar [!DNL Google Analytics]

>[!NOTE]
>
>Requiere [permisos de administrador](../../../administrator/user-management/user-management.md).

![logotipo de Google Analytics](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] es el servicio de análisis web más utilizado en Internet. La implementación de [!DNL Google Analytics] en el sitio web permite rastrear cómo los visitantes utilizan el sitio, qué contenido es atractivo, de dónde salen los visitantes, etc. El análisis de estas métricas en [!DNL Commerce Intelligence], junto con otros datos, mejora el estado general y la facilidad de uso del sitio.

Comience por escribir sus credenciales de [!DNL Google Analytics] en [!DNL Commerce Intelligence]:

1. Ir a **[!UICONTROL Manage Data** > **Integrations]**.

1. Haga clic en **[!UICONTROL Add Integration]**, ubicado en el lado derecho de la pantalla.

1. Haga clic en el icono [!DNL Google Analytics]. Se abre la página de credenciales [!DNL Google Analytics].

1. Escriba sus credenciales de [!DNL Google Analytics]. Al finalizar el proceso de autorización, se le redirigirá de nuevo a [!DNL Commerce Intelligence].

1. Se muestra una lista de ID de perfil. Compruebe los perfiles con los que desea conectarse a [!DNL Commerce Intelligence]. Si tiene varios perfiles y necesita ayuda para identificar cuál es cuál, consulte la sección Conexión de varios perfiles [!DNL Google Analytics] más abajo.

   ![Página de administración de Google Analytics que muestra el ID de perfil en la URL](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

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
