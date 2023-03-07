---
title: Conectar Google ECommerce
description: Obtenga información sobre los canales de referencia más valorados.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Connect [!DNL Google ECommerce]

>[!NOTE]
>
>Requiere [Permisos de administración](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

Tiene un flujo constante de tráfico y pedidos, lo que significa que está llegando y adquiriendo clientes de forma eficaz. Pero, ¿cuáles son sus canales de referencia más valiosos? ¿Cuál es el valor promedio de duración de los clientes adquiridos de un origen frente a otro? Al conectar los datos de origen de referencia del pedido desde [!DNL Google ECommerce] hasta [!DNL MBI], puede crear análisis que le ayuden a identificar su [canales de marketing más valiosos](../../../data-analyst/analysis/most-value-source-channel.md).

Comience introduciendo su [!DNL Google ECommerce] credenciales en [!DNL MBI]:

1. Vaya a la `Connections` página debajo de **[!UICONTROL Admin** > **Connections]**.
1. Clic **[!UICONTROL Add a New Source]**, situado en el lado derecho de la pantalla, encima de `Data Sources` tabla.
1. Haga clic en [!DNL Google ECommerce] icono. Esto abre el [!DNL Google ECommerce] página credenciales.
1. Introduzca su [!DNL Google Analytics] credenciales. Al finalizar el proceso de autorización, se le redirige de nuevo a [!DNL MBI].
1. Se muestra una lista de ID de perfil. Compruebe los perfiles a los que desea conectarse [!DNL MBI].

   Si tiene varios perfiles y necesita ayuda para identificar cuál es cuál, consulte la ** Conexión de varios [!DNL Google Analytics] perfiles de la sección siguiente.

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. Los cambios se guardan automáticamente, por lo que haga clic en **[!UICONTROL Back to Connections]** cuando haya terminado.

## Conexión múltiple [!DNL Google Analytics] perfiles para [!DNL MBI]

Es posible que tenga varios sitios web conectados a un único [!DNL Google Analytics] cuenta, identificadas por su propia cuenta [!DNL Google Analytics] ID de perfil. En este caso, tiene la opción de incluir todos sus ID de perfil en [!DNL MBI]. Compruebe los ID de perfil que desea incluir durante el paso de selección de perfiles.

Para identificar el de un sitio web en particular [!DNL Google Analytics] ID de perfil:

1. Iniciar sesión en [!DNL Google Analytics]
1. Vaya al sitio web de [!DNL Google Analytics] tablero
1. Observe la dirección URL: el ID de perfil corresponde a los ocho números que siguen `p` al final de la línea

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconectando [!DNL Google ECommerce] de [!DNL MBI] {#disconnect}

1. Visite su [!DNL Google Analytics] [configuración de cuenta](https://www.google.com/account/about/?hl=en) página.
1. En el `Security` , haga clic en **[!UICONTROL edit]** junto a `Authorizing` aplicaciones y sitios.
1. Clic **[!UICONTROL revoke access]** junto a [!DNL MBI].

## Relacionado:

* [Previsto [!DNL Google ECommerce] datos](../integrations/google-ecommerce-data.md)
* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Configuración de [!DNL Google ECommerce] tracking](https://support.google.com/analytics/answer/1009612?hl=en)
* [Descubra sus fuentes y canales de adquisición más valiosos](../../analysis/most-value-source-channel.md)
* [Aumente el retorno de la inversión en sus campañas publicitarias](../../analysis/roi-ad-camp.md)
