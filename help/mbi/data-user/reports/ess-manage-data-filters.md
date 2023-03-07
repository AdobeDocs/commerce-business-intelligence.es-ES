---
title: Creación de conjuntos de filtros para métricas
description: Obtenga información sobre cómo crear conjuntos de filtros guardados y aplicarlos a las métricas.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Creación de conjuntos de filtros

Si tiene varias métricas en [!DNL MBI] Si necesita filtrarse de forma similar (por ejemplo, filtrando pedidos de prueba), puede crear conjuntos de filtros guardados y aplicarlos a las métricas. Esto le ahorra tiempo, ya que no tiene que añadir filtros individuales al crear o editar una métrica.

Consulte la [vídeo de formación](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html?lang=en) para obtener más información.

>[!NOTE]
>
>Requiere [Permisos de administración](../../administrator/user-management/user-management.md).

1. Clic **[!DNL Manage Data** > **Filter Sets]** en la barra lateral.

   ![](../../assets/create-filter-sets.png)

1. Clic **[!UICONTROL Add Filter Set]** en la parte superior de la página.

1. Seleccione la tabla que contiene las métricas que desea filtrar.

   Por ejemplo, si desea filtrar los `Total number of orders` y se basa en la variable `orders` , seleccione esa tabla.

1. Asigne un nombre al `Filter Set`.

1. Añada todos los filtros relevantes.

   Por ejemplo, si solo desea incluir pedidos con un estado de completado en su `Total number of orders` métrica, aplicaría un filtro que excluyera todos los pedidos que no tuvieran el estado = `complete`.

1. Compruebe la lógica del filtro y que los paréntesis y operadores se colocan correctamente: por ejemplo, `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   Un filtro incorrecto suele ser la causa de discrepancias de datos entre [!DNL MBI] y sus resultados esperados.

1. Guarde el `Filter Set`.

Una vez guardado un conjunto de filtros, puede aplicarlo a cualquier métrica que utilice la misma tabla. Por ejemplo, si ha creado un `Filter Set` en el `orders` tabla, puede aplicarla a *cualquier métrica* creado en esta tabla, como `Revenue`.

>[!NOTE]
>
>`Filter Sets` también se puede aplicar a columnas calculadas en [!DNL MBI]. Puede solicitar aplicar un conjunto de filtros a una dimensión de datos creada en [!DNL MBI] a través de poniéndose en contacto con el servicio de asistencia.

## Relacionado

* [Prácticas recomendadas para segmentación y filtrado](../../best-practices/segment-filter.md)
