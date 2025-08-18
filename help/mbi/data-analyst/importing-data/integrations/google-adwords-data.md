---
title: Datos esperados de Google Adwords
description: Aprenda a utilizar el Administrador de Data Warehouse para rastrear fácilmente campos de datos relevantes para su análisis.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# Se esperaban [!DNL Google Adwords] datos

Después de [haber conectado tu [!DNL Google Adwords] cuenta](../integrations/google-adwords.md), puedes usar [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) para rastrear fácilmente los campos de datos relevantes para el análisis.

Aquí puede observar dos tablas disponibles para la replicación en su Data Warehouse:

* `campaigns[account-id]`
* `adwords[account-id]`

La tabla `campaigns` *debe usarse de forma predeterminada*, por lo que puede empezar sincronizando todos los campos relevantes de esa tabla.

La tabla `adwords` contiene cuatro columnas que no están en la tabla `campaigns`:

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

Siempre que esté interesado en realizar un análisis que considere estos atributos, debe utilizar la tabla `adwords`.

>[!IMPORTANT]
>
>Esta tabla excluye las filas donde las cuatro columnas son `null`.

A continuación se muestra un vistazo al esquema esperado para ambas tablas.

## [!DNL Campaigns] tabla

La tabla `campaigns` contiene las siguientes columnas:

| **Columna** | **Descripción** |
|-----|-----|
| `\_id` | La clave principal de la tabla |
| `accountId` | ID de la cuenta |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | Número total de clics del día |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | Coste total de la campaña para el día |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords] ID de campaña |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | Nombre de campaña (por ejemplo, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | La fecha de ejecución de la campaña |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | Número de impresiones del día |
| `profileId` | El ID de perfil |
| `profileName` | El nombre del perfil |
| `\_updated\_at` | La fecha y hora de la última actualización de esta fila |

{style="table-layout:auto"}

## [!DNL AdWords] tabla

La tabla `adwords` contiene las siguientes columnas:

| **Columna** | **Descripción** |
|-----|-----|
| `\_id` | La clave principal de la tabla |
| `accountId` | ID de la cuenta |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | Número total de clics del día |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | Coste total de la campaña para el día |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords] ID de campaña |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | Nombre de campaña (por ejemplo, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | La fecha de ejecución de la campaña |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | Número de impresiones del día |
| `profileId` | El ID de perfil |
| `profileName` | El nombre del perfil |
| `\_updated\_at` | La fecha y hora de la última actualización de esta fila |
| `keyword` | La palabra clave de la campaña |
| `adContent` | Primera línea del texto de la campaña en línea |
| `adDestinationUrl` | Dirección URL a la cual hace referencia el tráfico de [!DNL Adwords] anuncios |
| `adGroup` | Nombre del grupo de anuncios [!DNL Adwords] |

{style="table-layout:auto"}

Con estos datos, puedes empezar a crear [métricas](../../../data-user/reports/ess-manage-data-metrics.md) e [informes](../../../tutorials/using-visual-report-builder.md) basados en los datos de gastos y [combinarlos con los ingresos de por vida para calcular el retorno de la inversión](../../analysis/roi-ad-camp.md).

## Tablas consolidadas

[!DNL Adobe] recomienda crear una tabla `consolidated ad spend` para combinar los datos de todos los orígenes de publicidad múltiples en una sola tabla. Esto le permite utilizar un único conjunto de métricas para el análisis de publicidad.

Si no tiene una tabla consolidada y crea un tablero hermoso en la tabla `adwords`, debe replicar el sistema de informes o crear métricas duplicadas para comparar esos datos con los datos de [!DNL Facebook Ads]. El uso de una tabla consolidada le permite incorporar sin problemas los datos de [!DNL Facebook Ads] con los informes de [!DNL Adwords] existentes. También puede segmentar por plataforma de publicidad.

Si ya ha sincronizado los campos anteriores, [póngase en contacto con nosotros](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) para consolidar la inversión en publicidad.
