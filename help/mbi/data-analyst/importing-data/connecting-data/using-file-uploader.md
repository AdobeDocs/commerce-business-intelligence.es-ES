---
title: Utilizar el cargador de archivos
description: Aprenda a colocar todos los datos en una sola Data Warehouse.
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 0%

---

# Utilizar el cargador de archivos

>[!NOTE]
>
>Requiere [Permisos de administración](../../../administrator/user-management/user-management.md).

[!DNL Adobe Commerce Intelligence] es potente no solo por sus características de visualización, sino porque le permite colocar todos los datos en una sola Data Warehouse. Incluso los datos que se encuentran fuera de sus bases de datos e integraciones se pueden incorporar a [!DNL Commerce Intelligence] mediante la herramienta de carga de archivos en el Administrador de Datas Warehouse.

Utilice campañas de publicidad como ejemplo. Si está ejecutando campañas en línea y sin conexión, no puede obtener una imagen completa si solo está analizando los datos de una integración en línea. Al cargar una hoja de cálculo con los datos de campañas sin conexión, puede analizar ambos conjuntos de datos y comprender mejor el rendimiento de la campaña.

## Restricciones y requisitos {#require}

1. **El único formato admitido para la carga de archivos es `CSV` o`comma separated values`**. Si está trabajando en Excel, puede utilizar la función Guardar como para guardar el archivo en `.csv` formato.
1. **`CSV`Los archivos deben utilizar`UTF-8 encoding`**. La mayoría de las veces, esto no es un problema. Si aparece este error al cargar un archivo, [consulte este artículo de soporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolving-utf-8-errors-for-csv-file-uploads.html).
1. **Los archivos no pueden superar los 100 MB**. Si el archivo es más grande que este, separe la tabla en fragmentos y guárdela como archivos individuales. Puede anexar los datos después de cargar el archivo inicial.
1. **Todas las tablas deben tener un`primary key`**. Debe haber al menos una columna en la tabla que pueda utilizarse como `primary key`o un identificador único para cada fila de la tabla. Cualquier columna designada como `primary key` lata *nunca* ser nulo. A `primary key` puede ser tan simple como agregar una columna que da un número a cada fila, o puede ser dos columnas concatenadas para crear una columna de valores únicos (por ejemplo, `campaign name` y `date`).

   Si una columna (o columnas) se designa como única pero hay duplicados, las filas duplicadas no se importan.

## Formato de datos para carga {#formatting}

Antes de cargar los datos en [!DNL Commerce Intelligence], compruebe que tiene el formato indicado en las directrices de esta sección.

### Fila de encabezado {#header}

Para asegurarse de que las columnas están etiquetadas e importadas correctamente, asegúrese de que la primera fila de la hoja de cálculo sea un encabezado que describa los datos de cada columna.

Los nombres de columna deben ser únicos y contener solo letras, números, espacios y estos símbolos: `$ % # /`. Si el nombre de una columna contiene una coma, se divide en dos columnas cuando se carga el archivo. Además, Adobe recomienda que haya menos de 85 columnas en el archivo para optimizar la velocidad de actualización.

### Datos con comas {#commas}

Porque los archivos tienen que estar en `CSV` , el uso de comas puede causar problemas al cargar datos. `CSV` Los archivos de utilizan comas para indicar nuevos valores, por lo tanto, una columna con un nombre como `Campaigns`, `August` se lee como dos columnas (`Campaigns` y `August`) en lugar de uno, desplazando todos los datos en una fila. El Adobe recomienda evitar las comas siempre que sea posible. Puede utilizar `Data Preview` para ver si los datos se muestran correctamente una vez que se completa una actualización.

### Fechas

Cualquier conjunto de datos que incluya fechas debe utilizar el [formato de fecha estándar](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` o `MM/DD/YYYY`.

### Caracteres especiales

No se aceptan algunos caracteres especiales. Por ejemplo, el símbolo de barra vertical `& # 1 2 4` se interpreta como la creación de una columna y provoca errores al cargar un archivo.

### Números decimales

Los valores de moneda deben tener el tipo de datos `Decimal Number` y estas columnas se redondean automáticamente a dos decimales en la Data Warehouse. Si no desea redondear los números decimales o si tiene un grado de precisión mayor que este, debe seleccionar la opción `Non-Currency Decimal Number` tipo de datos.

### Porcentajes

Los porcentajes deben introducirse como decimales. Por ejemplo:

| **Derecha:** | **Incorrecto:** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style="table-layout:auto"}

### Valores con ceros a la izquierda o ambas {#zeroes}

