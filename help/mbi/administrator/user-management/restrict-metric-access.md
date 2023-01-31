---
title: Restringir el acceso a las métricas
description: Obtenga información sobre cómo trabajar con métricas, acceso y restricciones.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Administrar usuarios de métricas

Además de establecer niveles de permisos de usuario, también puede restringir el acceso a las métricas de forma usuario por usuario. Por ejemplo, si desea que su departamento de contabilidad tenga acceso a métricas relacionadas con los ingresos pero no a métricas de adquisición de usuarios, puede restringir el acceso a esas métricas.

En casos como estos, se recomienda configurar la cuenta de ese usuario en **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** se deben conceder permisos a los usuarios que no necesiten crear o modificar métricas, columnas calculadas, integraciones o usuarios, pero que sí necesiten acceder a los datos de la Data Warehouse. Si desea restringir completamente el acceso a los datos, utilice la variable **[!UICONTROL Read Only]** permisos en su lugar.

Después de establecer el nivel de permiso, puede seleccionar las métricas en **[!UICONTROL Standard]** puede acceder a haciendo lo siguiente:

1. Vaya a **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. Seleccione la cuenta de usuario que desee.
1. La variable **[!UICONTROL Metrics]** mostrará una lista de las métricas disponibles. Compruebe las métricas a las que desea que el usuario tenga acceso; anule la selección de aquellos a los que el usuario no debería tener acceso.
1. [!DNL MBI] guarda los cambios automáticamente. Si el cambio se realiza correctamente, [!DNL MBI] display **[!UICONTROL Saved!]** en la parte superior de la página.

>[!NOTE]
>
>Todos los usuarios con **[!UICONTROL Standard]** Los permisos de pueden acceder a todos los datos del almacén de datos a través de la exportación de datos, además de a todas las métricas de [!DNL Google Analytics].

También puede restringir el acceso a una métrica editando la métrica y **[!UICONTROL Standard]** seleccionar usuarios en el **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** para obtener más información.

>[!NOTE]
>
>Si duplica una métrica, [!DNL MBI] copia los permisos de usuario establecidos en la métrica original.
