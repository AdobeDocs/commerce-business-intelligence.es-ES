---
title: Uso del Report Builder SQL
description: Obtenga información sobre cómo auditar datos y métricas con el Report Builder SQL para poder comparar los resultados con los datos de la base de datos local.
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
role: Admin, Data Architect, Data Engineer, User
feature: Reports, Data Warehouse Manager, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# [!DNL SQL Report Builder]

El [!DNL SQL Report Builder] se utiliza principalmente para generar nuevos informes e iterar en análisis, pero también se puede utilizar para auditar datos y métricas de forma eficaz. La siguiente información explica cómo auditar datos y métricas mediante el [!DNL SQL Report Builder] para poder comparar los resultados con los datos de la base de datos local.

## Consulta de una métrica

Para empezar, abra el [!DNL SQL Report Builder] navegando a **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. Puede utilizar la barra lateral en la [!DNL SQL] editor para insertar una métrica directamente en la consulta pasando el puntero sobre la métrica y haciendo clic en **[!UICONTROL Insert]**. Esto agrega la definición de consulta de esa métrica al editor. La definición de incluye los siguientes componentes:

- El **operación de métrica** que se está realizando, indicado por `SUM()` en el ejemplo siguiente.
- El **tabla en** la métrica se genera, indicada por la variable `FROM` Cláusula.
- Cualquiera **filtros (y conjuntos de filtros)** que se han agregado a la métrica, indicadas por el `WHERE` en el ejemplo siguiente.
- El componente del **timestamp** (año, mes) en el que se van a solicitar los datos, indicado por el `ORDER BY` en el ejemplo siguiente.

Para tener una vista más clara de la consulta, puede cambiar el formato de su visualización en el campo de consulta. Cuando esté listo, seleccione `Run Query`. Los resultados se rellenan como una tabla en el panel de informe debajo de la consulta.

![](../../assets/run-query-results.gif)

## Restricción de la consulta

Si intenta localizar una discrepancia o un conjunto de datos específicos, debe restringir la consulta a un ejemplo específico para comprobarlo con la base de datos local. Para ello, edite la consulta para que coincida con las restricciones que desee. En el ejemplo siguiente, se restringe la consulta para incluir solo los ingresos a partir del 1 de enero de 2013. Después de actualizar la consulta, seleccione **[!UICONTROL Run Query]** para actualizar los resultados.

![](../../assets/restricting-query.gif)

## Guardado y exportación

Cuando el informe satisfaga sus necesidades, asígnele un nombre distinto y haga clic en **[!UICONTROL Save]** y seleccione el tipo de informe que desea guardar y el tablero. Al auditar métricas, Adobe recomienda guardar el informe como una `Table` y guardarlo en un panel de prueba.

Una vez guardado el informe, vaya a ese panel seleccionando `Go to Dashboard`. Desde allí, puede exportar los datos buscando el informe y seleccionando **[!UICONTROL Options gear > Full `.csv`Exportar]** o **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## Consultas personalizadas

También puede escribir consultas personalizadas y exportar los resultados para compararlos con la base de datos local. Siguiendo las [directrices para la optimización de consultas](../../best-practices/optimizing-your-sql-queries.md), escriba una consulta en el editor SQL. Puede utilizar los botones de la parte superior de la barra lateral para alternar entre listas de tablas y métricas disponibles para usar en [!DNL SQL Report Builder] y agréguelas a la consulta. Cuando la consulta personalizada se ajuste a sus necesidades, puede guardar el informe y exportar esos datos desde el panel.

>[!NOTE]
>
>Si encuentra alguna discrepancia después de auditar los datos, consulte la [Contacto con el soporte: Discrepancias de datos](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html) tema de soporte para obtener más información sobre qué hacer a continuación.
