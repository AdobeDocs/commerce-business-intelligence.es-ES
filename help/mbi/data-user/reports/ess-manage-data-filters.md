---
title: Creación de conjuntos de filtros para métricas
description: Obtenga información sobre cómo crear conjuntos de filtros guardados y aplicarlos a las métricas.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/Y3SA-ypB62c0mwZ6uqAOQUyrISc5Tu8yqClrGwXspoU
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 277
ht-degree: 0%

---

# Creación de conjuntos de filtros

Si tiene varias métricas en [!DNL Commerce Intelligence] que necesitan filtrarse de manera similar (por ejemplo, filtrar los pedidos de prueba), puede crear conjuntos de filtros guardados y aplicarlos a las métricas. Esto le ahorra tiempo, ya que no tiene que añadir filtros individuales al crear o editar una métrica.

Consulte el [vídeo de formación](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html) para obtener más información.

>[!NOTE]
>
>Requiere [permisos de administrador](../../administrator/user-management/user-management.md).

1. Haga clic en **[!DNL Manage Data** > **Filter Sets]** en la barra lateral.

   ![Crear interfaz de conjuntos de filtros con la opción Agregar conjunto de filtros](../../assets/create-filter-sets.png)

1. Haga clic en **[!UICONTROL Add Filter Set]** en la parte superior de la página.

1. Seleccione la tabla que contiene las métricas que desea filtrar.

   Por ejemplo, si desea filtrar la métrica `Total number of orders` y está creada en la tabla `orders`, seleccione esa tabla.

1. Asigne un nombre a `Filter Set`.

1. Añada todos los filtros relevantes.

   Por ejemplo, si solo desea incluir pedidos con un estado de completado en la métrica `Total number of orders`, aplicaría un filtro que excluye todos los pedidos que no tienen un estado = `complete`.

1. Compruebe la lógica del filtro y que los paréntesis y los operadores se colocan correctamente: por ejemplo, `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   Un filtro incorrecto suele ser la causa de discrepancias de datos entre [!DNL Commerce Intelligence] informes y los resultados esperados.

1. Guarde `Filter Set`.

Una vez guardado un conjunto de filtros, puede aplicarlo a cualquier métrica que utilice la misma tabla. Por ejemplo, si creó un(a) `Filter Set` en la tabla `orders`, puede aplicarlo a *cualquier métrica* creada en esta tabla, como `Revenue`.

>[!NOTE]
>
>`Filter Sets` también se puede aplicar a columnas calculadas en [!DNL Commerce Intelligence]. Puede solicitar aplicar un conjunto de filtros a una dimensión de datos creada en [!DNL Commerce Intelligence] a través de poniéndose en contacto con el soporte técnico.

## Relacionado

* [Prácticas recomendadas para segmentación y filtrado](../../best-practices/segment-filter.md)
