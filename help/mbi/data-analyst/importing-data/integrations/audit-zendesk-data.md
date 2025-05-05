---
title: Auditoría de datos de Zendesk
description: Conozca los pasos para exportar sus datos de Zendesk.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Auditoría de datos de Zendesk

¿Encontraste algo extraño en tus [[!DNL Zendesk] datos](../integrations/exp-zendesk-data.md)? Para identificar el problema, debe explorar los datos. Esto se puede hacer exportando los datos de [!DNL Zendesk] a un archivo descargable.

## Activación de la exportación de datos

La exportación de datos no está habilitada actualmente para todas las cuentas de [!DNL Zendesk]. Para activar esta característica, [envía un ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es), mencionando tu nombre de subdominio [!DNL Zendesk].

>[!NOTE]
>
>Actualmente, solo los planes `Enterprise` y `Plus` tienen acceso a esta función.

Una vez habilitada la exportación de datos, solamente los administradores de un dominio de correo electrónico específico podrán exportar datos desde la cuenta de [!DNL Zendesk]. Este dominio de correo electrónico suele ser el mismo dominio de correo electrónico que [!DNL Zendesk]. El dominio de correo electrónico del propietario de la cuenta se utiliza como predeterminado, pero puede cambiarlo si es necesario.

## Exportación a un archivo descargable

1. Haga clic en el icono Administración (logotipo de engranaje) en la barra lateral y elija **[!UICONTROL Manage** > **Reports]**.
1. Haga clic en la ficha **[!UICONTROL Export]**.
1. Haga clic en **[!UICONTROL Request file]** junto a Exportación XML completa, tal como se ve en la siguiente imagen.

   En este punto, comienza una compilación; se le notifica por correo electrónico cuando se completa.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. Haga clic en el vínculo de la notificación por correo electrónico para descargar un archivo zip que contenga el informe.

   Este vínculo de descarga es válido durante al menos tres días.

Este proceso genera un archivo XML que contiene toda la información almacenada en su cuenta actual de [!DNL Zendesk], incluidos los datos de vales (con comentarios), los datos de usuario y los datos de cuenta. En este momento, puede [enviar un ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es) (asegúrese de adjuntar este archivo). para que pueda ver más de cerca sus datos. Si el archivo es demasiado grande, compártalo con el equipo [!DNL Commerce Intelligence] a través de [!DNL Dropbox] o [!DNL Google Drive].

Para obtener más información sobre las exportaciones de archivos de [!DNL Zendesk], consulte la [[!DNL Zendesk] documentación de exportación](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file) oficial.
