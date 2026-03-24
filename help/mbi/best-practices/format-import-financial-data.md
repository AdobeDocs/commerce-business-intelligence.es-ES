---
title: Formato e importación de datos financieros
description: Aprenda a dar formato e importar datos financieros.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
role: Admin, Developer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/O1WKa98rRVw1dcgNQPsORit2gmZNn1Wi7H-Q4J7KcA0
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 278
ht-degree: 0%

---

# Dar formato e importar datos financieros

En este tema se describe la mejor manera de importar datos financieros para su análisis en [!DNL Adobe Commerce Intelligence].

Una tabla de datos bidimensional entre pestañas suele ser el formato utilizado para los datos financieros. Con valores clasificados por etiquetas tanto en columnas como en filas, este tipo de diseño puede ser fácil de ver con ojos humanos y herramientas de hoja de cálculo, pero no es sencillo para las bases de datos.

![Formato de tabla cruzada que muestra datos en el diseño de tabla dinámica](../../mbi/assets/crosstab.png)

Para importar y analizar estos datos en [!DNL Commerce Intelligence], la tabla debe acoplarse a una lista unidimensional. Cuando se acopla, cada valor de datos se clasifica por varias etiquetas que se encuentran todas en una sola fila, donde cada fila es única o tendría un identificador único, por ejemplo una columna de clave principal.

![Formato plano que muestra datos en diseño de columnas](../../mbi/assets/flattened.png)

## Formato de archivos de Excel para importar

Para acoplar una tabla bidimensional con una tabla dinámica [!DNL Excel]:

1. Abra el archivo con la tabla de datos bidimensional.
1. Abra el Asistente para tablas dinámicas. En [!DNL Windows], el acceso directo es `Alt-D`. En [!DNL Mac OS], escriba `Command-Option-P`.
1. Seleccione **[!UICONTROL Multiple consolidated ranges]** y haga clic en **[!UICONTROL Next]**.
1. Seleccione **[!UICONTROL I will create the page fields]** y haga clic en **[!UICONTROL Next]**.
1. Seleccione todo el conjunto de datos en la tabla bidimensional, incluidas las etiquetas. Asegúrese de que `0` esté seleccionado para el número de campos de página deseados y haga clic en **[!UICONTROL Next]**.
1. Cree la tabla dinámica en una hoja nueva y haga clic en **[!UICONTROL Finish]**.
1. Anule la selección de los campos de columna y fila de la lista de campos.
1. Haga doble clic en el valor numérico resultante para mostrar los datos de origen aplanados en una hoja nueva.
   ![Lista de campos de tabla dinámica de Excel que muestra doble clic para expandir](../../mbi/assets/pivot-table-double-click.png)
1. Guardar como archivo de `CSV`.

## Ajuste

La tabla de datos se ha convertido a un formato de lista, conservando toda su información original, y ahora se puede [importar a [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) para su análisis.
