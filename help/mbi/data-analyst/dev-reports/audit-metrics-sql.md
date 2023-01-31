---
title: Trabajo con el Report Builder SQL
description: Obtenga información sobre cómo auditar datos y métricas mediante el Report Builder SQL para poder comparar los resultados con los datos de la base de datos local.
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# `SQL Report Builder`

La variable `SQL Report Builder` se utiliza principalmente para generar nuevos informes e iterar en los análisis, pero también se puede utilizar para auditar de forma eficaz los datos y las métricas. La siguiente información explica cómo auditar datos y métricas utilizando la variable `SQL Report Builder` para poder comparar los resultados con los datos de la base de datos local.

## Consulta de una métrica

Para empezar, abra el `SQL Report Builder` navegando a **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. Puede utilizar la barra lateral del editor SQL para insertar una métrica directamente en la consulta pasando el cursor sobre la métrica y haciendo clic en **[!UICONTROL Insert]**. Esto agregará la definición de consulta de esa métrica al editor. La definición incluirá los siguientes componentes:

- La variable **operación de métrica** se está realizando, indicado por SUM() en el ejemplo siguiente.
- La variable **tabla en** que crea la métrica, indicada por la cláusula FROM.
- Cualquiera **filtros (y conjuntos de filtros)** que se han agregado a la métrica, indicada por la cláusula WHERE en el ejemplo siguiente.
- El componente de la variable **timestamp** (año, mes) en el que se deben ordenar los datos, indicada por la cláusula ORDER BY del ejemplo siguiente.

Si desea tener una vista más clara de la consulta, puede cambiar el formato de cómo se muestra en el campo de consulta. Cuando esté listo, seleccione `Run Query`. Los resultados se rellenarán como una tabla en el panel de informe debajo de la consulta.

![](../../assets/run-query-results.gif)

## Restricción de la consulta

Si está intentando localizar una discrepancia o un conjunto de datos específicos, debe restringir la consulta a una muestra específica para comprobarla con la base de datos local. Puede hacerlo editando la consulta para que coincida con las restricciones deseadas. En el siguiente ejemplo, se restringe la consulta para incluir solo los ingresos a partir del 1 de enero de 2013 o posteriores. Después de actualizar la consulta, seleccione **[!UICONTROL Run Query]** para actualizar los resultados.

![](../../assets/restricting-query.gif)

## Guardado y exportación

Cuando el informe satisfaga sus necesidades, guárdelo en un tablero asignando un nombre distinto al informe y haciendo clic en **[!UICONTROL Save]**, y seleccionando el tipo de informe que desea guardar y el tablero. Al auditar métricas, se recomienda guardar el informe como un `Table` y guardarlo en un panel de prueba.

Una vez guardado el informe, vaya a ese tablero seleccionando `Go to Dashboard`. Desde allí, puede exportar los datos buscando el informe y seleccionando **[!UICONTROL Options gear > Full `.csv`Exportar]** o **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## Consultas personalizadas

También puede escribir consultas personalizadas y exportar los resultados para compararlos con la base de datos local. A continuación se muestra la [directrices para la optimización de consultas](../../best-practices/optimizing-your-sql-queries.md), escriba una consulta en el editor SQL. Puede utilizar los botones de la parte superior de la barra lateral para alternar entre listas de tablas y métricas disponibles para usar en la variable `SQL Report Builder` y agréguelos a la consulta. Cuando la consulta personalizada se ajuste a sus necesidades, puede guardar el informe y exportar esos datos desde el panel.

### ¿Sigue tropezado?

Si encuentra alguna discrepancia después de auditar sus datos, consulte la [Contactar con el servicio de asistencia técnica: Discrepancias de datos](https://support.magento.com/hc/en-us/articles/360016505312) artículo de soporte técnico para obtener más información sobre qué hacer a continuación.
