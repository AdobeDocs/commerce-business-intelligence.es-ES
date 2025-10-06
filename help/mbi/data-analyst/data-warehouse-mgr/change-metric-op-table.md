---
title: Cambio de la tabla operativa de una métrica
description: Aprenda a cambiar la tabla de datos que utiliza una métrica para realizar su operación.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Cambio de la tabla operativa de una métrica

En determinados casos, puede decidir cambiar la tabla de datos que utiliza una métrica para realizar su operación. Por ejemplo, si tiene una nueva tabla de usuarios, desea migrar las métricas relacionadas con el usuario de la tabla `Users\_Old` para que en su lugar utilice la tabla `Users\_New`.

1. Ir a **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. Haga clic en **[!UICONTROL Edit]** al lado de la métrica para la cual desea cambiar la tabla `operational`.
1. En el editor, haga clic en **[!UICONTROL Change]**.

   ![Página de definición de métrica que muestra la configuración de tabla operativa](../../assets/change-metrics-1.png)
1. Seleccione la nueva tabla en la que desea basar esta métrica.
1. Hacer coincidir las dimensiones de datos existentes con las correspondientes de la nueva tabla. Por ejemplo, si tiene una columna llamada `User's registration date`, simplemente seleccione qué columna de la nueva tabla registra los mismos datos de fecha. (Consulte el paso siguiente si no tiene columnas coincidentes en la nueva tabla)

   ![Menú desplegable de selección de tabla que muestra las tablas disponibles](../../assets/change-metrics-2.png)

1. Si no tiene una columna coincidente en la nueva tabla, puede **crearla en la tabla de datos** o [ponerse en contacto con el soporte técnico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es) si es una columna de cálculo o dimensión creada por [!DNL Commerce Intelligence]. También puede **eliminar la dimensión de la métrica**. Para eliminar una dimensión que ya no necesite, simplemente vuelva al editor de la métrica y seleccione las dimensiones que desea eliminar en `Dimensions`.

   ![Menú desplegable de selección de columna operativa](../../assets/change-metrics-3.png)
