---
title: Usar grupos de paneles
description: Aprenda a permitir una mejor organización de los paneles.
exl-id: e48b7345-62d0-4898-997e-3c3c02040ad3
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/8YJRsYyWhmBvEE5JFjQChnRvKFwBVzvMk4TbRJVJ3RY
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 301
ht-degree: 0%

---

# Usar grupos de tableros

Los grupos de paneles permiten una mejor organización de los paneles. El caso de uso más común es agrupar paneles similares en el mismo &quot;grupo&quot;. Por ejemplo, todos los paneles relacionados con el marketing podrían agruparse en un grupo de paneles llamado &quot;Marketing&quot;.

En el menú desplegable de selección de tableros, los grupos de tableros se muestran en orden alfabético, con todos los tableros debajo de &quot;Sin grupo&quot; en último lugar. Los paneles bajo el mismo grupo se muestran juntos y en orden alfabético dentro de cada grupo.

## Uso compartido de grupos de paneles

Los grupos de paneles no se pueden compartir directamente entre los usuarios. Cuando se comparte un panel con los usuarios, el grupo de paneles en el que se encuentra se crea automáticamente para esos usuarios si no existe. Si existe el grupo de tableros, el tablero se anexará a la lista.

Cuando el propietario cambia el grupo de un panel, el cambio se refleja automáticamente en todos los usuarios con los que se ha compartido el panel. Los usuarios no pueden cambiar el grupo de paneles de paneles de los que no son propietarios.

## Crear grupos de tableros

Los grupos de paneles se pueden crear de una de las dos maneras siguientes:

1. Al crear un tablero:

   ![crear grupo de tableros](../../assets/create-dashboard-groups-new-dashboard.png)

1. Al cambiar el grupo de un tablero existente, desde la página `Manage Data > Dashboards`:

   1. Haga clic en el tablero para el que desea crear el grupo.

   1. En `Dashboard Group (optional)`, aparece el grupo de tableros actual.

   1. Para crear un grupo, escriba el nombre del nuevo grupo y haga clic fuera del cuadro.

      ![crear grupo de tableros](../../assets/create-dashboard-groups-existing-dashboard.png)

## Añadir tableros existentes a grupos existentes

1. En la página `Manage Data > Dashboards`, elija el tablero para el cual desea cambiar el grupo.

1. El texto bajo `Dashboard Group (optional)` muestra el grupo de tableros actual del tablero.

1. Para cambiar el grupo del tablero, elija otro grupo de la lista, en este caso `PS`, `Campaigns`.

   ![cambiar tablero de grupo](../../assets/add-existing-dashboard-existing-group.png)

## Eliminar grupos de tableros

Cuando un grupo de paneles no tiene paneles debajo, se elimina automáticamente.
