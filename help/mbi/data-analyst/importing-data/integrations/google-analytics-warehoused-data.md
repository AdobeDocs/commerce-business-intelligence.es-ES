---
title: Datos esperados del Google Analytics Warehouse
description: Aprenda a interactuar con los datos almacenados en Google Analytics.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# Se esperaban [!DNL Google Analytics Warehoused] datos

>[!NOTE]
>
>Requiere [permisos de administrador](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>Parte de la información se usó con el permiso de tus amigos en [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

La integración de [!DNL Google Analytics Warehoused] en [!DNL Commerce Intelligence] usa la [!DNL Google Analytics] [API de informes principales](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>Para evitar resultados inesperados o sin sentido, confirme que las dimensiones que utilice son [compatibles con una o más métricas](https://ga-dev-tools.google/dimensions-metrics-explorer/) que utilice en `Report Builder`.

Se crea una sola tabla denominada `report` en su Data Warehouse.

El esquema de esta tabla está compuesto por las métricas y dimensiones seleccionadas durante el proceso de configuración y otras dos columnas: `start-date` y `end-date`.

Por ejemplo, si seleccionó las siguientes métricas y dimensiones durante la configuración:

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

La tabla sería como el ejemplo siguiente.

| **Nombre de columna** | **Descripción** |
|-----|-----|
| `\_id` | Esta columna es la `primary key`. |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence] identificador único. Esta columna la creó [!DNL Commerce Intelligence]. |
| `\_updated\_at` | Esta columna contiene la última vez que se actualizó la fila de datos. Esta columna la creó [!DNL Commerce Intelligence]. |
| `start-date` | Identificación del día para el que es la fila. |
| `end-date` | Identificación del día para el que es la fila. |
| `month` | Dimensión seleccionada: mes de la sesión, un entero de dos dígitos comprendido entre 01 y 12. |
| `users` | Métrica seleccionada: número total de usuarios durante el período de tiempo solicitado. |

{style="table-layout:auto"}

## Cuál es la diferencia entre [!DNL Google Analytics Warehoused] y [!DNL Live Integration]

El principal diferenciador es que una integración está almacenada ([!DNL Google Analytics Warehoused]) y la otra no ([!DNL Google Analytics Live]). En los casos de [!DNL Google Analytics Warehoused], esto permite manipular los datos de [!DNL Google Analytics] y permite combinar [!DNL Google Analytics] y otras fuentes de datos para crear informes profundos.

Consulte [!DNL Google Analytics] campañas de publicidad para ver un ejemplo de lo que se puede hacer desde el punto de vista de la manipulación. Supongamos que ha tenido varias campañas publicitarias para el cuarto trimestre con nombres diferentes. Las campañas fueron el resultado de una iniciativa de marketing específica. Con los datos almacenados, puede crear una columna que encuentre los nombres de campaña en cuestión y devuelva el nombre de la iniciativa del cuarto trimestre de `Operation Dumbo`.

El aspecto de combinación permite que los datos de [!DNL Google Analytics] se unan a otros datos para realizar análisis. Por ejemplo, tome `Total Time On Site By Ad Campaign` datos de [!DNL Google Analytics] y únase a ellos con `Total Spent Per Campaign` datos de [!DNL Facebook Ads] para obtener una idea completa de cuánto le está costando la participación.

Con la integración de [!DNL Google Analytics Live] por otro lado, cada gráfico de [!DNL Google Analytics] es como un pequeño silo que no está almacenado en su Data Warehouse de [!DNL Commerce Intelligence].

## Relacionado:

* [Conectando [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
