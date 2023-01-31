---
title: Declución de [!DNL MBI] Cuenta
description: Aprenda a limpiar su [!DNL MBI] cuenta.
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---

# Limpia tu [!DNL MBI] Cuenta

Si ha estado con [!DNL MBI] durante 6 meses o 6 años, mantener una cuenta ordenada es fundamental para que su organización aproveche al máximo la plataforma. Con el tiempo, es natural que haya usuarios, tableros, informes, métricas y columnas que ya no sean necesarios. Tal vez haya creado un informe para usarlo de una sola vez y se haya olvidado de él, o que un usuario que abandonó su empresa nunca haya desactivado su cuenta.

Junto con [nomenclatura estandarizada y clara para todos los elementos](../best-practices/naming-elements.md)) de su [!DNL MBI] , los pasos de auditoría de cuentas que se indican a continuación le ayudarán a reducir el desorden y los análisis innecesarios para sus usuarios. Una prestación adicional incluye [ciclos de actualización potencialmente más rápidos](../best-practices/reduce-update-cycle-time.md).

## Paso 1: Identificación de los usuarios no activos

El primer paso para limpiar la cuenta es desactivar las cuentas de los usuarios no activos, como aquellos que han abandonado la empresa o que ya no utilizan [!DNL MBI] en sus funciones actuales.

Para ello, haga clic en el nombre de su empresa en la esquina superior derecha de la barra de navegación superior y, a continuación, seleccione **[!UICONTROL Manage Users]**. A continuación, seleccione el usuario que desea desactivar y haga clic en **[!UICONTROL Deactivate User]**.

>[!NOTE]
>
>Necesita [Permisos de administrador](../administrator/user-management/user-management.md) para hacer esto.

>[!WARNING]
>
>Al desactivar un usuario también se eliminarán los gráficos, tableros y otros recursos creados por ese usuario. Si desea conservar estos recursos, póngase en contacto con el [!DNL MBI] [support](../guide-overview.md) antes de desactivar el usuario. La asistencia técnica puede ayudarle a transferir estos recursos a otro usuario.

### Reactivar un usuario

Para reactivar un usuario, vuelva a invitarlo recreando su cuenta con la misma dirección de correo electrónico que se desactivó, y su acceso y los datos que posee se restaurarán tras el inicio de sesión.

## Paso 2: Eliminar tableros e informes no utilizados

El siguiente paso para auditar su cuenta es eliminar los tableros e informes que no se utilicen.

>[!NOTE]
>
>Necesita `Admin` o `Standard` [permisos de usuario](../administrator/user-management/user-management.md) para hacer esto.

Cada usuario con `Admin` o `Standard` access puede crear informes y tableros. Por ese motivo, todas las personas con estos permisos deben seguir los pasos a continuación para identificar y eliminar los informes no utilizados.

### Revisar tableros e informes

Antes de eliminar cualquier elemento, debe revisar los informes y tableros para evaluar qué está usando actualmente. Mientras que puede usar la variable **[!UICONTROL find unused reports]** descrita a continuación, cualquier revisión inicial hará que sus esfuerzos de limpieza sean mucho más productivos.

### Eliminación de tableros e informes

Después de acceder a los tableros y a los informes, puede empezar a limpiar la cuenta.

**Eliminación de un informe de un tablero**

1. Busque el informe que desee eliminar en el tablero.
1. Select **[!UICONTROL Options]** en la esquina superior derecha del informe.
1. Haga clic en **[!UICONTROL Remove From Dashboard]**.

**Para eliminar un tablero completo**

1. Select **[!UICONTROL Manage Data]** y, a continuación, **[!UICONTROL Dashboards**].
1. Haga clic en el tablero que desee eliminar.
1. Haga clic en **[!UICONTROL Delete Dashboard]**.

También puede seleccionar **[!UICONTROL Dashboard Options]**, luego **[!UICONTROL Delete]** del propio panel.

