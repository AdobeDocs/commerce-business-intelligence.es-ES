---
title: Administrador de Datas Warehouse
description: Obtenga información sobre cómo administrar la configuración de sincronización de columnas y tablas, explorar en profundidad el esquema de una tabla y crear columnas calculadas para utilizarlas en los informes.
exl-id: b9577919-0db0-47f1-a426-1abe48443ac0
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 0%

---

# Administrador de Datas Warehouse

>[!NOTE]
>
>Requiere [permisos de administrador](../../administrator/user-management/user-management.md)

El Administrador de Datas Warehouse, al que se tiene acceso haciendo clic en **[!UICONTROL Manage Data > Data Warehouse]**, es el portal de la Data Warehouse [!DNL Adobe Commerce Intelligence]. Con el Administrador de Datas Warehouse, puede administrar la configuración de sincronización de columnas y tablas, explorar en profundidad el esquema de una tabla y crear columnas calculadas para utilizarlas en los informes.

Este tema trata sobre:

* [Aprender a dar la vuelta](#learning)
* [Sincronización de tablas y columnas](#syncing)
* [Creación de columnas calculadas](#calculated)
* [Borrado de tablas y eliminación de columnas](#delete)
* [Sincronización de nuevas tablas en segundo plano](#syncnew)
* [Entonces, ¿cuándo puedo usar mis nuevas columnas?](#when)

## Aprender a dar la vuelta {#learning}

La parte izquierda de la página `Data Warehouse Manager` contiene la lista de tablas, lo que le permite alternar fácilmente entre tablas. Al seleccionar una tabla de la lista, el área de administración de tablas se rellena con el esquema de la tabla, donde puede modificar la tabla seleccionada.

En la lista de la tabla, las tablas se agrupan por su origen de conexión. Estos orígenes se agregan en [!UICONTROL Manage Data > Integrations] y pueden ser una base de datos, una [API](https://developer.adobe.com/commerce/services/reporting/) o un conector de terceros. En la parte superior de la lista de la tabla, hay un cuadro de búsqueda que le permite encontrar fácilmente las tablas deseadas.

Debajo del cuadro de búsqueda, verá dos opciones: `All Tables` y `Synced Tables`. La opción `All Tables` enumera todas las tablas que ha puesto a disposición de la Data Warehouse, lo que incluye tanto las tablas sincronizadas como las no sincronizadas.

La opción `Synced Tables` muestra todas las tablas que ya se han agregado a la Data Warehouse y que tienen datos que se replican desde las columnas seleccionadas.

¿No ve la tabla que está buscando en la lista `All Tables`? Esto puede deberse a varios motivos:

* La fuente de datos aún no se ha agregado
* El origen de datos es una base de datos y el usuario [!DNL Commerce Intelligence] que ha creado no tiene acceso. En este caso, usted o el administrador de la base de datos deben conceder acceso.
* La fuente de datos o tabla se ha agregado recientemente y aún no se ha sincronizado

## Sincronización de tablas y columnas {#syncing}

### Sincronización de nuevas tablas y columnas nativas

El Administrador de Datas Warehouse no solo le permite ver y administrar fácilmente sus fuentes de datos, sino que también tiene la libertad de seleccionar las tablas y columnas individuales que desee sincronizar.

1. Haga clic en la opción `All Tables` y busque la tabla que desee sincronizar.
1. Haga clic en el nombre de la tabla para previsualizar el esquema. Si la tabla es nueva, todas las columnas se mostrarán como `Unsynced`.
1. Compruebe las columnas que desea sincronizar.

   >[!NOTE]
   >
   >Las columnas nativas de una tabla tienen From Your Database en la columna `Location`.

1. Asegúrese de comprobar las columnas `Primary Key`; estas columnas tienen un símbolo de clave junto al nombre de la columna. Se requiere un `Primary Key` para sincronizar correctamente los datos en la Data Warehouse.

   Si está sincronizando una tabla que proviene directamente de la base de datos, es posible que no se indique `Primary Keys`. En este caso, póngase en contacto con el administrador de la base de datos para solicitar que se agregue una o varias claves principales a la tabla.
1. Cuando termine, haga clic en el botón ![button](../../assets/button.png).

¡Un *Correcto!Se muestra el mensaje* y el estado cambia a `Pending` para las columnas seleccionadas. Una vez que se complete la siguiente actualización completa, las tablas y columnas recién sincronizadas estarán disponibles para usarlas en los informes. También puede establecer nuevos [métodos de replicación](./cfg-replication-methods.md) después de la sincronización inicial.

A continuación se muestra un breve vistazo a todo el proceso:

![Agregando columnas al almacén de datos](../../assets/DW_sync.gif)

### Sincronización de nuevas tablas en segundo plano {#syncnew}

Cuando puede sincronizar una tabla grande por primera vez, la Data Warehouse debe capturar de forma retroactiva todos los puntos de datos de la tabla antes de capturar nuevos datos de forma continua. Si la tabla es grande, es posible que no desee que la sincronización inicial se ejecute en secuencia con el **ciclo de actualización**. En este caso, desea que la sincronización inicial se produzca en segundo plano, en *paralelo* con cualquier actualización en ejecución.

Para asegurarse de que esto ocurra, debe seleccionar la opción `Save and Sync Data Immediately` que sincroniza esa tabla por primera vez.

### Comprobación de nuevas tablas y columnas {#forceupdate}

La Data Warehouse no detecta automáticamente nuevas fuentes, tablas o columnas en el momento en que se agregan. Un proceso de sincronización se ejecuta durante la semana para buscar nuevas adiciones y ponerlas a disposición, pero puede forzar una sincronización de estructura si desea acceder a las tablas y columnas agregadas recientemente antes de que se ejecute el proceso.

Debajo de la barra de búsqueda en la lista de la tabla hay un vínculo `Check for new tables and columns`. Al hacer clic en este vínculo, se fuerza el inicio del proceso de sincronización de estructura; las nuevas incorporaciones suelen estar disponibles después de 10 minutos. Actualice la página para ver el nuevo origen, tabla o columna.

## Creación de columnas calculadas {#calculated}

El simple hecho de poder ver y administrar datos de todas sus fuentes facilita en gran medida la obtención de información sobre su negocio. Sin embargo, dentro del Administrador de Datas Warehouse, puede ir un paso más allá al crear columnas calculadas dentro de las tablas. Las columnas de `Calculated` derivan información nueva de los datos existentes.

Supongamos que desea agregar `user's lifetime revenue` a su tabla `users` para encontrar usuarios de alto valor. O bien, si desea segmentar los ingresos por sexo, puede agregar `customer's gender` a la tabla `orders`.

Para obtener más información, consulte este [tutorial](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

## Borrado de tablas y eliminación de columnas {#delete}

Del mismo modo que puede seleccionar tablas y columnas para sincronizarlas con la Data Warehouse, también puede soltarlas o eliminarlas.

>[!NOTE]
>
>Al soltar una tabla o eliminar columnas, se eliminan los informes, las métricas, los conjuntos de filtros y las columnas dependientes una vez que se confirma la eliminación. Asegúrese de que desea hacer esto: **esta acción no se puede deshacer.**

No se preocupe si hace clic en **[!UICONTROL Delete]** por accidente. Se ejecuta una comprobación de dependencias antes de que se elimine algo, por lo que tiene la oportunidad de revisarlo todo antes de confirmarlo.

Para quitar columnas, haga clic en la tabla a la que pertenece la columna. Compruebe las columnas que desea quitar y haga clic en el botón ![button\_1.png](../../assets/button_1.png).

Para quitar una tabla sincronizada, seleccione todas las columnas de la tabla y vuelva a hacer clic en el botón ![button](../../assets/button_1.png). Esto elimina de la Data Warehouse todas las columnas nativas y calculadas que utilizan esta tabla.

### Confirmación de cambios

Tanto si va a borrar una tabla como si va a quitar columnas, se ejecuta una comprobación de dependencias antes de que finalice el proceso de eliminación. Las dependencias son columnas calculadas, métricas, conjuntos de filtros e informes que utilizan la tabla o columnas que se están eliminando. Se muestran todas las dependencias detectadas: en este momento, puede cancelar el proceso o hacer clic en **[!UICONTROL Confirm Changes]** para soltar la tabla o quitar las columnas.

Aunque las dependencias eliminadas no se pueden restaurar, las tablas y columnas seguirán estando disponibles si necesita volver a sincronizar cualquier columna nativa en el futuro.

A continuación se muestra un vistazo rápido para eliminar una columna:

![Quitando una columna del almacén de datos](../../assets/DW_delete.gif)

## Entonces, ¿cuándo puedo usar mis nuevas columnas? {#when}

Las nuevas columnas sincronizadas y las columnas calculadas nuevas o actualizadas estarán listas para su uso una vez que se complete la siguiente actualización completa. Si una actualización aún no está en curso, puede forzarla si hace clic en **[!UICONTROL Force update]**, que se muestra en la parte superior de la página `Data Warehouse` o `Integrations`. También puede programar una notificación por correo electrónico al finalizar la actualización haciendo clic en **[!UICONTROL Email me when complete]**.

Cuando esté listo para usar las nuevas columnas en los informes, [primero debe agregarlas a las métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md). Aunque los datos no están disponibles hasta que se complete una actualización, aún puede utilizar columnas nuevas en los informes. Los datos del informe se muestran cuando finaliza la actualización.

## Ajuste

Este artículo abarcaba mucho material. Por ahora, debería tener una comprensión sólida de lo que es una base de datos, cómo se organizan los datos, cómo se relacionan las tablas entre sí y qué puede hacer con el Administrador de Datas Warehouse.

Pruebe sus conocimientos [creando una columna calculada](../data-warehouse-mgr/creating-calculated-columns.md) o [creando algunos informes interesantes](../../tutorials/using-visual-report-builder.md).
