---
title: Uso compartido de paneles con otros usuarios
description: Obtenga información sobre cómo compartir tableros con otros usuarios.
exl-id: 6279b049-d1b2-4d40-b30b-ee8772e990f4
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Uso compartido de paneles con otros usuarios

Compartir paneles es una buena manera de mantener a su equipo en el bucle y fomentar el debate colaborativo. Al crear y compartir un tablero central, puede proporcionar a su equipo la información que necesita y, al mismo tiempo, mantener el control. [[!DNL Adobe] recomienda](../../best-practices/share-dashboard-best-practice.md){: target=&quot;_blank&quot;} que concede `Edit` derechos sobre algunos seleccionados para minimizar los cambios accidentales.

>[!NOTE]
>
>Si el tablero que está compartiendo contiene informes creados con métricas a las que un usuario específico no tiene acceso, los informes muestran un `Error Loading Data` Mensaje. Si desea que los datos aparezcan para el usuario específico, una [usuario administrador](../../administrator/user-management/user-management.md) debe conceder acceso a todas las métricas utilizadas en esos informes.

## Compartir un tablero

1. Clic **[!UICONTROL Share Dashboard]** en la parte superior de la pantalla.

   Una lista de todos los usuarios de su [!DNL Commerce Intelligence] se mostrará la cuenta.

1. Para seleccionar un usuario con el que compartir el panel, marque la casilla a la izquierda de su nombre.

   Para seleccionar o deseleccionar todos los usuarios, haga clic en **[!UICONTROL Select]** y seleccione `Everyone` o `None`, respectivamente.

1. Los permisos se pueden configurar usuario por usuario o en masa.

   *Para establecer permisos individuales*, haga clic en **[!UICONTROL None]** a la derecha del nombre del usuario. En este menú desplegable, seleccione el tipo de permisos que debe tener el usuario.

   *Para establecer permisos en masa*, haga clic en **[!UICONTROL Set Permissions]**. En este menú desplegable, seleccione el tipo de permisos que deben tener los usuarios seleccionados.

   >[!NOTE]
   >
   >También puede utilizar esta función para actualizar los permisos establecidos anteriormente. Por ejemplo, si desea dejar de compartir el tablero con alguien, establezca sus permisos en `None`.

1. Para compartir el tablero, haga clic en **[!UICONTROL Save Changes]**. Los usuarios seleccionados recibirán un correo electrónico que les invitará a ver el panel.

Ejemplo:

![compartir tablero](../../assets/Share_Dashboards.gif)