![](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>Al eliminar un tablero, no se eliminan los informes que contiene, por lo que tendrá que dar un paso más para eliminar los informes.

**Para eliminar informes no utilizados**

1. Select **[!UICONTROL Manage Data]**, luego **[!UICONTROL Reports]**.
1. Marque la **Mostrar solo los informes no utilizados** situado debajo de la lista de métricas. Esto creará una lista de informes que no se usan en un tablero o un resumen por correo electrónico.
1. Seleccione los informes que desee eliminar. Para seleccionar todo, haga clic en la casilla de verificación situada encima de la lista del informe.
1. Haga clic en **[!UICONTROL Delete Selected]**.

A continuación se muestra un vistazo al proceso de eliminación de informes no utilizado:

![](../../mbi/assets/unused_reports.png)

## Paso 3: Eliminar métricas no utilizadas

Después de haber limpiado la lista de usuarios, los tableros y los informes, puede pasar a la auditoría de su lista de métricas. Esto le ayudará a identificar cualquier elemento que podría estar obsoleto (por ejemplo, si se creó una nueva métrica con una definición diferente) o que no esté en uso.

1. Para generar una lista de informes dependientes de una métrica, vaya a **[!DNL Manage Data]** y, a continuación, seleccione Haga clic en **[!UICONTROL Metrics]**.
1. Haga clic en **[!UICONTROL Edit]** junto a una métrica.
1. En la parte inferior de la página, verá una sección llamada **[!UICONTROL Dependent Charts]**. Haga clic en el vínculo para generar una lista de informes dependientes para esta métrica.
1. Una vez que el sistema haya completado la comprobación, [!DNL MBI] muestra una lista de tableros, informes y usuarios que utilizan esta métrica.

![](../../mbi/assets/report_dependecies.png)

Si decide que la métrica ya no es necesaria, vuelva a la página **[!UICONTROL Metrics]** página haciendo clic en **[!UICONTROL Back to Metric List]** en la parte superior de la página y busque la métrica que desee eliminar. Haga clic en **[!UICONTROL Delete]**.

## Paso 4: Evaluar las columnas sincronizadas

El último paso es evaluar las columnas que se sincronizan actualmente en el almacén de datos. La dessincronización de columnas no solo puede ralentizar la cuenta, sino que también puede reducir el tiempo de actualización.

Si desea continuar con esto, póngase en contacto con [!DNL MBI] [Asistencia](../guide-overview.md). El equipo de asistencia puede crear un informe que incluya todas las columnas que no se estén utilizando en ningún tablero para ningún usuario y que no se usen en los resúmenes de correo electrónico, excepto los informes SQL. A continuación, puede utilizar este informe como guía para seleccionar columnas para dessincronizarlas mediante el Administrador de Datas Warehouse.

>[!NOTE]
>
>Siempre puede empezar a sincronizar estas columnas de nuevo en el futuro. Al anular la sincronización de una columna, no se eliminará ningún dato del almacén de datos; solo significa que esta columna no se comprobará si hay valores nuevos o actualizados durante el ciclo de actualización.

**Para dessincronizar una columna (o columnas)**

1. Vaya a **[!DNL Manage Data]**, luego **[!UICONTROL Data Warehouse]**.
1. En el **[!UICONTROL Synced Tables]** , vaya a la tabla que contiene la columna .
1. Marque las casillas que aparecen junto a las columnas que desea dessincronizar.
   >[!NOTE]
   >
   >No puede dessincronizar una columna Clave principal sin soltar toda la tabla.

1. Haga clic en **[!UICONTROL Remove]** para dessincronizar las columnas.

A continuación se muestra un vistazo a todo el proceso:

![](../../mbi/assets/drop_column.png)

## Ajuste

¡Eso es! Su [!DNL MBI] ahora debe ser más ordenada y fácil de navegar por usted y su equipo.
