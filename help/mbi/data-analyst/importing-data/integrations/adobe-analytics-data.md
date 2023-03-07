---
title: Previsto [!DNL Adobe Analytics] Datos
description: Conozca los pasos para conectar su instancia de RDS.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# Previsto [!DNL Adobe Analytics] Datos

El [!DNL Adobe Analytics] integración para [!DNL MBI] utiliza el [API de informes de Analytics 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>Para garantizar la obtención de los datos esperados, primero puede crear un informe en la variable [!DNL Adobe Analytics] Workspace con las métricas y dimensiones que desee. Esto le permite comprobar la compatibilidad y disponibilidad de los datos.

Una tabla por grupo de informes conectado (llamada `report-suite-<ID>`, donde `<ID>` es un ID único generado por [!DNL MBI] : se crea en la Data Warehouse.

El esquema de esta tabla está compuesto por las métricas y dimensiones seleccionadas en el proceso de configuración de la integración. Varias columnas adicionales también se generan mediante [!DNL MBI], con fines de identificación.

Por ejemplo, si seleccionó la siguiente métrica y dimensión durante la configuración:
- `Metric`: `Page views`
- `Dimension`: `Page`

La tabla contendría estas columnas:

| Nombre de columna | Descripción |
| --- | --- |
| `_id` | Esta columna es la clave principal. |
| `_item_hash` | [!DNL MBI] identificador único. Esta columna la crea [!DNL MBI]. |
| `_updated_at` | Esta columna contiene la última vez que se actualizó la fila de datos. Lo crea un [!DNL MBI]. |
| `start_date` | Fecha de inicio de los datos incluidos para la fila. `start_date` siempre es 00:00 del mismo día dentro de una fila. |
| `end_date` | Fecha de finalización de los datos incluidos para la fila. `end_date` siempre es 23:59 del mismo día dentro de una fila. |
| `page_views` | Métrica seleccionada: número total de vistas de página para el período de tiempo identificado. |
| `page` | Dimensión seleccionada: nombres de página individuales con vistas rastreadas. |

Controle qué métricas y dimensiones seleccionadas tienen datos disponibles en su [!DNL MBI] mediante el uso de *sincronizar* o *desincronizar* opciones en la `Data Warehouse` página. Las columnas que no se están sincronizando actualmente aparecen en gris. Si deja de sincronizar una columna, puede empezar a sincronizarla de nuevo más tarde.

## Limitaciones actuales

Esta sección describe las limitaciones de la [!DNL Adobe Analytics] integración para [!DNL MBI].

| Limitación | Descripción |
| --- | --- |
| `Historical data period` | Al igual que con otras integraciones de terceros, la variable [!DNL Adobe Analytics] La integración de extrae una cantidad limitada de datos históricos y, a continuación, continúa manteniendo los datos actualizados. El periodo histórico se configura en 2 semanas. |
| `Empty component combinations` | Algunas combinaciones de métricas y dimensiones no contienen datos. Si se selecciona dicha combinación para la replicación, [!DNL MBI] excluye la columna de la tabla replicada. Para evitar seleccionar una combinación de este tipo, primero puede crear un informe en la variable [[!DNL Adobe Analytics] Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=en) para verificar que obtiene los datos esperados. |
| `Re-authorization cadence` | Reautorización de la [!DNL Adobe Analytics] La integración de se requiere cada dos semanas. Para volver a autorizar, vaya a la página Editar de la integración y haga clic en **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] proporciona datos de métricas para dimensiones de una en una. Si selecciona varias dimensiones durante la configuración, cada fila de la [!DNL MBI] La tabla contiene un valor de dimensión único y valores nulos para cada otra dimensión. |
