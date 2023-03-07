---
title: Formato e importación de datos financieros
description: Aprenda a dar formato e importar datos financieros.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Dar formato e importar datos financieros

En este tema se describe la mejor manera de importar datos financieros para su análisis en [!DNL MBI].

Una tabla de datos bidimensional entre pestañas suele ser el formato utilizado para los datos financieros. Con valores clasificados por etiquetas tanto en columnas como en filas, este tipo de diseño puede ser fácil de ver con ojos humanos y herramientas de hoja de cálculo, pero no es sencillo para las bases de datos.

![](../../mbi/assets/crosstab.png)

Para importar y analizar estos datos en [!DNL MBI], la tabla debe acoplarse en una lista unidimensional. Cuando se acopla, cada valor de datos se clasifica por varias etiquetas que se encuentran todas en una sola fila, donde cada fila es única o tendría un identificador único, por ejemplo una columna de clave principal.

![](../../mbi/assets/flattened.png)

## Formato de archivos de Excel para importar

Para acoplar una tabla bidimensional con una tabla dinámica de Excel:

1. Abra el archivo con la tabla de datos bidimensional.
1. Abra el Asistente para tablas dinámicas. En Windows, el método abreviado es `Alt-D`. En Mac OS, introduzca `Command-Option-P`.
1. Seleccionar **[!UICONTROL Multiple consolidated ranges]** y haga clic en **[!UICONTROL Next]**.
1. Seleccionar **[!UICONTROL I will create the page fields]** y haga clic en **[!UICONTROL Next]**.
1. Seleccione todo el conjunto de datos en la tabla bidimensional, incluidas las etiquetas. Asegúrese de que `0` está seleccionado para el número de campos de página deseados y haga clic en **[!UICONTROL Next]**.
1. Cree la tabla dinámica en una hoja nueva y haga clic en **[!UICONTROL Finish]**.
1. Anule la selección de los campos de columna y fila de la lista de campos.
1. Haga doble clic en el valor numérico resultante para mostrar los datos de origen aplanados en una hoja nueva.
   ![](../../mbi/assets/pivot-table-double-click.png)
1. Guardar como `CSV` archivo.

¡Eso es todo! La tabla de datos se ha convertido a un formato de lista, conservando toda su información original, y ahora se puede [importado a [!DNL MBI]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) para su análisis.
