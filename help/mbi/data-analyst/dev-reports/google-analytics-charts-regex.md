---
title: Crear gráficos de Google Analytics
description: Aprenda a crear gráficos a partir de los datos de sus Google Analytics.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Crear [!DNL Google Analytics] gráficos

(con la ayuda de sintaxis regex)

Una vez que haya conectado su [[!DNL Google Analytics] account](../../data-analyst/importing-data/integrations/google-analytics.md), puede crear gráficos a partir de su [!DNL Google Analytics] datos.

## Crear [!DNL Google Analytics] Gráficos

1. Haga clic en **[!UICONTROL Add Chart** > **Create New Chart]**.

1. Al seleccionar una métrica en la variable `Chart Builder`, desplácese hasta la parte inferior de la lista para encontrar una sección que incluya su [!DNL Google Analytics] Perfiles. Aparecerá un segundo menú desplegable de métricas. Aquí puede elegir la métrica que desea analizar.

1. Después de elegir la métrica, puede continuar con este gráfico como si fuera cualquier otro gráfico seleccionando la `time period`, `interval`y datos `perspectives` que le gustaría ver.

1. La principal diferencia aquí es que `√` utiliza expresiones regulares para los filtros. Una expresión regular (regex para short) es una cadena de texto especial para describir un patrón de búsqueda. Consulte ejemplos de sintaxis regex en la [[!DNL Google] guía sobre las expresiones regulares de Analytics](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>Los únicos caracteres especiales que necesitan ser escapados usando el carácter \ son los metacaracteres siguientes:

|  |  |  |  |  |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style=&quot;table-layout:auto&quot;}
