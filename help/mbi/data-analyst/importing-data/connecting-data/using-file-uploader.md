---
title: Uso de la carga de archivos
description: Aprenda a colocar todos los datos en un único almacén de datos.
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1392'
ht-degree: 0%

---

# Uso de la carga de archivos

>[!NOTE]
>
>Requiere [Permisos de administrador](../../../administrator/user-management/user-management.md).

[!DNL MBI] es potente no solo por sus características de visualización, sino porque le permite colocar todos los datos en un único almacén de datos. Incluso los datos que residen fuera de las bases de datos y las integraciones pueden introducirse en [!DNL MBI] mediante la herramienta Carga de archivos en el Administrador de Datas Warehouse.

Usemos campañas publicitarias como ejemplo. Si está ejecutando campañas en línea y sin conexión, no puede obtener una imagen completa si solo está analizando datos de una integración en línea. La carga de una hoja de cálculo con los datos de campaña sin conexión le permite analizar ambos conjuntos de datos y comprender mejor el rendimiento de la campaña.

## Restricciones y requisitos {#require}

1. **El único formato admitido para las cargas de archivos es `CSV` o`comma separated values`**. Si está trabajando en Excel, puede utilizar la función Guardar como para guardar el archivo en `.csv` formato.
1. **`CSV`los archivos deben utilizar`UTF-8 encoding`**. La mayoría de las veces, esto no será un problema. Si se produce este error al cargar un archivo, [consulte este artículo de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolving-utf-8-errors-for-csv-file-uploads.html?lang=en).
1. **Los archivos no pueden superar los 100 MB**. Si el archivo es más grande que esto, separe la tabla en fragmentos y guárdela como archivos individuales. Puede utilizar anexar los datos después de cargar el archivo inicial.
1. **Todas las tablas deben tener un`primary key`**. Debe haber al menos una columna en la tabla que pueda utilizarse como `primary key`o un identificador único para cada fila de la tabla. Cualquier columna designada como `primary key` can *never* sea nulo. A `primary key` puede ser tan sencillo como agregar una columna que da un número a cada fila, o puede ser de dos columnas concatenadas para crear una columna de valores únicos (por ejemplo, `campaign name` y `date`).

   Si una columna (o columnas) se designan como únicas pero hay duplicados, las filas duplicadas no se importarán.

## Formato de datos para la carga {#formatting}

Antes de cargar los datos en [!DNL MBI], compruebe que tiene formato según las directrices de esta sección.

### Fila de encabezado {#header}

Para asegurarse de que las columnas están etiquetadas y se importan correctamente, asegúrese de que la primera fila de la hoja de cálculo sea un encabezado que describa los datos de cada columna.

Los nombres de columna deben ser únicos y contener solo letras, números, espacios y estos símbolos: `$ % # /`. Si el nombre de una columna contiene una coma, se dividirá en dos columnas al cargar el archivo. Además, recomendamos que haya menos de 85 columnas en el archivo para optimizar la velocidad de actualización.

### Datos con comas {#commas}

Porque los archivos deben estar en `CSV` , el uso de comas puede causar problemas al cargar datos. `CSV` Los archivos utilizan comas para indicar nuevos valores, por lo que una columna con un nombre como `Campaigns`, `August` se leerá como dos columnas (`Campaigns` y `August`) en lugar de uno, desplazando todos los datos sobre una fila. Se recomienda evitar comas siempre que sea posible. Puede usar `Data Preview` para ver si los datos se muestran correctamente una vez completada la actualización.

### Fechas

Cualquier conjunto de datos que incluya fechas debe usar la variable [formato de fecha estándar](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` o `MM/DD/YYYY`.

### Caracteres especiales

Algunos caracteres especiales no se aceptan. Por ejemplo, el símbolo de barra vertical `& # 1 2 4` se interpreta como la creación de una columna nueva y provocará errores al cargar un archivo.

### Números decimales

Los valores monetarios deben tener el tipo de datos `Decimal Number` y estas columnas se redondearán automáticamente a dos decimales en el almacén de datos. Si no desea redondear los números decimales o tiene un grado de precisión bueno que esto, debe seleccionar la variable `Non-Currency Decimal Number` tipo de datos.

### Porcentajes

Los porcentajes deben introducirse como decimales. Por ejemplo:

| **Derecha:** | **Error:** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style=&quot;table-layout:auto&quot;}

### Valores con ceros a la izquierda o a la derecha {#zeroes}

