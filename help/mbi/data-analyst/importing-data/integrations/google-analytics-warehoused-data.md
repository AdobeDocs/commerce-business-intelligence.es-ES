---
title: Datos Almacenados De Google Analytics Esperados
description: Aprenda a interactuar con los datos almacenados de los Google Analytics.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# Previsto [!DNL Google Analytics Warehoused] Datos

>[!NOTE]
>
>Requiere [Permisos de administración](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>Algunos datos se utilizaron con el permiso de tus amigos en [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] integración en [!DNL Commerce Intelligence] utiliza el [!DNL Google Analytics] [API de informes principales](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>Para evitar resultados inesperados o sin sentido, confirme que las dimensiones que utilice son las siguientes [compatible con una o más métricas](https://ga-dev-tools.google/dimensions-metrics-explorer/) que utiliza en la `Report Builder`.

Una sola tabla denominada `report` : se crea en la Data Warehouse.

El esquema de esta tabla está compuesto por las métricas y los Dimension seleccionados durante el proceso de configuración y otras dos columnas: `start-date` y `end-date`.

Si, por ejemplo, seleccionó las siguientes métricas y Dimension durante la configuración:

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

La tabla sería como el ejemplo siguiente.

| **Nombre de columna** | **Descripción** |
|-----|-----|
| `\_id` | Esta columna es la `primary key`. |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence] identificador único. Esta columna la crea [!DNL Commerce Intelligence]. |
| `\_updated\_at` | Esta columna contiene la última vez que se actualizó la fila de datos. Esta columna la crea [!DNL Commerce Intelligence]. |
| `start-date` | Identificación del día para el que es la fila. |
| `end-date` | Identificación del día para el que es la fila. |
| `month` | Dimensión seleccionada: mes de la sesión, un entero de dos dígitos comprendido entre 01 y 12. |
| `users` | Métrica seleccionada: número total de usuarios durante el período de tiempo solicitado. |

{style="table-layout:auto"}

## ¿Cuál es la diferencia entre [!DNL Google Analytics Warehoused] y [!DNL Live Integration]

El principal diferenciador es que se almacena una integración ([!DNL Google Analytics Warehoused]), y la otra no es ([!DNL Google Analytics Live]). En casos de [!DNL Google Analytics Warehoused], esto permite manipular los [!DNL Google Analytics] y le ofrece la posibilidad de combinar [!DNL Google Analytics] y otras fuentes de datos para crear informes reveladores.

Observe lo siguiente [!DNL Google Analytics] añada campañas para ver un ejemplo de lo que se puede hacer desde el punto de vista de la manipulación. Supongamos que ha tenido varias campañas publicitarias para el cuarto trimestre con nombres diferentes. Las campañas fueron el resultado de una iniciativa de marketing específica. Con los datos almacenados, puede crear una columna que encuentre los nombres de campaña en cuestión y devuelva el nombre de la iniciativa del cuarto trimestre de `Operation Dumbo`.

El aspecto combinado permite [!DNL Google Analytics] datos que se van a unir a otros datos para llevar a cabo análisis. Por ejemplo, tome `Total Time On Site By Ad Campaign` datos de [!DNL Google Analytics] y únete a él en contra `Total Spent Per Campaign` datos de [!DNL Facebook Ads] para obtener una imagen completa de cuánto le está costando la participación.

Con el [!DNL Google Analytics Live] integración, por otro lado, cada [!DNL Google Analytics] es como un pequeño silo que no se almacena en su [!DNL Commerce Intelligence] Data Warehouse.

## Relacionado:

* [Conectando [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
