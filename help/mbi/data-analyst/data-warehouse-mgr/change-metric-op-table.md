---
title: Cambiar la tabla operativa de una métrica
description: Obtenga información sobre cómo cambiar la tabla de datos que utiliza una métrica para realizar su operación.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# Cambiar la tabla operativa de una métrica

En algunos casos, puede decidir cambiar la tabla de datos que utiliza una métrica para realizar su operación. Por ejemplo, si tiene una nueva tabla de usuarios, desea migrar las métricas relacionadas con el usuario de la tabla &quot;Usuarios\_Antiguos&quot; para usar la tabla &quot;Usuarios\_Nuevo&quot; en su lugar.

1. Vaya a **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. Haga clic en **[!UICONTROL Edit]** junto a la métrica para la que desea cambiar el `operational` tabla.
1. En el editor, haga clic en **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. Ahora seleccione la nueva tabla en la que desea basar esta métrica.
1. A continuación, tendrá que hacer coincidir las dimensiones de datos existentes con las correspondientes de la nueva tabla. Por ejemplo, si tenía una columna llamada `User's registration date`, simplemente seleccione qué columna de la nueva tabla registra los mismos datos de fecha. (Consulte el paso siguiente si no tiene columnas coincidentes en la nueva tabla)

   ![](../../assets/change-metrics-2.png)

1. Si no tiene una columna coincidente en la nueva tabla, puede: **crearlo en la tabla de datos** o [póngase en contacto con el servicio de asistencia técnica](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) si se trata de una columna o dimensión de cálculo realizada por [!DNL MBI]), o simplemente **eliminar la dimensión de la métrica**. Para eliminar una dimensión que ya no necesite, simplemente vuelva al editor de la métrica y seleccione las dimensiones que desea eliminar en `Dimensions`.

   ![](../../assets/change-metrics-3.png)
