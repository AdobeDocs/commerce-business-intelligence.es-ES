---
title: Esperado [!DNL Adobe Analytics] Datos
description: Conozca los pasos para conectar su instancia de RDS.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# Esperado [!DNL Adobe Analytics] Datos

La variable [!DNL Adobe Analytics] integración para [!DNL MBI] utiliza la variable [API de informes de Analytics 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>Para asegurarse de obtener los datos esperados, primero puede crear un informe en la variable [!DNL Adobe Analytics] Espacio de trabajo con las métricas y dimensiones que desee. Esto le permite comprobar la compatibilidad y disponibilidad de los datos.

Una tabla por grupo de informes conectado: `report-suite-<ID>`, donde `<ID>` es un ID único generado por [!DNL MBI] - se creará en la Data Warehouse.

El esquema de esta tabla está compuesto por las métricas y dimensiones seleccionadas en el proceso de configuración de la integración. Varias columnas adicionales también se generan mediante [!DNL MBI], con fines de identificación.

Por ejemplo, si seleccionó la siguiente métrica y dimensión durante la configuración:
- `Metric`: `Page views`
- `Dimension`: `Page`

La tabla contendría estas columnas:

| Nombre de columna | Descripción |
| --- | --- |
| `_id` | Esta columna es la clave principal. |
| `_item_hash` | [!DNL MBI] identificador único. Esta columna la crea [!DNL MBI]. |
| `_updated_at` | Esta columna contiene la última vez que se actualizó la fila de datos. Se crea mediante [!DNL MBI]. |
| `start_date` | Fecha de inicio de los datos incluidos para la fila. `start_date` siempre será de 00:00 del mismo día dentro de una fila. |
| `end_date` | Fecha final de los datos incluidos para la fila. `end_date` siempre será de 23:59 del mismo día dentro de una fila. |
| `page_views` | Métrica seleccionada: Número total de vistas de página para el período de tiempo identificado. |
| `page` | Dimensión seleccionada: Nombres de páginas individuales con vistas rastreadas. |

Controle qué métricas y dimensiones seleccionadas tienen datos disponibles en su [!DNL MBI] usando la variable *sincronizar* o *unsync* en el `Data Warehouse` página. Las columnas que no se están sincronizando aparecen en gris. Si deja de sincronizar una columna, puede empezar a sincronizarla de nuevo más tarde.

## Limitaciones actuales

Esta sección describe las limitaciones de la variable [!DNL Adobe Analytics] integración para [!DNL MBI].

| Limitación | Descripción |
| --- | --- |
| `Historical data period` | Al igual que con otras integraciones de terceros, la variable [!DNL Adobe Analytics] la integración extrae una cantidad limitada de datos históricos y, a continuación, mantiene los datos actualizados. El periodo histórico se configura en 2 semanas. |
| `Empty component combinations` | Algunas combinaciones de métricas y dimensiones no contienen datos. Si se selecciona una combinación de este tipo para la replicación, [!DNL MBI] excluye la columna de la tabla replicada. Para evitar seleccionar una combinación de este tipo, primero puede crear un informe en la [[!DNL Adobe Analytics] Espacio de trabajo](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=en) para verificar que obtendrá los datos esperados. |
| `Re-authorization cadence` | Reautorización del [!DNL Adobe Analytics] actualmente se requiere cada dos semanas. Para volver a autorizar, vaya a la página Editar para la integración y haga clic en **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] proporciona datos de métricas de una dimensión a la vez. Si selecciona varias dimensiones durante la configuración, cada fila del [!DNL MBI] La tabla contendrá un solo valor de dimensión y números nulos para cada dimensión. |
