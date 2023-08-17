---
title: Administrar tableros
description: Obtenga información sobre cómo administrar los permisos de usuario para los paneles que posee, eliminar los que ya no necesita y establecer un panel predeterminado.
exl-id: 32c21093-2a7d-4d8e-afc0-19bd702f9b36
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Administrar un tablero

>[!NOTE]
>
>Requiere [Permisos de administración](../../administrator/user-management/user-management.md).

Entrada **[!DNL Manage Data** > **Dashboards]**, puede administrar los permisos de usuario para los tableros que posee, eliminar los tableros que ya no necesita y establecer un tablero predeterminado. Este tema trata sobre:

1. [Cambiar nombre de paneles](#rename)

1. [Administración de permisos de tablero](#userperm)

1. [Modificación del tablero predeterminado](#default)

1. [Eliminación de paneles](#delete)

## Cambiar nombre de panel {#rename}

Para cambiar el nombre de un tablero:

1. Haga clic en el nombre del tablero que desee cambiar.

2. Introduzca el nuevo nombre en la `Dashboard Name` field.

## Administrar permisos de usuario {#userperm}

Existen tres niveles de acceso en [!DNL Commerce Intelligence] para paneles: `View`, `Edit`, y `None`.

* `View` permite a los usuarios seleccionados ver el tablero, pero no editarlo. Los usuarios también pueden cambiar el tamaño de los gráficos, exportar datos y copiar los gráficos en sus propios paneles mediante la función Guardar como si tuvieran permisos estándar o de administrador.

* `Edit` permite a los usuarios seleccionados editar y guardar gráficos en este panel si tienen permisos estándar o de administrador. Además, los usuarios con permisos de edición también pueden compartir tableros con otros usuarios.

* `None` significa que los usuarios seleccionados no pueden ver ni editar este panel.

Los permisos de usuario se pueden cambiar de una de las dos maneras siguientes: para todos los usuarios o para un usuario individual.

1. *Para cambiar los permisos de todos los usuarios,* utilice el menú desplegable situado junto a `Set all users' permissions to…` etiqueta.

1. *Para cambiar los permisos de un usuario individual,* utilice el menú desplegable situado junto al nombre del usuario para definir el nivel de acceso deseado.

## Cambio del tablero predeterminado {#default}

Para cambiar el tablero predeterminado de la cuenta:

1. Haga clic en el nombre del tablero que desee utilizar como predeterminado.

1. Haga clic **[!UICONTROL Make Default]**.

## Eliminar paneles {#delete}

Para eliminar un tablero:

1. Haga clic en el nombre del tablero que desee eliminar.

1. Haga clic **[!UICONTROL Delete Dashboard]**.
