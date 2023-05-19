---
title: Cambio de la tabla operativa de una métrica
description: Aprenda a cambiar la tabla de datos que utiliza una métrica para realizar su operación.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Cambio de la tabla operativa de una métrica

En determinados casos, puede decidir cambiar la tabla de datos que utiliza una métrica para realizar su operación. Por ejemplo, si tiene una nueva tabla de usuarios, quiere migrar las métricas relacionadas con el usuario desde el  `Users\_Old` tabla para utilizar el `Users\_New` en su lugar.

1. Ir a **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. Clic **[!UICONTROL Edit]** junto a la métrica para la que desea cambiar el `operational` tabla.
1. En el editor, haga clic en **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. Seleccione la nueva tabla en la que desea basar esta métrica.
1. Hacer coincidir las dimensiones de datos existentes con las correspondientes de la nueva tabla. Por ejemplo, si tuviera una columna llamada `User's registration date`, simplemente seleccione qué columna de la nueva tabla registra los mismos datos de fecha. (Consulte el paso siguiente si no tiene columnas coincidentes en la nueva tabla)

   ![](../../assets/change-metrics-2.png)

1. Si no tiene una columna coincidente en la nueva tabla, puede **créela en la tabla de datos** o [soporte de contacto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) si es una columna de cálculo o dimensión realizada por [!DNL Commerce Intelligence]. También puede **eliminar la dimensión de la métrica**. Para eliminar una dimensión que ya no necesite, simplemente vuelva al editor de la métrica y seleccione las dimensiones bajo las que desea eliminar `Dimensions`.

   ![](../../assets/change-metrics-3.png)
