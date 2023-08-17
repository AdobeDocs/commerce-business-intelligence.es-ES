---
title: Seguimiento de UTM en Google Analytics
description: Conozca las prácticas recomendadas para el seguimiento de UTM (etiquetado) en Google Analytics.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# Seguimiento de UTM

`UTM` El seguimiento de es una convención de etiquetado de direcciones URL que le permite analizar de dónde provienen los usuarios. Si mira las direcciones URL en las que hace clic desde la mayoría de los correos electrónicos de marketing o anuncios de banners, verá el etiquetado UTM. Son esos vínculos largos los que terminan con cosas como `utm\_source` y `utm\_medium`.

[!DNL Google Analytics] utiliza `UTM` Etiquetado para saber de dónde proviene su tráfico. Parte de esta información proviene del [Referente HTTP](https://en.wikipedia.org/wiki/HTTP_referer) pero el resto lo tienes que proveer tú mismo `UTM` parámetros. Cuando vea `google adwords` o `email marketing`, significa que `UTM` Los parámetros que se registran desde el vínculo original hacen clic en y luego se almacenan en las cookies de los usuarios. A partir de ahí, [!DNL Google Analytics] utiliza esos datos para [atribuir comportamientos interesantes](../data-analyst/analysis/google-track-user-acq.md) en el sitio. Comprender para qué sirven esos parámetros le ayuda a comprender la mejor manera de configurar y utilizar el etiquetado UTM.

## Prácticas recomendadas para el etiquetado UTM

A continuación se enumeran los cinco aspectos más importantes que deben tenerse en cuenta a la hora de configurar las direcciones URL con `UTM` etiquetado.

### 1. Intente etiquetar todas las direcciones URL que puede controlar cuando llegue al sitio

Cada vez que pida a otras personas que hagan clic en un vínculo, debería estar configurando `UTM` etiquetado. Esto incluye todos los vínculos de correo electrónico (es probable que el proveedor de servicios de correo electrónico tenga una forma de etiquetar automáticamente las direcciones URL), vínculos de publicidad, artículos de prensa y publicaciones de blog.

### 2. Utilice una herramienta para crear la dirección URL

`UTM`Las direcciones URL etiquetadas con pueden ser engorrosas. En lugar de intentar escribirlos a mano, use una herramienta [como este](https://support.google.com/analytics/answer/1033867?hl=en) para ayudarte. Esto garantiza que está pensando en añadir todos los parámetros razonables a la dirección URL y que obtiene la dirección URL que copia y pega directamente de ella. Para administrar vínculos sociales, herramientas como [!DNL Hootsuite] incluya la opción de agregar parámetros de URL personalizados a todos los vínculos.

### 3. Asegúrese de que distingue entre mayúsculas y minúsculas en los valores de parámetros

Es importante recordar que la etiqueta `utm\_source=adwords` es una etiqueta diferente a `utm\_source=Adwords`. Considere la posibilidad de ponerlo todo en minúsculas.

### 4. Almacene los valores de parámetros de UTM en la base de datos

Cada vez que se produce una transacción o un evento, se desea evaluar el rendimiento de las actividades de marketing. Para ello, lea los valores de los valores de los parámetros de UTM en la [[!DNL Google Analytics] cookie en la base de datos](../data-analyst/analysis/google-track-user-acq.md).

### 5. Piense en cómo nombra las campañas

Para realizar un seguimiento de cómo mejoran los esfuerzos de marketing con el paso del tiempo, deberá ser inteligente con respecto a las convenciones de nomenclatura. Simplifique y minimice lo máximo posible. Los sistemas de nombres complicados son más difíciles de mantener.

Una vez que esté capturando estos datos en la base de datos, puede evaluar el rendimiento de su marketing y publicidad mediante análisis más sofisticados, que incluyen [Valor de duración del cliente](../data-analyst/analysis/ess-expected-ltv.md), [Tarifas de compra repetida](../data-analyst/analysis/repurchase-behavior.md), y [Valor de pedido promedio](../data-analyst/analysis/basic-analytics.md).