Algunos valores del archivo, como los códigos postales y los ID, pueden comenzar o finalizar con ceros. Para asegurarse de que los ceros se retienen y cargan correctamente, puede cambiar el tipo de formato (por ejemplo, [de número a texto](https://support.microsoft.com/en-us/office/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4?ui=en-us&amp;rs=en-us&amp;ad=us)) o aplique formato de número.

Uso `US ZIP codes` como ejemplo de cómo cambiar el formato de números. Entrada [!DNL Excel], resalte la columna que contiene `ZIP codes` y [cambiar el formato de número](https://support.microsoft.com/en-us/office/display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d?ui=en-us&amp;rs=en-us&amp;ad=us) hasta `ZIP code`. También puede seleccionar un formato de número personalizado y, en el `Type` ventana, introduzca `00000`. Tenga en cuenta que este método podría presentar problemas si algunos códigos tienen el formato `00000` y otros son `00000-0000`.

El `Type` puede ser [tiene un formato diferente para dar cabida a otros tipos de datos](https://support.microsoft.com/en-us/office/keeping-leading-zeros-and-large-numbers-1bf7b935-36e1-4985-842f-5dfa51f85fe7?correlationid=e1d4c2d3-cd5d-4a14-999d-437800274a90&amp;ui=en-us&amp;rs=en-us&amp;ad=us), como los ID. Si un `ID` tiene nueve dígitos de longitud; por ejemplo, la variable `Type` podría ser `000000000` o `000-000-000`. Esto cambiaría `123456` hasta `000-123-456`.

Para [!DNL Google Docs] y [!DNL Apple Numbers] recursos, consulte la [Relacionado](#related) al final de esta página.

## Carga de datos {#uploading}

Ahora que la hoja de cálculo tiene el formato correcto y [!DNL Commerce Intelligence]compatible con, añádalo a su Data Warehouse.

1. Para empezar, vaya a **[!UICONTROL Data** > **File Uploads]**.

1. Haga clic en **[!UICONTROL Upload to New Table]** pestaña.

1. Clic **[!UICONTROL Choose File]** y seleccione el archivo. Clic **[!UICONTROL Open]** para iniciar la carga.

   Una vez finalizada la carga, una lista de las columnas [!DNL Commerce Intelligence] que se encuentran en el archivo se muestra.

1. Compruebe que los nombres de columna y los tipos de datos son correctos. Concretamente, compruebe que todas las columnas de fecha se lean como fechas y no como números.

   >[!NOTE]
   >
   >El `datatype` es importante, por lo que no omita este paso.

1. Seleccione la columna (o columnas) que conforman la variable `primary key` para la tabla mediante las casillas de verificación situadas bajo el icono de clave.

1. Asigne un nombre a la tabla.

1. Haga clic **[!UICONTROL Save Table]**.

A *¡Correcto!* El mensaje aparece en la parte superior de la pantalla después de guardar la tabla.

Si necesita una imagen, observe todo el proceso:

![](../../../assets/fileupload.gif)

Las tablas cargadas se muestran en **Cargas de archivos** de la lista de tablas (en las opciones Todas las tablas y Tablas sincronizadas) del Administrador de Datas Warehouse:

![](../../../assets/upload-tables.png)

## Actualización o adición de datos a una tabla existente {#appending}

¿Tiene nuevos datos para agregar a un archivo que ya ha cargado? No hay problema: puede actualizar y anexar datos fácilmente en [!DNL Commerce Intelligence].

1. Para empezar, vaya a **[!UICONTROL Manage Data** > **File Uploads]**.

1. Haga clic en **[!UICONTROL Edit/Upload `.csv`a tablas existentes]** pestaña.

1. En el menú desplegable, haga clic en el nombre de la tabla que desee actualizar o anexar.

1. Utilice el menú desplegable para seleccionar la opción para administrar filas duplicadas:

   | Opción | Descripción |
   |---|---|
   | `Overwrite old row with new row` | Esto sobrescribe los datos existentes con datos nuevos si una fila tiene la misma clave principal en la tabla existente y en el nuevo archivo. Es el método que se utiliza para columnas con valores que cambian con el tiempo; por ejemplo, una columna Estado. Los datos existentes se sobrescriben y actualizan con los nuevos datos. Las filas con claves principales que no están en la tabla existente se agregan como filas nuevas. |
   | `Retain old row; discard new row` | Esto hace que se ignoren los nuevos datos si una fila tiene la misma clave principal en la tabla existente y en el nuevo archivo. |
   | `Purge all existing rows first and ignore duplicate keys within the file` | Esto elimina los datos existentes y los reemplaza por los nuevos datos del archivo. Utilice esta opción únicamente si no necesita ninguno de los datos de la tabla existente. |

1. Clic **[!UICONTROL Choose File]** y seleccione el archivo.

1. Clic **[!UICONTROL Open]** para iniciar la carga.

   Una vez finalizada la carga, [!DNL Commerce Intelligence] validará la estructura de datos del archivo. A *¡Correcto!* El mensaje aparece en la parte superior de la pantalla después de guardar la tabla.

## Disponibilidad de datos {#availability}

Al igual que las columnas calculadas, los datos de las cargas de archivos están disponibles una vez finalizado el siguiente ciclo de actualización. Si hay una actualización en curso durante la carga del archivo, los datos no estarán disponibles hasta después de la siguiente actualización. Una vez completado el ciclo de actualización, puede ir a la `Data Preview` en la Data Warehouse para asegurarse de que el archivo se ha cargado correctamente y de que los datos se muestran según lo esperado.

## Ajuste {#wrapup}

En este tema se trataron únicamente los conceptos básicos para utilizar la importación de datos, pero puede que desee hacer algo más avanzado. Consulte los Artículos relacionados para obtener instrucciones sobre el formato y la importación de datos financieros, de comercio electrónico, de gasto en publicidad y de otro tipo.

Además, la carga de archivos no es la única manera de introducir sus datos en [!DNL Commerce Intelligence]. El [API de importación de datos](https://developer.adobe.com/commerce/services/reporting/import-api/) Las funciones de le permiten insertar datos arbitrarios en su [!DNL Commerce Intelligence] Data Warehouse.

## Relacionado {#related}

* [Formato e importación de datos financieros](../../../best-practices/format-import-financial-data.md)
* [Importación de datos de gasto en publicidad/sin conexión](../connecting-data/import-offline-ad-data.md)
* [Previsto[!DNL Google ECommerce] datos](../integrations/google-ecommerce-data.md)

## Recursos de terceros

* [Guía de formato de datos - Números](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs] Guía de formato de datos](https://support.google.com/docs/answer/56470?hl=en)
