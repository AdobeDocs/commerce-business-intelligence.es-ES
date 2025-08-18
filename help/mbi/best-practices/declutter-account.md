---
title: Desorganización de su cuenta  [!DNL Commerce Intelligence] s
description: Aprenda a limpiar su cuenta de  [!DNL Commerce Intelligence] .
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# Limpiar su cuenta de [!DNL Adobe Commerce Intelligence]

Ya sea que haya estado con [!DNL Commerce Intelligence] durante seis meses o seis años, mantener una cuenta ordenada es primordial para que su organización pueda sacar el máximo partido a la plataforma. Con el tiempo, es natural que haya usuarios, paneles, informes, métricas y columnas que ya no sean necesarios. Tal vez creó un informe para un solo uso y se olvidó de él, o bien un usuario que abandonó su compañía nunca tuvo su cuenta desactivada.

Con [un nombre estandarizado y claro para todos los elementos](../best-practices/naming-elements.md)) de su cuenta de [!DNL Commerce Intelligence], los pasos de auditoría de cuentas a continuación le ayudan a reducir el desorden y los análisis innecesarios para sus usuarios. Un beneficio adicional incluye [ciclos de actualización potencialmente más rápidos](../best-practices/reduce-update-cycle-time.md).

## Paso 1: Identificar A Los Usuarios No Activos

El primer paso para limpiar su cuenta es desactivar las cuentas de los usuarios no activos, como las personas que han dejado la compañía o que ya no usan [!DNL Commerce Intelligence] en sus roles actuales.

Para ello, haga clic en el nombre de su empresa en la barra de navegación superior derecha y seleccione **[!UICONTROL Manage Users]**. A continuación, seleccione el usuario que desea desactivar y haga clic en **[!UICONTROL Deactivate User]**.

>[!NOTE]
>
>Necesita [permisos de administrador](../administrator/user-management/user-management.md) para hacerlo.

