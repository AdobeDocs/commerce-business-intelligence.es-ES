---
title: Conectar Google ECommerce
description: Conozca sus canales de referencia más valiosos.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Connect [!DNL Google ECommerce]

>[!NOTE]
>
>Requiere [Permisos de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

Tiene un flujo constante de tráfico y pedidos, lo que significa que está llegando a los clientes y adquiriéndolos de forma eficaz. Pero, ¿cuáles son sus canales de referencia más valiosos? ¿cuál es el valor promedio de duración de los clientes adquiridos de una fuente frente a otra? Al conectar los datos de origen de referencia de pedido de [!DNL Google ECommerce] a [!DNL MBI], puede crear análisis que le ayudarán a identificar su [los canales de marketing más valiosos](../../../data-analyst/analysis/most-value-source-channel.md).

Empecemos entrando en nuestra [!DNL Google ECommerce] credenciales a [!DNL MBI]:

1. Vaya a la `Connections` página debajo de **[!UICONTROL Admin** > **Connections]**.
1. Haga clic en **[!UICONTROL Add a New Source]**, situado en el lado derecho de la pantalla, encima de la `Data Sources` tabla.
1. Haga clic en el [!DNL Google ECommerce] icono. Se abrirá la variable [!DNL Google ECommerce] credenciales .
1. Escriba la [!DNL Google Analytics] credenciales. Al finalizar el proceso de autorización, se le redirigirá de nuevo a [!DNL MBI].
1. Se mostrará una lista de ID de perfil. Compruebe los perfiles a los que desea conectarse [!DNL MBI].

   Si tiene varios perfiles y necesita ayuda para identificar cuál es cuál, consulte **Conexión múltiple [!DNL Google Analytics] a continuación.

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. Los cambios se guardan automáticamente, por lo que solo tiene que hacer clic en **[!UICONTROL Back to Connections]** cuando haya terminado.

## Conexión múltiple [!DNL Google Analytics] perfiles para [!DNL MBI]

Es posible que tenga varios sitios web conectados a una sola [!DNL Google Analytics] cuenta, identificada por su propia cuenta [!DNL Google Analytics] ID de perfil. En este caso, tendrá la opción de incluir todos sus ID de perfil en [!DNL MBI]. Compruebe los ID de perfil que desea incluir durante el paso de selección de perfiles.

Para identificar el [!DNL Google Analytics] ID de perfil:

1. Iniciar sesión [!DNL Google Analytics]
1. Vaya al sitio web en particular [!DNL Google Analytics] tablero
1. Busque la dirección URL: el ID de perfil corresponde a los 8 números siguientes `p` al final de la línea

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconexión [!DNL Google ECommerce] from [!DNL MBI] {#disconnect}

1. Visite su [!DNL Google Analytics] [configuración de la cuenta](https://www.google.com/accounts/) página.
1. En el `Security` , haga clic en **[!UICONTROL edit]** junto a `Authorizing` aplicaciones y sitios.
1. Haga clic en **[!UICONTROL revoke access]** junto a [!DNL MBI].

## Relacionado:

* [Esperado [!DNL Google ECommerce] data](../integrations/google-ecommerce-data.md)
* [Reautenticación de integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Configuración [!DNL Google ECommerce] seguimiento](https://support.google.com/analytics/answer/1009612?hl=en)
* [Descubra las fuentes y canales de adquisición más valiosos](../../analysis/most-value-source-channel.md)
* [Aumento del ROI en las campañas publicitarias](../../analysis/roi-ad-camp.md)
