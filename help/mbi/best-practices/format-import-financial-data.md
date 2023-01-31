---
title: Formato e importación de datos financieros
description: Aprenda a dar formato e importar datos financieros.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Formato e importación de datos financieros

En este tema se analiza la mejor manera de importar datos financieros para su análisis en [!DNL MBI].

Una tabla de datos bidimensional entre fichas suele ser el formato utilizado para los datos financieros. Con valores categorizados por etiquetas tanto en columnas como en filas, este tipo de diseño puede ser fácil de ver con ojos humanos y herramientas de hoja de cálculo, pero no es muy sencillo para las bases de datos.

![](../../mbi/assets/crosstab.png)

Para importar y analizar estos datos en [!DNL MBI], la tabla debe acoplarse en una lista unidimensional. Cuando se acopla, cada valor de datos se clasifica por varias etiquetas que están todas en una sola fila, donde cada fila es única o tendría un identificador único, por ejemplo una columna de clave principal.

![](../../mbi/assets/flattened.png)

## Formato de archivos de Excel para importación

Para acoplar una tabla bidimensional utilizando una tabla dinámica de Excel:

1. Abra el archivo con la tabla de datos bidimensional.
1. Abra el Asistente para tablas dinámicas. En Windows, el acceso directo es `Alt-D`. En Mac OSX, introduzca `Command-Option-P`.
1. Select **[!UICONTROL Multiple consolidated ranges]** y haga clic en **[!UICONTROL Next]**.
1. Select **[!UICONTROL I will create the page fields]** y haga clic en **[!UICONTROL Next]**.
1. Seleccione todo el conjunto de datos de la tabla bidimensional, incluidas las etiquetas. Asegúrese de que `0` está seleccionado para el número de campos de página deseados y haga clic en **[!UICONTROL Next]**.
1. Cree la tabla dinámica en una nueva hoja y haga clic en **[!UICONTROL Finish]**.
1. Anule la selección de los campos de columna y fila de la lista de campos.
1. Haga doble clic en el valor numérico resultante para mostrar los datos de origen acoplados en una nueva hoja.
   ![](../../mbi/assets/pivot-table-double-click.png)
1. Guardar como `CSV` archivo.

¡Eso es! La tabla de datos se ha convertido a un formato de lista, preservando toda la información original, y ahora puede [importado a [!DNL MBI]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) para análisis.
