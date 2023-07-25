---
title: Creación de gráficos de Google Analytics
description: Aprenda a crear gráficos a partir de los datos de los Google Analytics.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Crear [!DNL Google Analytics] tablas

(con ayuda de sintaxis regex)

Después de haber conectado su [[!DNL Google Analytics] account](../../data-analyst/importing-data/integrations/google-analytics.md), puede crear gráficos con su [!DNL Google Analytics] datos.

## Crear [!DNL Google Analytics] Gráficos

1. Clic **[!UICONTROL Add Chart** > **Create New Chart]**.

1. Al seleccionar una métrica en la `Chart Builder`, desplácese hasta la parte inferior de la lista para buscar una sección que incluya su [!DNL Google Analytics] Perfiles. Aparece un segundo menú desplegable de métricas. Aquí puede elegir la métrica que desea analizar.

1. Después de elegir la métrica, puede continuar con este gráfico como si fuera cualquier otro gráfico seleccionando la variable `time period`, `interval`, y datos `perspectives` que le gustaría ver.

1. La diferencia principal aquí es que `√` utiliza expresiones regulares para los filtros. Una expresión regular (regex para abreviar) es una cadena de texto especial para describir un patrón de búsqueda. Consulte ejemplos de sintaxis regex en la [[!DNL Google] Guía de expresiones regulares de Analytics](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>Los únicos caracteres especiales a los que se debe aplicar un escape utilizando el carácter \ son los siguientes metacaracteres:

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
