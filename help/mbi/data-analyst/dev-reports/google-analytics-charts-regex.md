---
title: Creación de gráficos de Google Analytics
description: Aprenda a crear gráficos a partir de los datos de los Google Analytics.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# Crear [!DNL Google Analytics] gráficos

(con ayuda de sintaxis regex)

Una vez que hayas conectado tu [[!DNL Google Analytics] cuenta](../../data-analyst/importing-data/integrations/google-analytics.md), puedes crear gráficos con tus datos de [!DNL Google Analytics].

## Crear [!DNL Google Analytics] gráficos

1. Haga clic en **[!UICONTROL Add Chart** > **Create New Chart]**.

1. Al seleccionar una métrica en `Chart Builder`, desplácese hasta la parte inferior de la lista para encontrar una sección que incluya sus perfiles de [!DNL Google Analytics]. Aparece un segundo menú desplegable de métricas. Aquí puede elegir la métrica que desea analizar.

1. Una vez que haya elegido la métrica, puede continuar con este gráfico como si fuera cualquier otro gráfico seleccionando los `time period`, `interval` y los datos `perspectives` que desee ver.

1. La principal diferencia aquí es que `√` usa expresiones regulares para los filtros. Una expresión regular (regex para abreviar) es una cadena de texto especial para describir un patrón de búsqueda. Consulte ejemplos de sintaxis regex en la [[!DNL Google] guía de expresiones regulares de Analytics](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>Los únicos caracteres especiales a los que se debe aplicar un escape utilizando el carácter \ son los siguientes metacaracteres:

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
