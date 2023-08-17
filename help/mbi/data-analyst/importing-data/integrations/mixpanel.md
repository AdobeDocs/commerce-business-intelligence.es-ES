---
title: Conectar Mixpanel
description: Obtenga información sobre cómo analizar cómo navegan y utilizan los usuarios sus sitios web y aplicaciones.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Connect [!DNL Mixpanel]

>[!NOTE]
>
>Requiere [Permisos de administración](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

Con [!DNL Mixpanel], puede analizar cómo navegan y utilizan los usuarios sus sitios web y aplicaciones. Echar un vistazo a los datos de comportamiento de los usuarios conduce a decisiones de diseño y desarrollo más inteligentes, lo que significa un mejor producto en general. Conectando [!DNL Mixpanel] hasta [!DNL Commerce Intelligence] le permite analizar cómo se comportan los usuarios y cómo ese comportamiento se traduce en ingresos.

Conexión de su [!DNL Mixpanel] datos a [!DNL Commerce Intelligence] un proceso sencillo de tres pasos:

1. [Abra el [!DNL Mixpanel] página credenciales en [!DNL Commerce Intelligence]](#stepone)
1. [Recupere su [!DNL Mixpanel] Credenciales de API](#steptwo)
1. [Introduzca su [!DNL Mixpanel] Credenciales de API en [!DNL Commerce Intelligence]](#stepthree)

Para completar este proceso, debe abrir dos ventanas o pestañas del explorador, una para [!DNL Commerce Intelligence] y el otro para su [!DNL Mixpanel] cuenta.

## Abriendo el [!DNL Mixpanel] página credenciales {#stepone}

Introducción:

1. Vaya a la `Connections` página debajo de **[!DNL Manage Data** > **Connections]**.

1. Clic **[!UICONTROL Add a New Source]**, situado en el lado derecho de la pantalla, encima de `Data Sources` tabla.

1. Haga clic en [!DNL Mixpanel] y se abrirá la página credenciales.

Deje esta página abierta por ahora y cambie a la ventana del explorador con su [!DNL Mixpanel] cuenta.

## Recuperación de su [!DNL Mixpanel] Credenciales de API {#steptwo}

Si no ha iniciado sesión en su [!DNL Mixpanel] cuenta aún, hágalo y haga lo siguiente:

1. Clic **[!UICONTROL Account]** en la esquina superior derecha.

1. En el cuadro de diálogo que aparece, haga clic en **[!UICONTROL Projects]**.

1. Se muestran sus credenciales de API:

![Recuperando credenciales de API de Mixpanel](../../../assets/Mixpanel_API_creds.png)

Mantén esto abierto, lo necesitas para terminar esto.

## Introducción de su [!DNL Mixpanel] Credenciales de API en [!DNL Commerce Intelligence] {#stepthree}

1. Copie el `API Key` y `Secret` en el [!DNL Mixpanel] página credenciales en [!DNL Commerce Intelligence].
1. Clic **[!UICONTROL Connect to Mixpanel]** para completar la configuración.

Si la conexión se realiza correctamente, _¡Correcto!_ El mensaje se muestra en la parte superior de la página.

### Relacionado

* [Previsto [!DNL Mixpanel] datos](../integrations/mixpanel-data.md)
* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
