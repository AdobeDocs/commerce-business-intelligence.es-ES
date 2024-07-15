---
title: Clonar paneles
description: Obtenga información sobre cómo clonar tableros.
exl-id: f0bfa786-ab01-4c55-9d8a-ed002c2321b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Clonar un tablero

La clonación de un tablero permite copiar todos los informes de un tablero en un tablero nuevo.

Esto resulta útil si desea volver a crear un conjunto de gráficos existente pero cambiar la perspectiva (por ejemplo, diferentes vistas de datos, mercados, sitios web o tiendas). Después de duplicar el panel, puede editar cada uno de los nuevos gráficos para cambiar su métrica, vista de datos, filtro o agrupación.

1. Para clonar un tablero, haga clic en **[!UICONTROL Options]** en la parte superior de la pantalla.

1. En el menú desplegable , haga clic en **[!UICONTROL Save As]**.

1. Cuando se le solicite, escriba `New Dashboard Name`. Adobe recomienda nombres que le indiquen, de un vistazo, qué información contiene el panel.

   Por ejemplo, está clonando un tablero denominado `Customer Activity`. Este panel contenía información de la actividad del cliente para su ubicación de Filadelfia, pero ahora desea crear un panel para su nueva ubicación de la ciudad de Nueva York. Este tablero podría llamarse `New York City - Customer Activity`.

1. Utilice los campos `Chart Title Find` y `Chart Title Replace` para buscar todos los gráficos con `Philadelphia` en el título y reemplazarlos con `New York City`.

   Si no escribe ningún valor en estos campos, se agregará automáticamente un `(2)` al final de todos los títulos de gráficos en el nuevo tablero.

1. Haga clic en **[!UICONTROL Save]** para clonar el tablero.

Ejemplo:

![tablero de clonación](../../assets/datgif.gif)
