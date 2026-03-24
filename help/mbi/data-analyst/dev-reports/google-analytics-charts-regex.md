---
title: Creación de gráficos de Google Analytics
description: Aprenda a crear gráficos a partir de los datos de Google Analytics.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/xfh0BjVasnSNP9mic7ps4jckaGpjF7INFNi2lSaKi-o
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 160
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
