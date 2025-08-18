---
title: Auditoría de datos de Google AdWords
description: Conozca los pasos para exportar los datos de Google AdWords.
exl-id: f619801f-e789-44ad-945e-268d430bf583
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Auditar datos de [!DNL Google Adwords]

¿Encontró algo extraño en [[!DNL Google Adwords]](../integrations/google-adwords.md)? Para identificar el problema, debe explorar los datos. Esto se puede hacer exportando los datos de [!DNL Google Adwords] a un archivo de `.csv`.

1. Descargue e instale la aplicación gratuita [[!DNL Google Adwords] Editor](https://ads.google.com/home/tools/ads-editor/).

1. Una vez finalizada la instalación, seleccione `Add Count` en el panel `Add/manage accounts`.

1. Escriba la información de su cuenta de [!DNL Google Adwords].

1. Una vez agregada su cuenta al editor [!DNL Google Adwords], seleccione **[!UICONTROL File** > ** Exportar hoja de cálculo (CSV)**> **Exportar toda la cuenta]**

Esto genera un archivo de `.csv` que contiene toda la información almacenada en su cuenta actual de [!DNL Google Adwords]. En este punto, envíe un [ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) (asegúrese de adjuntar este archivo) para que pueda ver más de cerca sus datos. Si el archivo es demasiado grande, compártalo con el equipo [!DNL Commerce Intelligence] a través de [!DNL Dropbox] o [!DNL Google Drive].

Para obtener más información sobre [!DNL Google Adwords] `.csv` exportaciones de archivos, consulte la [[!DNL Google Adwords] documentación](https://support.google.com/google-ads/editor/answer/38657?hl=en) oficial.
