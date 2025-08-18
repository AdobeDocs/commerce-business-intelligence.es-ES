---
title: Se Esperaban  [!DNL Adobe Analytics] Datos
description: Conozca los pasos para conectar su instancia de RDS.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Se esperaban [!DNL Adobe Analytics] datos

La integración de [!DNL Adobe Analytics] para [!DNL Adobe Commerce Intelligence] usa la [API de informes de Analytics 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>Para asegurarse de obtener los datos esperados, primero puede generar un informe en la Workspace [!DNL Adobe Analytics] con las métricas y dimensiones deseadas. Esto le permite comprobar la compatibilidad y disponibilidad de los datos.

Se crea en su Data Warehouse una tabla por cada grupo de informes conectado llamada `report-suite-<ID>` (donde `<ID>` es un identificador único generado por [!DNL Commerce Intelligence]).

El esquema de esta tabla está compuesto por las métricas y dimensiones seleccionadas en el proceso de configuración de la integración. [!DNL Commerce Intelligence] también genera varias columnas adicionales para fines de identificación.

Por ejemplo, si seleccionó la siguiente métrica y dimensión durante la configuración:
- `Metric`: `Page views`
- `Dimension`: `Page`

La tabla contendría estas columnas:

| Nombre de columna | Descripción |
| --- | --- |
| `_id` | Esta columna es la clave principal. |
| `_item_hash` | [!DNL Commerce Intelligence] identificador único. Esta columna la creó [!DNL Commerce Intelligence]. |
| `_updated_at` | Esta columna contiene la última vez que se actualizó la fila de datos. Se creó por [!DNL Commerce Intelligence]. |
| `start_date` | Fecha de inicio de los datos incluidos para la fila. `start_date` siempre es 00:00 del mismo día dentro de una fila. |
| `end_date` | Fecha de finalización de los datos incluidos para la fila. `end_date` siempre es 23:59 del mismo día dentro de una fila. |
| `page_views` | Métrica seleccionada: número total de vistas de página para el período de tiempo identificado. |
| `page` | Dimensión seleccionada: nombres de página individuales con vistas rastreadas. |

Controle qué métricas y dimensiones seleccionadas tienen datos disponibles en su tabla [!DNL Commerce Intelligence] mediante las opciones *sync* o *unsync* de la página `Data Warehouse`. Las columnas que no se están sincronizando actualmente aparecen en gris. Si deja de sincronizar una columna, puede empezar a sincronizarla de nuevo más tarde.

## Limitaciones actuales

Esta sección describe las limitaciones de la integración de [!DNL Adobe Analytics] para [!DNL Commerce Intelligence].

| Limitación | Descripción |
| --- | --- |
| `Historical data period` | Al igual que con otras integraciones de terceros, la integración de [!DNL Adobe Analytics] extrae una cantidad limitada de datos históricos y, a continuación, continúa manteniendo los datos actualizados. El periodo histórico se configura en 2 semanas. |
| `Empty component combinations` | Algunas combinaciones de métricas y dimensiones no contienen datos. Si se selecciona una combinación de este tipo para la replicación, [!DNL Commerce Intelligence] excluye la columna de la tabla replicada. Para evitar seleccionar una combinación de este tipo, primero puede crear un informe en [[!DNL Adobe Analytics] Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html) para comprobar que obtiene los datos esperados. |
| `Re-authorization cadence` | Se requiere la reautorización de la integración de [!DNL Adobe Analytics] cada dos semanas. Para volver a autorizar, vaya a la página Editar de la integración y haga clic en **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] proporciona datos de métrica para una dimensión a la vez. Si selecciona varias dimensiones durante la configuración, cada fila de la tabla [!DNL Commerce Intelligence] contendrá un solo valor de dimensión y valores nulos para cada otra dimensión. |
