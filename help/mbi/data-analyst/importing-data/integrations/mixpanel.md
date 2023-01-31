---
title: Conectar panel mixto
description: Obtenga información sobre cómo analizar cómo navegan los usuarios y cómo utilizan sus sitios web y aplicaciones.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Connect [!DNL Mixpanel]

>[!NOTE]
>
>Requiere [Permisos de administrador](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

con [!DNL Mixpanel], puede analizar cómo navegan los usuarios y cómo utilizan sus sitios web y aplicaciones. Echar un vistazo a los datos de comportamiento de los usuarios conduce a decisiones de desarrollo y diseño más inteligentes, lo que significa un mejor producto en general. Conexión [!DNL Mixpanel] a [!DNL MBI] permite analizar cómo se comportan los usuarios y cómo se traduce ese comportamiento en ingresos.

Conexión de [!DNL Mixpanel] datos a [!DNL MBI] un proceso sencillo de tres pasos:

1. [Abra el [!DNL Mixpanel] página credenciales en [!DNL MBI]](#stepone)
1. [Recupere su [!DNL Mixpanel] Credenciales de API](#steptwo)
1. [Escriba la [!DNL Mixpanel] Credenciales de API en MBI](#stepthree)

Para completar este proceso, deberá abrir dos ventanas o pestañas del explorador: una para [!DNL MBI], el otro para su [!DNL Mixpanel] cuenta.

## Apertura del [!DNL Mixpanel] página credenciales {#stepone}

Empecemos:

1. Vaya a la `Connections` página debajo de **[!DNL Manage Data** > **Connections]**.
1. Haga clic en **[!UICONTROL Add a New Source]**, situado en el lado derecho de la pantalla, encima de la `Data Sources` tabla.
1. Haga clic en el [!DNL Mixpanel] y se abrirá la página de credenciales.

Deje esta página abierta por ahora y cambie a la ventana del explorador con su [!DNL Mixpanel] cuenta.

## Recuperando su [!DNL Mixpanel] Credenciales de API {#steptwo}

Si no ha iniciado sesión en su [!DNL Mixpanel] Haga lo siguiente:

1. Haga clic en **[!UICONTROL Account]** en la esquina superior derecha.
1. En el cuadro de diálogo mostrado, haga clic en **[!UICONTROL Projects]**.
1. Sus credenciales de API mostrarán:

![Recuperación de credenciales de API de Mixpanel](../../../assets/Mixpanel_API_creds.png)

Mantenlo abierto - lo necesitamos para envolver esto.

## Introducción a su [!DNL Mixpanel] Credenciales de API en [!DNL MBI] {#stepthree}

1. Copie el `API Key` y `Secret` en el [!DNL Mixpanel] página credenciales en [!DNL MBI].
1. Haga clic en **[!UICONTROL Connect to Mixpanel]** para completar la configuración.

¡Eso es! Si la conexión se realiza correctamente, una _¡Correcto!_ se mostrará en la parte superior de la página.

### Relacionado

* [Esperado [!DNL Mixpanel] data](../integrations/mixpanel-data.md)
* [Reautenticación de integraciones](https://support.magento.com/hc/en-us/articles/360016733151)
