---
title: Datos del Mixpanel esperados
description: Explore las tablas de datos principales que se pueden importar desde Mixpanel a su cuenta de  [!DNL Commerce Intelligence] .
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Se esperaban [!DNL Mixpanel] datos

Después de [haber conectado tu [!DNL Mixpanel] cuenta](../integrations/mixpanel.md), puedes usar el [Administrador de Datas Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para rastrear fácilmente los campos de datos relevantes para el análisis.

En este tema se exploran las tablas de datos principales que puede importar de [!DNL Mixpanel] a su cuenta de [!DNL Commerce Intelligence]. Las tablas siguientes se crearán en la Data Warehouse después de conectar [!DNL Mixpanel]. Para ver todos los campos disponibles para el seguimiento, haga clic en los vínculos de la columna de nombre de tabla.

>[!NOTE]
>
>Debido a las limitaciones de la API [!DNL Mixpanel], los datos históricos (datos anteriores a siete (7) días desde la fecha de conexión a [!DNL Commerce Intelligence]) no se replican.

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | Esta tabla contiene datos de evento sin procesar, incluido el evento, las fechas del evento y el bloque de plataforma. |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | Esta tabla contiene datos sobre los canales, incluido el ID de canal, la longitud del canal (número de días que el usuario debe completar el canal) y las fechas de inicio y finalización del canal. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | Contiene datos de People Analytics, incluidos los ID de sesión, la página y la información de usuario, así como la fecha y la hora en que se vio por última vez al usuario. |

{style="table-layout:auto"}

## Documentación relacionada

* [Conectando [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Reautenticando integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=es)
