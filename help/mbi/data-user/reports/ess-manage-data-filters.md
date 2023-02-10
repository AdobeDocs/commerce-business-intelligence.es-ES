---
title: Crear conjuntos de filtros para métricas
description: Obtenga información sobre cómo crear conjuntos de filtros guardados y aplicarlos a las métricas.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Crear conjuntos de filtros

Si tiene varias métricas en [!DNL MBI] que deben filtrarse de forma similar (por ejemplo, para filtrar los pedidos de prueba), puede crear conjuntos de filtros guardados y aplicarlos a las métricas. Esto le ahorra tiempo, ya que no tiene que agregar filtros individuales al crear o editar una métrica.

Consulte nuestra [vídeo de formación](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html?lang=en) para obtener más información.

>[!NOTE]
>
>Requiere [Permisos de administrador](../../administrator/user-management/user-management.md).

1. Haga clic en **[!DNL Manage Data** > **Filter Sets]** en la barra lateral.

   ![](../../assets/create-filter-sets.png)

1. Haga clic en **[!UICONTROL Add Filter Set]** en la parte superior de la página.

1. Seleccione la tabla que contiene las métricas que desea filtrar.

   Por ejemplo, si desea filtrar su `Total number of orders` y se basa en la variable `orders` seleccione esa tabla.

1. Asigne un nombre a la variable `Filter Set`.

1. Añada todos los filtros relevantes.

   Por ejemplo, si solo queremos incluir pedidos con un estado de finalización en nuestra `Total number of orders` , aplicaríamos un filtro que excluye todos los pedidos que no tienen estado = `complete`.

1. Compruebe la lógica del filtro y que los paréntesis y operadores están colocados correctamente: por ejemplo, `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   Un filtro incorrecto suele ser la causa de discrepancias de datos entre [!DNL MBI] y los resultados esperados.

1. Guarde el `Filter Set`.

Una vez guardado un conjunto de filtros, puede aplicarlo a cualquier métrica que esté usando la misma tabla. Por ejemplo, si ha creado un `Filter Set` en el `orders` tabla, puede aplicarla a *cualquier métrica* creado en esta tabla, como `Revenue`.

>[!NOTE]
>
>`Filter Sets` también se puede aplicar a columnas calculadas en [!DNL MBI]. Puede solicitar la aplicación de un conjunto de filtros a una dimensión de datos creada en [!DNL MBI] mediante contacto con el servicio de asistencia técnica.

## Relacionado

* [Prácticas recomendadas para la segmentación y el filtrado](../../best-practices/segment-filter.md)
