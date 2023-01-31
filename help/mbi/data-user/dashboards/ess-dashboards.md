---
title: Tableros
description: Aprenda a crear y trabajar con un tablero.
exl-id: a872344b-ac66-41eb-a471-5a69f8802527
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# Tableros

[!DNL MBI] Los tableros le ofrecen una vista rápida del rendimiento y la actividad de ventas de su tienda de un vistazo. Los tableros individuales se pueden compartir con otros usuarios y organizar en grupos lógicos. También puede establecer diferentes niveles de permisos para otros usuarios.

Es fácil crear un nuevo informe, agregarlo a un tablero y exportar los datos a Excel. Se puede cambiar el tamaño de los gráficos y los informes y arrastrarlos a su posición en el tablero.

![Panel](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## Creación de tableros {#createdash}

Los tableros son esencialmente compartibles, bloques temáticos para los análisis que crea en los Report Builder. Así puede animar a su equipo a colaborar y a mantener una única fuente de verdad en su organización.

*Si es administrador o usuario de Standard*, puede crear un tablero haciendo clic en el `Dashboard Options` lista desplegable y selección `Create New dashboard`.

Cómo se ven los tableros que crea depende totalmente de usted. Puede organizar y cambiar el tamaño de los elementos en el panel del modo que desee según sus necesidades y flujo de trabajo.

![organizar cambiar el tamaño del elemento del tablero](../../assets/arrange_resize_dashboard_element.gif)

### Crear un tablero nuevo

1. En el menú , haga clic en **[!UICONTROL Dashboards]**.

1. El nombre del tablero predeterminado aparece en la esquina superior izquierda del encabezado del tablero. Haga clic en la flecha hacia abajo (![](../../assets/magento-bi-btn-down.png)) para mostrar las opciones disponibles.

   ![Crear tablero](../../assets/magento-bi-dashboard-create.png)

1. Haga clic en **[!UICONTROL Create Dashboard]**. A continuación, haga lo siguiente:

   * Escriba un `Name` para su tablero.

   * Para crear un `Group` para el tablero, introduzca el nombre del grupo.

      Por ejemplo, si la instalación de Commerce tiene varias vistas de tienda, puede crear un Grupo para cada vista de tienda.

   * Haga clic en **[!UICONTROL Create]**.

   ![nombre del tablero](../../assets/magento-bi-dashboard-create-name.png)

   * El nombre del nuevo tablero aparece en la esquina superior izquierda. Haga clic en la flecha hacia abajo (![](../../assets/magento-bi-btn-down.png)) para mostrar las opciones. Si ha creado un grupo, el nuevo panel aparece debajo del grupo en la lista.


### Agregar un informe

1. Para agregar un informe, realice una de las siguientes acciones:

   * Haga clic en el **[!UICONTROL Add a report]** en la página.

   * En el encabezado del tablero, haga clic en **[!UICONTROL Add Report]**.

      ![Agregar informe](../../assets/magento-bi-dashboard-create-add-report.png)

1. Haga clic en **[!UICONTROL Create Report]** para mostrar la variable **[!UICONTROL Report Builder Options]**.

   ![Opciones del Report Builder](../../assets/magento-bi-report-builder.png)

## Organizar elementos en un tablero

* Para cambiar el tamaño de un gráfico o informe, arrastre la esquina inferior derecha al nuevo tamaño.

* Para mover un gráfico o informe, pase el ratón sobre el título o el encabezado hasta que el cursor cambie a una cruz. A continuación, arrástrela a su posición.

## Administración de tableros {#managedash}

En **[!DNL Manage Data** > **Dashboards]**, puede administrar los permisos de usuario para los tableros que posea, eliminar los que ya no necesite y establecer un tablero predeterminado.

### Uso compartido de los paneles {#sharingdash}

Para escalar realmente [!DNL MBI] en toda la organización y proporcione información valiosa, le recomendamos que comparta los paneles que cree con otros integrantes del equipo. *Puede compartir los tableros que le pertenecen* haciendo clic en el botón `Share Dashboard` en la parte superior de la página.

Al compartir un tablero, puede asignar permisos en su organización O de forma individual, lo que significa que puede decidir quién puede ver y editar los informes.

>[!NOTE]
>
>`Read-Only` los usuarios solo tienen acceso a tableros que se comparten directamente con ellos; no pueden buscar ni agregar tableros por su cuenta. ¡No te olvides de mantenerlos en el circuito!

### Acceso a tableros compartidos {#accessshared}

*Si es administrador o usuario de Standard* y desea agregar un tablero compartido a su cuenta, puede hacerlo haciendo clic en **[!UICONTROL Dashboard Options]** y, a continuación, haga clic en **[!UICONTROL Find]** en la lista desplegable .

![buscar panel](../../assets/find_dashboard.png)<!--{: width="1000" height="535"}-->

### Administrar la configuración del tablero

1. En el menú , haga clic en **[!DNL Manage Data** > **Dashboards]**.

1. Si procede, introduzca un nuevo `Dashboard Name`.

1. Para asignar el tablero a un `Dashboard Group`, elija entre la lista de grupos.

   **`Permissions`**

   Para proporcionar a todos los usuarios el mismo nivel de acceso al panel, haga lo siguiente:

   1. En **`Shared with`**, elija una de las siguientes opciones:

      * `View`
      * `Edit`
      * `None`
   1. Cuando se le pida que confirme la acción, haga clic en **[!UICONTROL OK]** para actualizar el nivel de permisos de cada usuario.

   1. Para cambiar el nivel de permiso de una persona, busque el usuario en la lista y cambie el nivel de permiso. El cambio se guarda automáticamente.

   **`Default`**

   1. Para que este tablero sea el predeterminado para su [!DNL MBI] cuenta, haga clic en **[!UICONTROL Make Default]**.

   **`Remove`**

   1. Para quitar el tablero, haga clic en **[!UICONTROL Delete Dashboard]**.
