---
title: Conectar Google ECommerce
description: Obtenga información sobre los canales de referencia más valorados.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iBVf-dkbm1NbELZUYjLp1TzypO7Cu55tIzd93lQ1zo0
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: d095671a-1355-40aa-8b5f-06c33c68080bid: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 305
ht-degree: 0%

---

# Conectar [!DNL Google ECommerce]

>[!NOTE]
>
>Requiere [permisos de administrador](../../../administrator/user-management/user-management.md).

![Logotipo de Google eCommerce](../../../assets/google-ecommerce-logo.png)

Tiene un flujo constante de tráfico y pedidos, lo que significa que está llegando y adquiriendo clientes de forma eficaz. Pero, ¿cuáles son sus canales de referencia más valiosos? ¿Cuál es el valor promedio de duración de los clientes adquiridos de un origen frente a otro? Al conectar los datos de la fuente de referencia de pedidos de [!DNL Google ECommerce] a [!DNL Commerce Intelligence], puede generar análisis que le ayudarán a identificar los [canales de marketing más valiosos](../../../data-analyst/analysis/most-value-source-channel.md).

Comience por escribir sus credenciales de [!DNL Google ECommerce] en [!DNL Commerce Intelligence]:

1. Vaya a la página `Connections` en **[!UICONTROL Admin** > **Connections]**.

1. Haga clic en **[!UICONTROL Add a New Source]**, ubicado en el lado derecho de la pantalla sobre la tabla `Data Sources`.

1. Haga clic en el icono [!DNL Google ECommerce]. Se abre la página de credenciales [!DNL Google ECommerce].

1. Escriba sus credenciales de [!DNL Google Analytics]. Al finalizar el proceso de autorización, se le redirigirá de nuevo a [!DNL Commerce Intelligence].

1. Se muestra una lista de ID de perfil. Compruebe los perfiles con los que desea conectarse a [!DNL Commerce Intelligence].

   Si tiene varios perfiles y necesita ayuda para identificar cuál es cuál, consulte la sección **Conexión de varios perfiles [!DNL Google Analytics] más abajo.

   ![Formulario que muestra opciones para conectar varios perfiles de Google Analytics](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. Los cambios se guardan automáticamente, por lo que debe hacer clic en **[!UICONTROL Back to Connections]** cuando haya terminado.

## Conectando varios perfiles [!DNL Google Analytics] a [!DNL Commerce Intelligence]

Es posible que tenga varios sitios web conectados a una sola cuenta de [!DNL Google Analytics], identificada por su propio identificador de perfil [!DNL Google Analytics]. En este caso, tiene la opción de incluir todos los identificadores de perfil en [!DNL Commerce Intelligence]. Compruebe los ID de perfil que desea incluir durante el paso de selección de perfiles.

Para identificar el identificador de perfil [!DNL Google Analytics] de un sitio web en particular:

1. Iniciar sesión en [!DNL Google Analytics].
1. Vaya al panel [!DNL Google Analytics] del sitio web en particular.
1. Observe la dirección URL: el ID de perfil corresponde a los ocho números que siguen a `p` al final de la línea.

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconectando [!DNL Google ECommerce] de [!DNL Commerce Intelligence] {#disconnect}

1. Visite la página [!DNL Google Analytics] [configuración de la cuenta](https://www.google.com/account/about/?hl=en).
1. En la sección `Security`, haga clic en **[!UICONTROL edit]** junto a `Authorizing` aplicaciones y sitios.
1. Haga clic en **[!UICONTROL revoke access]** junto a [!DNL Commerce Intelligence].

## Relacionado:

* [Se esperaban  [!DNL Google ECommerce] datos](../integrations/google-ecommerce-data.md)
* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Configurando [!DNL Google ECommerce] seguimiento](https://support.google.com/analytics/answer/1009612?hl=en)
* [Descubra sus fuentes y canales de adquisición más valiosos](../../analysis/most-value-source-channel.md)
* [Aumente el retorno de la inversión en sus campañas publicitarias](../../analysis/roi-ad-camp.md)
