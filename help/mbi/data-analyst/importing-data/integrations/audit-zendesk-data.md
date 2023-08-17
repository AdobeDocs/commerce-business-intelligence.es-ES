---
title: Auditoría de datos de Zendesk
description: Conozca los pasos para exportar sus datos de Zendesk.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# Auditoría de datos de Zendesk

Encontré algo extraño en su [[!DNL Zendesk] datos](../integrations/exp-zendesk-data.md)? Para identificar el problema, debe explorar los datos. Esto se puede hacer exportando el [!DNL Zendesk] en un archivo descargable.

## Activación de la exportación de datos

Actualmente, la exportación de datos no está habilitada para todas las [!DNL Zendesk] cuentas. Para activar esta función, [enviar un ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html), mencionando su [!DNL Zendesk] nombre de subdominio.

>[!NOTE]
>
>Solo `Enterprise` y `Plus` los planes de actualmente tienen acceso a esta función.

Una vez habilitada la exportación de datos, solo los administradores de un dominio de correo electrónico específico pueden exportar datos desde el [!DNL Zendesk] cuenta. Este dominio de correo electrónico suele ser el mismo dominio de correo electrónico que su [!DNL Zendesk]. El dominio de correo electrónico del propietario de la cuenta se utiliza como predeterminado, pero puede cambiarlo si es necesario.

## Exportación a un archivo descargable

1. Haga clic en el icono Administración (logotipo de engranaje) en la barra lateral y elija **[!UICONTROL Manage** > **Reports]**.
1. Haga clic en **[!UICONTROL Export]** pestaña.
1. Clic **[!UICONTROL Request file]** junto a Exportación XML completa, tal como se ve en la siguiente imagen.

   En este punto, comienza una compilación; se le notifica por correo electrónico cuando se completa.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. Haga clic en el vínculo de la notificación por correo electrónico para descargar un archivo zip que contenga el informe.

   Este vínculo de descarga es válido durante al menos tres días.

Este proceso crea un archivo XML que contiene toda la información almacenada en el [!DNL Zendesk] Cuenta de, incluidos los datos de tickets (con comentarios), datos de usuario y datos de cuenta. En este punto, puede [enviar un ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) (asegúrese de adjuntar este archivo). para que pueda ver más de cerca sus datos. Si el archivo es demasiado grande, compártalo con el [!DNL Commerce Intelligence] equipo mediante [!DNL Dropbox] o [!DNL Google Drive].

Para obtener más información acerca de [!DNL Zendesk] exportaciones de archivos, consulte el [[!DNL Zendesk] documentación de exportación](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
