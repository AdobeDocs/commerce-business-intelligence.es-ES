---
title: Conectar Google ECommerce
description: Obtenga información sobre los canales de referencia más valorados.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Conectar [!DNL Google ECommerce]

>[!NOTE]
>
>Requiere [permisos de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

Tiene un flujo constante de tráfico y pedidos, lo que significa que está llegando y adquiriendo clientes de forma eficaz. Pero, ¿cuáles son sus canales de referencia más valiosos? ¿Cuál es el valor promedio de duración de los clientes adquiridos de un origen frente a otro? Al conectar los datos de la fuente de referencia de pedidos de [!DNL Google ECommerce] a [!DNL Commerce Intelligence], puede generar análisis que le ayudarán a identificar los [canales de marketing más valiosos](../../../data-analyst/analysis/most-value-source-channel.md).

Comience por escribir sus credenciales de [!DNL Google ECommerce] en [!DNL Commerce Intelligence]:

1. Vaya a la página `Connections` en **[!UICONTROL Admin** > **Connections]**.

1. Haga clic en **[!UICONTROL Add a New Source]**, ubicado en el lado derecho de la pantalla sobre la tabla `Data Sources`.

1. Haga clic en el icono [!DNL Google ECommerce]. Se abre la página de credenciales [!DNL Google ECommerce].

1. Escriba sus credenciales de [!DNL Google Analytics]. Al finalizar el proceso de autorización, se le redirigirá de nuevo a [!DNL Commerce Intelligence].

1. Se muestra una lista de ID de perfil. Compruebe los perfiles con los que desea conectarse a [!DNL Commerce Intelligence].

   Si tiene varios perfiles y necesita ayuda para identificar cuál es cuál, consulte la sección **Conexión de varios perfiles [!DNL Google Analytics] más abajo.

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

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
