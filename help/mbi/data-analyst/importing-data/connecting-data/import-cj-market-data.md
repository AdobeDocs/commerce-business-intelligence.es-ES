---
title: Importación de datos de marketing de afiliados de CJ (unión de la Comisión)
description: Aprenda a importar los datos de Afiliados de CJ (unión de la Comisión) en [!DNL MBI].L MBI].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# Importar `CJ Affiliate` data

Para importar `CJ Affiliate` (unión de la Comisión) a [!DNL MBI], simplemente siga los pasos a continuación y adjunte el archivo resultante a un ticket de asistencia. Configuraremos la tabla de datos en su cuenta y le permitiremos seguir cargando datos de forma independiente.

## Exportar `CJ Affiliate` Datos

1. En `CJ Affiliate` , vaya a la `Reports` pestaña .

1. En el `Performance` , seleccione `Report Options`.

1. Establezca `Performance By` igual a `Program`, `Trend` igual a `Daily`y `Date Range` igual al intervalo de fechas que se va a auditar.

   ![export-cj-afiliados-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Select `Run Report`.

1. En el `File Format` menú desplegable, seleccione `CSV`.  Haga clic en **[!UICONTROL Download]**.

   ![exportar datos de afiliados de cj](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Una vez descargado el archivo, puede [cargar el archivo](../connecting-data/using-file-uploader.md) a su [!DNL MBI] almacén de datos.

   Esto crea una nueva tabla en el [!DNL MBI] almacén de datos en el que se pueden seguir cargando datos nuevos periódicamente. Al cargar el archivo, asegúrese de seguir los requisitos de formato enumerados en [Uso del cargador de archivos](../connecting-data/using-file-uploader.md).
