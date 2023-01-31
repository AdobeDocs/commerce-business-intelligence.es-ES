---
title: Seguimiento de UTM en Google Analytics
description: Obtenga información sobre las prácticas recomendadas para el seguimiento UTM (etiquetado) en Google Analytics.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# Seguimiento de UTM

`UTM` seguimiento es una convención de etiquetado para direcciones URL que le permite analizar de dónde provienen los usuarios. Si observa las direcciones URL en las que hace clic desde la mayoría de los correos electrónicos de marketing o las publicidades de banner, verá etiquetado de UTM. Son esos vínculos largos los que terminan con cosas como `utm\_source` y `utm\_medium`.

[!DNL Google Analytics] uses `UTM` etiquetado para saber de dónde proviene el tráfico. Parte de esta información proviene del [Referente HTTP](https://en.wikipedia.org/wiki/HTTP_referer) pero el resto, tienes que proveerte `UTM` parámetros. Cuando vea `google adwords` o `email marketing` significa que `UTM` parámetros que se registran a partir del clic en vínculo original y que luego se almacenan en las cookies de los usuarios. Desde allí, [!DNL Google Analytics] utiliza esos datos para [atributos comportamientos interesantes](../data-analyst/analysis/google-track-user-acq.md) del sitio. Comprender cuáles son esos parámetros le ayuda a comprender mejor cómo configurar y utilizar el etiquetado UTM.

## Prácticas recomendadas para el etiquetado de UTM

A continuación se enumeran las cinco cosas más importantes que debe recordar al configurar las URL con `UTM` etiquetado.

### 1. Intente etiquetar cada URL que pueda controlar que llega a su sitio

Cada vez que pida a las personas que hagan clic en un vínculo, debe configurar `UTM` etiquetado. Esto incluye todos los vínculos de correo electrónico (es probable que su proveedor de servicios de correo electrónico tenga una forma de etiquetar automáticamente sus URL), vínculos de anuncios, artículos de prensa y publicaciones de blogs.

### 2. Utilice una herramienta para crear la URL

`UTM`Las direcciones URL con etiquetas pueden ser bastante engorrosas. En lugar de intentar escribirlas a tiempo, utilice una herramienta [like this](https://support.google.com/analytics/answer/1033867?hl=en) para ayudarle. Esto garantiza que esté pensando en añadir todos los parámetros coherentes a la URL y que obtenga la URL para copiarla y pegarla directamente desde ella. Para administrar vínculos sociales, herramientas como [!DNL Hootsuite] incluya la opción para agregar parámetros de URL personalizados a todos los vínculos.

### 3. Asegúrese de que distingue entre mayúsculas y minúsculas en los valores de parámetro

Es importante recordar que la etiqueta `utm\_source=adwords` es una etiqueta diferente a `utm\_source=Adwords`. Considere hacer todo en minúsculas.

### 4. Almacene los valores de parámetro UTM en la base de datos

Cada vez que se produzca una transacción o un evento, deberá evaluar el rendimiento de las actividades de marketing. Para ello, lea los valores de los parámetros de UTM de la [[!DNL Google Analytics] cookie en la base de datos](../data-analyst/analysis/google-track-user-acq.md).

### 5. Considere cómo nombra las campañas

Para realizar un seguimiento de cómo mejoran los esfuerzos de marketing a lo largo del tiempo, debe conocer las convenciones de nomenclatura con precisión. Manténgalo simple y minimice todo lo posible. Los sistemas de nomenclatura complicados son más difíciles de mantener.

Una vez que capture estos datos en su base de datos, puede evaluar el rendimiento de su marketing y publicidad mediante análisis más sofisticados, que incluyen [Valor de duración del cliente](../data-analyst/analysis/ess-expected-ltv.md), [Repetir tasas de compra](../data-analyst/analysis/repurchase-behavior.md)y [Valor de pedido promedio](../data-analyst/analysis/basic-analytics.md).