Algunos valores del archivo (como códigos postales e ID) pueden comenzar o terminar con ceros. Para asegurarse de que los ceros se conservan y se cargan correctamente, puede cambiar el tipo de formato (por ejemplo, [de número a texto](https://support.office.com/en-US/article/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4)) o aplicar formato de número.

Déjenos usar `US ZIP codes` como ejemplo de cómo cambiar el formato de los números. En [!DNL Excel], resalte la columna que contiene `ZIP codes` y [cambiar el formato de número](https://support.office.com/en-za/article/Display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d) a `ZIP code`. También puede seleccionar un formato de número personalizado y `Type` ventana, introduzca `00000`. Tenga en cuenta que este método puede presentar problemas si algunos códigos tienen el formato `00000` y otros `00000-0000`.

La variable `Type` can [con un formato diferente para adaptarse a otros tipos de datos](https://support.office.com/en-us/article/Keep-leading-zeros-in-number-codes-1bf7b935-36e1-4985-842f-5dfa51f85fe7?CorrelationId=e1d4c2d3-cd5d-4a14-999d-437800274a90&amp;ui=en-US&amp;rs=en-US&amp;ad=US), como los ID. Si una `ID` tiene una longitud de nueve dígitos, por ejemplo, la variable `Type` podría `000000000` o `000-000-000`. Esto cambiaría `123456` a `000-123-456`.

Para [!DNL Google Docs] y [!DNL Apple Numbers] recursos, consulte [Relacionado](#related) en la parte inferior de esta página.

## Carga de datos {#uploading}

Ahora la hoja de cálculo tiene el formato correcto y [!DNL MBI]fácil de usar, permítanos agregarlo a su almacén de datos.

1. Para empezar, vaya a **[!UICONTROL Data** > **File Uploads]**.

1. Haga clic en el **[!UICONTROL Upload to New Table]** pestaña .

1. Haga clic en **[!UICONTROL Choose File]** y seleccione el archivo . Haga clic en **[!UICONTROL Open]** para iniciar la carga.

   Una vez finalizada la carga, verá una lista de las columnas [!DNL MBI] encontrado en su archivo .

1. Compruebe que los nombres de columna y los tipos de datos sean correctos. Concretamente, compruebe que las columnas de fecha se lean como fechas y no como números.

   >[!NOTE]
   >
   >La variable `datatype` es extremadamente importante, por lo que no omita este paso.

1. Seleccione la columna (o columnas) que formará la variable `primary key` para la tabla mediante las casillas de verificación situadas debajo del icono de clave.

1. Asigne un nombre a la tabla.

1. Haga clic en **[!UICONTROL Save Table]**.

A *¡Correcto!* aparece en la parte superior de la pantalla después de guardar la tabla.

Si necesita una imagen, aquí tiene un vistazo a todo el proceso:

![](../../../assets/fileupload.gif)

Las tablas cargadas se muestran en la sección **Cargas de archivos** de la lista de la tabla (en las opciones Todas las tablas y Tablas sincronizadas ) del Administrador de Datas Warehouse:

![](../../../assets/upload-tables.png)

## Actualización o adición de datos a una tabla existente {#appending}

¿Tiene datos nuevos para agregarlos a un archivo que ya ha cargado? Sin problema: puede actualizar y anexar datos fácilmente en [!DNL MBI].

1. Para empezar, vaya a **[!UICONTROL Manage Data** > **File Uploads]**.

1. Haga clic en el **[!UICONTROL Edit/Upload `.csv`a tablas existentes]** pestaña .

1. En la lista desplegable, haga clic en el nombre de la tabla que desee actualizar o anexar.

1. Utilice la lista desplegable para seleccionar la opción para administrar las filas duplicadas:

   |  |  |
   |---|---|
   | `Overwrite old row with new row` | Esto sobrescribirá los datos existentes con nuevos datos si una fila tiene la misma clave principal tanto en la tabla existente como en el nuevo archivo. Este es el método que se utiliza para las columnas con valores que cambian con el tiempo (por ejemplo, una columna Estado ). Los datos existentes se sobrescribirán y se actualizarán con los nuevos datos. Las filas con claves principales que no estén en la tabla existente se agregarán como filas nuevas. |
   | `Retain old row; discard new row` | Esto hará que se ignoren los nuevos datos si una fila tiene la misma clave principal tanto en la tabla existente como en el nuevo archivo. |
   | `Purge all existing rows first and ignore duplicate keys within the file` | Esto eliminará los datos existentes y los sustituirá por los nuevos datos del archivo. Solo debe utilizar esta opción si no necesita ninguno de los datos de la tabla existente. |

1. Haga clic en **[!UICONTROL Choose File]** y seleccione el archivo .

1. Haga clic en **[!UICONTROL Open]** para iniciar la carga.

   Una vez finalizada la carga, [!DNL MBI] validará la estructura de datos del archivo . A *¡Correcto!* aparece en la parte superior de la pantalla después de guardar la tabla.

## Disponibilidad de datos {#availability}

Al igual que las columnas calculadas, los datos de las cargas de archivos están disponibles una vez finalizado el siguiente ciclo de actualización. Si se estaba realizando una actualización durante la carga del archivo, los datos no estarán disponibles hasta después de la siguiente actualización. Una vez completado el ciclo de actualización, puede navegar hasta el `Data Preview` en el almacén de datos para asegurarse de que el archivo cargado correctamente y los datos se muestran según lo esperado.

## Ajuste {#wrapup}

Este artículo abarcaba solamente los conceptos básicos para usar la importación de datos, pero estamos apostando a que desee hacer algo un poco más avanzado. Consulte los artículos relacionados para obtener instrucciones sobre formatear e importar datos financieros, de comercio electrónico, de gasto publicitario y de otro tipo.

Además, la carga de archivos no es la única forma de introducir los datos en [!DNL MBI]. La variable [API de importación de datos](https://developer.adobe.com/commerce/services/reporting/import-api/) permite insertar datos arbitrarios en el [!DNL MBI] almacén de datos.

## Relacionado {#related}

* [Formato e importación de datos financieros](../../../best-practices/format-import-financial-data.md)
* [Importación de datos sin conexión/de otros gastos de publicidad](../connecting-data/import-offline-ad-data.md)
* [Esperado[!DNL Google ECommerce] data](../integrations/google-ecommerce-data.md)

## Recursos de terceros

* [Guía de formato de datos de números](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs] Guía de formato de datos](https://support.google.com/docs/answer/56470?hl=en)
