---
title: Creación de conjuntos de filtros para métricas
description: Obtenga información sobre cómo crear conjuntos de filtros guardados y aplicarlos a las métricas.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '277'
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
