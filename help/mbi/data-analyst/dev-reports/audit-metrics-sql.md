---
title: Uso de SQL Report Builder
description: Obtenga información sobre cómo auditar datos y métricas mediante SQL Report Builder para poder comparar los resultados con los datos de la base de datos local.
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
role: Admin, Developer, User
feature: Reports, Data Warehouse Manager, SQL Report Builder
TQID: https://experienceleague.adobe.com/7Yx7Kpir-xjz5TPuajN7CFsLjWAbY0AT3bKtBabA5Wk
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 507
ht-degree: 0%

---

# [!DNL SQL Report Builder]

[!DNL SQL Report Builder] se usa principalmente para generar nuevos informes e iterar en los análisis, pero también se puede usar para auditar datos y métricas de forma eficaz. La siguiente información explica cómo auditar datos y métricas usando [!DNL SQL Report Builder] para poder comparar los resultados con los datos de la base de datos local.

## Consulta de una métrica

Para empezar, abra [!DNL SQL Report Builder] navegando hasta **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. Puede usar la barra lateral del editor [!DNL SQL] para insertar una métrica directamente en la consulta pasando el puntero sobre la métrica y haciendo clic en **[!UICONTROL Insert]**. Esto agrega la definición de consulta de esa métrica al editor. La definición de incluye los siguientes componentes:

- Se está realizando la **operación de métrica**, indicada por `SUM()` en el ejemplo siguiente.
- La **tabla en** en la que se creó la métrica, indicada por la cláusula `FROM`.
- Cualquier **filtro (y conjunto de filtros)** que se haya agregado a la métrica, indicado por la cláusula `WHERE` en el ejemplo siguiente.
- Componente de **timestamp** (año, mes) en el que se van a ordenar los datos, indicado por la cláusula `ORDER BY` en el ejemplo siguiente.

Para tener una vista más clara de la consulta, puede cambiar el formato de su visualización en el campo de consulta. Cuando esté listo, seleccione `Run Query`. Los resultados se rellenan como una tabla en el panel de informe debajo de la consulta.

![Demostración animada de la ejecución de una consulta SQL y de la visualización de resultados](../../assets/run-query-results.gif)

## Restricción de la consulta

Si intenta localizar una discrepancia o un conjunto de datos específicos, debe restringir la consulta a un ejemplo específico para comprobarlo con la base de datos local. Para ello, edite la consulta para que coincida con las restricciones que desee. En el ejemplo siguiente, se restringe la consulta para incluir solo los ingresos a partir del 1 de enero de 2013. Después de actualizar la consulta, vuelva a seleccionar **[!UICONTROL Run Query]** para actualizar los resultados.

![Demostración animada de restricción de consulta con filtros](../../assets/restricting-query.gif)

## Guardado y exportación

Cuando el informe satisfaga sus necesidades, asígnele un nombre distinto, haga clic en **[!UICONTROL Save]** y seleccione el tipo de informe que desea guardar y el tablero. Al auditar métricas, Adobe recomienda guardar el informe como `Table` y guardarlo en un tablero de pruebas.

Una vez guardado el informe, vaya a ese panel seleccionando `Go to Dashboard`. Desde allí, puede exportar los datos buscando el informe y seleccionando **[!UICONTROL Options gear > Full `.csv`Export]** o **[!UICONTROL Full Excel Export]**.

![Demostración animada de exportación de datos de tablero](../../assets/export-dboard-data.gif)

## Consultas personalizadas

También puede escribir consultas personalizadas y exportar los resultados para compararlos con la base de datos local. Siguiendo las [directrices para la optimización de consultas](../../best-practices/optimizing-your-sql-queries.md), escriba una consulta en el editor SQL. Puede utilizar los botones de la parte superior de la barra lateral para alternar entre listas de tablas y métricas disponibles para usar en [!DNL SQL Report Builder] y agregarlas a la consulta. Cuando la consulta personalizada se ajuste a sus necesidades, puede guardar el informe y exportar esos datos desde el panel.

>[!NOTE]
>
>Si encuentra alguna discrepancia después de auditar sus datos, consulte el tema de soporte técnico de [Contacto con el soporte técnico: Discrepancias de datos](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html?lang=es) para obtener más información sobre qué hacer a continuación.
