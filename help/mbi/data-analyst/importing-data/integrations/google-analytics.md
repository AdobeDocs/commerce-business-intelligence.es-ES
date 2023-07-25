---
title: Conectar Google Analytics
description: Aprenda a conectar Google Analytics con [!DNL Commerce Intelligence].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Connect [!DNL Google Analytics]

>[!NOTE]
>
>Requiere [Permisos de administración](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] es el servicio de análisis web más utilizado en internet. Implementación [!DNL Google Analytics] en el sitio web le permite realizar un seguimiento de cómo utilizan el sitio los visitantes, qué contenido es atractivo, dónde abandonan el sitio los visitantes, etc. Análisis de estas métricas en [!DNL Commerce Intelligence], junto con otros datos, mejora el estado general y la facilidad de uso del sitio.

Comience introduciendo su [!DNL Google Analytics] credenciales en [!DNL Commerce Intelligence]:

1. Ir a **[!UICONTROL Manage Data** > **Integrations]**.

1. Clic **[!UICONTROL Add Integration]**, situado en el lado derecho de la pantalla.

1. Haga clic en [!DNL Google Analytics] icono. Esto abre el [!DNL Google Analytics] página credenciales.

1. Introduzca su [!DNL Google Analytics] credenciales. Al finalizar el proceso de autorización, se le redirige de nuevo a [!DNL Commerce Intelligence].

1. Se muestra una lista de ID de perfil. Compruebe los perfiles a los que desea conectarse [!DNL Commerce Intelligence]. Si tiene varios perfiles y necesita ayuda para identificar cuál es cuál, consulte la sección Conexión múltiple [!DNL Google Analytics] perfiles de la sección siguiente.

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. Los cambios se guardan automáticamente, por lo que haga clic en **Volver a Conexiones** cuando haya terminado.

## Conexión múltiple [!DNL Google Analytics] perfiles

Es posible que tenga varios sitios web conectados a un único [!DNL Google Analytics] cuenta, identificadas por su propia cuenta [!DNL Google Analytics] ID de perfil. En este caso, tiene la opción de incluir todos sus ID de perfil en [!DNL Commerce Intelligence]. Compruebe los ID de perfil que desea incluir durante el paso de selección de perfiles.

Para identificar el de un sitio web en particular [!DNL Google Analytics] ID de perfil:

1. Iniciar sesión en [!DNL Google Analytics]
1. Vaya al sitio web de [!DNL Google Analytics] tablero
1. Observe la dirección URL: el ID de perfil corresponde a los ocho números que siguen `p` al final de la línea:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Desconectando [!DNL Google Analytics] de [!DNL Commerce Intelligence] {#disconnect}

1. Visite su [!DNL Google Analytics] [configuración de cuenta](https://accounts.google.com/) página.
1. En el `Security` y haga clic en **[!UICONTROL edit]** junto a `Authorizing` aplicaciones y sitios.
1. Clic **[!UICONTROL revoke access]** junto a [!DNL Commerce Intelligence].

## Relacionado:

* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Conectando [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Análisis de la actividad del sitio web y las tasas de conversión de clientes](../../analysis/web-act-cust-conversion.md)
* [Seguimiento de datos de adquisición de usuarios mediante [!DNL Google Analytics] galletas](../../analysis/google-track-user-acq.md)
