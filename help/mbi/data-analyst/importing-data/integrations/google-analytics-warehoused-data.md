---
title: Datos del almacén de Google Analytics esperados
description: Aprenda a interactuar con los datos almacenados de sus Google Analytics.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# Esperado [!DNL Google Analytics] Datos almacenados

>[!NOTE]
>
>Requiere [Permisos de administrador](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>Alguna información fue usada con el permiso de nuestros amigos en [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] integración en [!DNL MBI] utiliza el [!DNL Google Analytics] [API de informes principales](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>Para evitar resultados inesperados o no significativos, confirme que todas las dimensiones que utilice son [compatible con las métricas](https://developers.google.com/analytics/devguides/reporting/core/dimsmets) utiliza en la variable `Report Builder`.

Una sola tabla denominada `report` - se creará en la Data Warehouse.

El esquema de esta tabla estará compuesto por las Métricas y Dimension que seleccionó durante el proceso de configuración y otras dos columnas: `start-date` y `end-date`.

Si, por ejemplo, seleccionó las siguientes métricas y Dimension durante la configuración:

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

La tabla sería como el ejemplo siguiente.

| **Nombre de columna** | **Descripción** |
|-----|-----|
| `\_id` | Esta columna es la `primary key`. |
| `\_rjm\_record\_hash` | [!DNL MBI] identificador único. Esta columna la crea [!DNL MBI]. |
| `\_updated\_at` | Esta columna contiene la última vez que se actualizó la fila de datos. Esta columna la crea [!DNL MBI]. |
| `start-date` | Identificación del día para el que está la fila. |
| `end-date` | Identificación del día para el que está la fila. |
| `month` | Dimensión seleccionada: Mes de la sesión, un entero de dos dígitos del 01 al 12. |
| `users` | Métrica seleccionada: El número total de usuarios para el período de tiempo solicitado. |

{style=&quot;table-layout:auto&quot;}

## Recordatorio: Diferencia entre Google Analytics almacenados e integración activa

El diferenciador principal es que se almacena una integración ([!DNL Google Analytics Warehoused]) y el otro no es ([!DNL Google Analytics Live]). En el caso de [!DNL Google Analytics Warehoused], esto permite la manipulación de su [!DNL Google Analytics] y le permite combinar [!DNL Google Analytics] y otras fuentes de datos para crear informes descriptivos.

Veamos [!DNL Google Analytics] campañas publicitarias para ver un ejemplo de lo que se puede hacer desde el punto de vista de la manipulación. Supongamos que tenía varias campañas publicitarias para el cuarto trimestre con nombres diferentes. Las campañas fueron el resultado de una iniciativa de marketing específica. Con los datos almacenados, podemos crear una nueva columna que encuentre los nombres de campaña en cuestión y devuelva el nombre de la iniciativa del cuarto trimestre de `Operation Dumbo`.

El aspecto de la combinación permite [!DNL Google Analytics] datos que se van a unir a otros datos para realizar análisis. Por ejemplo, tome `Total Time On Site By Ad Campaign` datos de [!DNL Google Analytics] y únela a `Total Spent Per Campaign` datos de [!DNL Facebook Ads] para obtener una imagen completa de la cantidad de compromiso que le está costando.

Con la variable [!DNL Google Analytics Live] integración, por otro lado, cada [!DNL Google Analytics] es como un pequeño silo que no está almacenado en su [!DNL MBI] almacén de datos.

## Relacionado:

* [Conexión [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
