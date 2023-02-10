---
title: Auditoría de datos de Zendesk
description: Conozca los pasos para exportar sus datos de Zendesk.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Auditoría de datos de Zendesk

Encontré algo extraño en tu [[!DNL Zendesk] data](../integrations/exp-zendesk-data.md)? Para identificar el problema, necesitamos explorar sus datos. Esto se puede hacer exportando su [!DNL Zendesk] a un archivo descargable.

## Habilitación de la exportación de datos

Actualmente, la exportación de datos no está habilitada para todos [!DNL Zendesk] cuentas. Para activar esta función, [enviar un ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en), mencionando su [!DNL Zendesk] nombre de subdominio.

>[!NOTE]
>
>Solo `Enterprise` y `Plus` los planes actualmente tienen acceso a esta función.

Una vez habilitada la exportación de datos, solo los administradores de un dominio de correo electrónico específico pueden exportar los datos de su [!DNL Zendesk] cuenta. Este dominio de correo electrónico suele ser el mismo dominio de correo electrónico que su [!DNL Zendesk]. El dominio de correo electrónico del propietario de la cuenta se usa como predeterminado, pero puede cambiarlo si es necesario.

## Exportación a un archivo descargable

1. Haga clic en el icono Admin (logotipo del engranaje) en la barra lateral y seleccione **[!UICONTROL Manage** > **Reports]**.
1. Haga clic en el **[!UICONTROL Export]** pestaña .
1. Haga clic en **[!UICONTROL Request file]** junto a Exportación XML completa como se ve en la siguiente imagen.

   En este punto, se iniciará una compilación; se le notificará por correo electrónico cuando termine.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. Haga clic en el vínculo de la notificación por correo electrónico para descargar un archivo zip que contenga el informe.

   Este vínculo de descarga es válido durante al menos tres días.

Este proceso crea un archivo XML que contiene toda la información almacenada en la [!DNL Zendesk] cuenta, incluidos datos de ticket (con comentarios), datos de usuario y datos de cuenta. En este punto, puede [enviar un ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) (asegúrese de adjuntar este archivo). así que podemos echar un vistazo a sus datos. Si el archivo es demasiado grande, compártalo con el [!DNL MBI] equipo via [!DNL Dropbox] o [!DNL Google Drive].

Para obtener más información, consulte [!DNL Zendesk] exportaciones de archivos, consulte la [[!DNL Zendesk] documentación de exportación](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
