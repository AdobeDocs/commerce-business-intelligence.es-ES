---
title: Datos del Mixpanel esperados
description: Explore las tablas de datos principales que se pueden importar desde Mixpanel a su [!DNL MBI] cuenta.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Previsto [!DNL Mixpanel] datos

Después [ha conectado su [!DNL Mixpanel] account](../integrations/mixpanel.md), puede utilizar el [Administrador de Datas Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) para realizar fácilmente un seguimiento de los campos de datos relevantes para su análisis.

Este artículo explora las tablas de datos principales desde las que puede importar [!DNL Mixpanel] en su [!DNL MBI] cuenta. Las siguientes tablas se crearán en la Data Warehouse después de conectar Mixpanel. Para ver todos los campos disponibles para el seguimiento, haga clic en los vínculos de la columna de nombre de tabla.

>[!NOTE]
>
>Debido a las limitaciones de la [!DNL Mixpanel] API, datos históricos: datos anteriores a siete (7) días desde la fecha de conexión a [!DNL MBI] - no se replica.

| **Nombre de tabla** | **Descripción** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | Esta tabla contiene datos de evento sin procesar, incluido el evento, las fechas del evento y el bloque de plataforma. |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | Esta tabla contiene datos sobre los canales, incluido el ID de canal, la longitud del canal (número de días que el usuario debe completar el canal) y las fechas de inicio y finalización del canal. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | Contiene datos de People Analytics, incluidos los ID de sesión, la página y la información de usuario, así como la fecha y la hora en que se vio por última vez al usuario. |

{style="table-layout:auto"}

## Documentación relacionada

* [Conectando [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
