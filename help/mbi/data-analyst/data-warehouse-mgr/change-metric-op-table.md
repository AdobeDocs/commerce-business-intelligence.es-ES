---
title: Cambio de la tabla operativa de una métrica
description: Aprenda a cambiar la tabla de datos que utiliza una métrica para realizar su operación.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/9yJ1Zc2NLDvXYO16UvDkeWE0hD1jx0-Ne3AyFFHX5ns
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 231
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

1. Si no tiene una columna coincidente en la nueva tabla, puede **crearla en la tabla de datos** o [ponerse en contacto con el soporte técnico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) si es una columna de cálculo o dimensión creada por [!DNL Commerce Intelligence]. También puede **eliminar la dimensión de la métrica**. Para eliminar una dimensión que ya no necesite, simplemente vuelva al editor de la métrica y seleccione las dimensiones que desea eliminar en `Dimensions`.

   ![Menú desplegable de selección de columna operativa](../../assets/change-metrics-3.png)