>[!WARNING]
>
>Al desactivar un usuario, se eliminan los gráficos, tableros y otros recursos creados por ese usuario. Si desea conservar estos recursos, póngase en contacto con el equipo de [!DNL Commerce Intelligence] [soporte técnico](../guide-overview.md#Submitting-a-Support-Ticket) antes de desactivar el usuario. La asistencia técnica puede ayudarle a transferir estos recursos a otro usuario.

### Reactivar un usuario

Para reactivar a un usuario, vuelva a invitarlo y vuelva a crear su cuenta con la misma dirección de correo electrónico que se desactivó. Además, su acceso y los datos que poseía se restauran al iniciar sesión.

## Paso 2: Eliminar paneles e informes no utilizados

El siguiente paso para auditar su cuenta es eliminar los tableros e informes que no se utilicen.

>[!NOTE]
>
>Necesita `Admin` o `Standard` [permisos de usuario](../administrator/user-management/user-management.md) para hacerlo.

Todos los usuarios con acceso de `Admin` o `Standard` pueden crear informes y paneles. Por ese motivo, todas las personas con estos permisos deben seguir los pasos a continuación para identificar y eliminar los informes no utilizados.

### Revisión de paneles e informes

Antes de eliminar algo, debe revisar los informes y los paneles para evaluar qué se está utilizando. Aunque puede usar la característica **[!UICONTROL find unused reports]** que se describe a continuación, cualquier revisión inicial hará que sus tareas de limpieza sean mucho más productivas.

### Eliminación de paneles e informes

Después de acceder a los paneles e informes, puede empezar a limpiar la cuenta.

**Para quitar un informe de un panel**

1. Busque el informe que desee quitar en el panel.
1. Seleccione **[!UICONTROL Options]** en la esquina superior derecha del informe.
1. Haga clic en **[!UICONTROL Remove From Dashboard]**.

**Para eliminar un panel completo**

1. Seleccione **[!UICONTROL Manage Data]** y luego **[!UICONTROL Dashboards**].
1. Haga clic en el tablero que desee eliminar.
1. Haga clic en **[!UICONTROL Delete Dashboard]**.

También puede seleccionar **[!UICONTROL Dashboard Options]** y luego **[!UICONTROL Delete]** en el propio tablero.

![](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>Al eliminar un tablero no se eliminan los informes que contiene, por lo que debe realizar un paso más para eliminar los informes.

**Para Eliminar Informes No Utilizados**

1. Seleccione **[!UICONTROL Manage Data]**, luego **[!UICONTROL Reports]**.
1. Marque la casilla **Mostrar solo los informes no utilizados** ubicada debajo de la lista de métricas. Esto crea una lista de informes que no se utilizan en un panel o resumen de correo electrónico.
1. Seleccione los informes que desee eliminar. Para seleccionar todos, haga clic en la casilla de verificación situada encima de la lista de informes.
1. Haga clic en **[!UICONTROL Delete Selected]**.

Aquí tiene un vistazo al proceso de eliminación de informes no utilizado:

![](../../mbi/assets/unused_reports.png)

## Paso 3: Eliminar Métricas No Utilizadas

Después de haber limpiado la lista de usuarios, los paneles y los informes, puede pasar a auditar la lista de métricas. Esto le ayuda a identificar cualquier elemento que pueda estar obsoleto (por ejemplo, se creó una nueva métrica con una definición diferente) o que no esté en uso.

1. Para generar una lista de informes dependientes para una métrica, vaya a **[!DNL Manage Data]** y seleccione Haga clic en **[!UICONTROL Metrics]**.
1. Haga clic en **[!UICONTROL Edit]** junto a una métrica.
1. En la parte inferior de la página, verá una sección llamada **[!UICONTROL Dependent Charts]**. Haga clic en el vínculo para generar una lista de informes dependientes para esta métrica.
1. Una vez que el sistema completa la comprobación, [!DNL Commerce Intelligence] muestra una lista de paneles, informes y usuarios que utilizan esta métrica.

![](../../mbi/assets/report_dependecies.png)

Si decide que la métrica ya no es necesaria, vuelva a la página **[!UICONTROL Metrics]** haciendo clic en **[!UICONTROL Back to Metric List]** para buscar la métrica que desea eliminar. Haga clic en **[!UICONTROL Delete]**.

## Paso 4: Evaluar las columnas sincronizadas

El último paso es evaluar las columnas que se están sincronizando en la Data Warehouse. La dessincronización de columnas no solo puede desorganizar la cuenta, sino que también puede reducir el tiempo de actualización.

Si desea continuar, póngase en contacto con el [!DNL Commerce Intelligence] [Soporte técnico](../guide-overview.md#Submitting-a-Support-Ticket). El equipo de asistencia puede crear un informe que incluya todas las columnas que no se utilicen en ningún tablero para ningún usuario y que no se utilicen en resúmenes de correo electrónico, excepto los informes SQL. A continuación, puede utilizar este informe como guía para seleccionar columnas para desincronizarlas mediante el Administrador de Data Warehouse.

>[!NOTE]
>
>Siempre puede volver a sincronizar estas columnas en el futuro. Al anular la sincronización de una columna, se eliminan los datos de su Data Warehouse; solo significa que esta columna no se comprueba para ver si hay valores nuevos o actualizados durante el ciclo de actualización.

**Para desincronizar una columna (o columnas)**

1. Vaya a **[!DNL Manage Data]** y después a **[!UICONTROL Data Warehouse]**.
1. En la lista **[!UICONTROL Synced Tables]**, vaya a la tabla que contiene la columna.
1. Marque una o más casillas junto a una o más columnas que desee desincronizar.
   >[!NOTE]
   >
   >No se puede anular la sincronización de una columna de clave principal sin soltar toda la tabla.

1. Haga clic en **[!UICONTROL Remove]** para anular la sincronización de una o varias columnas.

A continuación se muestra un vistazo a todo el proceso:

![](../../mbi/assets/drop_column.png)

## Ajuste

Tu cuenta de [!DNL Commerce Intelligence] debería ser más ordenada y fácil de navegar para ti y tu equipo.
