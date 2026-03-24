---
title: Auditoría de datos de Zendesk
description: Conozca los pasos para exportar sus datos de Zendesk.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/EQmiSbzzvOONQ8-F1U9uMVpgXUKd2PEjcLXLVSgQSm8
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 269
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

Este proceso genera un archivo XML que contiene toda la información almacenada en su cuenta actual de [!DNL Zendesk], incluidos los datos de vales (con comentarios), los datos de usuario y los datos de cuenta. En este punto, puede [enviar un vale de soporte técnico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es) (asegúrese de adjuntar este archivo) para que pueda ver más de cerca sus datos. Si el archivo es demasiado grande, compártalo con el equipo [!DNL Commerce Intelligence] a través de [!DNL Dropbox] o [!DNL Google Drive].

Para obtener más información sobre las exportaciones de archivos de [!DNL Zendesk], consulte la [[!DNL Zendesk] documentación de exportación](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file) oficial.
