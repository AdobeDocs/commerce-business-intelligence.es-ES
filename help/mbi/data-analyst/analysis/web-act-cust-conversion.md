---
title: Análisis de la actividad del sitio web y las tasas de conversión de clientes
description: Aprenda a configurar un tablero que haga un seguimiento de la actividad del sitio web, incluidas las vistas de página, las sesiones y los usuarios, y de la tasa de conversión de clientes a lo largo del tiempo.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
role: Admin, User
feature: Reports, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# Análisis de actividad del sitio web

[!DNL Adobe Commerce Intelligence] le permite integrar fácilmente sus datos de costos de publicidad con el resto de sus datos. Esto no solo le permite comprender la actividad de su sitio web, sino que también le permite obtener el porcentaje de visitantes en su sitio web que se convierten en usuarios registrados o realizan una compra.

En este tema se muestra cómo configurar un tablero que realice un seguimiento de la actividad del sitio web, incluidas las vistas de página, las sesiones y los usuarios, así como de la tasa de conversión de clientes a lo largo del tiempo.

## Requisitos previos

**Importe sus datos de costos de publicidad** - Conecte [[!DNL [Google AdWords]]](../importing-data/integrations/google-adwords.md) a [!DNL Adobe Commerce Intelligence] - esto sincroniza automáticamente su gasto de [!DNL AdWords] en Commerce Intelligence.

**Rastrear datos del canal de adquisición de usuarios** - Para enlazar los datos de [!DNL Google AdWords] con pedidos específicos de la base de datos, debe [rastrear la adquisición de usuarios](../analysis/google-track-user-acq.md) a través de [!DNL Google Analytics E-commerce]. Esto le permite conectar cada pedido con una fuente y un medio de utm.

## Campañas de adquisición de usuarios

Esta colección de informes se crea de la siguiente manera:

* Métricas que se generan automáticamente al conectar los datos de [!DNL Google AdWords]
* Métricas básicas que ya deberían estar disponibles en su cuenta, como `Number of orders` y `New users`
* Dimension creados al unir los datos de [!DNL Google Analytics Ecommerce] a la base de datos, como el origen de utm del pedido y el medio de utm del pedido. Póngase en contacto con el equipo de asistencia si estos campos no están disponibles actualmente en su cuenta

## Creación de informes

**Comience creando un informe que muestre la cantidad de vistas de página, sesiones y usuarios a lo largo del tiempo:**

1. Cree un informe.
1. Haga clic en **[!UICONTROL Add Metric]**, luego pase el ratón sobre la sección [!DNL Google Analytics] en la parte inferior de la lista desplegable y seleccione `Page Views`.
1. Agregue otra métrica, volviendo a pasar el ratón sobre la sección [!DNL Google Analytics], esta vez seleccionando `Sessions`.
1. Agregue una tercera métrica, volviendo a pasar el ratón sobre la sección [!DNL Google Analytics], esta vez seleccionando `Users`.
1. Ahora cambie el período de tiempo a un intervalo móvil, de hace 31 días a hace 1 día, y ajuste el intervalo de tiempo a `by day`.
1. Asigne un nombre al informe (por ejemplo, `Page views, sessions and users by day`) y haga clic en **[!UICONTROL Save]**.

**El segundo informe observa el número de vistas de página en el último año:**

1. Cree un informe.
1. Haga clic en **[!UICONTROL Add Metric]**, pase el ratón sobre la sección [!DNL Google Analytics] en la parte inferior de la lista desplegable y seleccione _Vistas de página_.
1. Cambie el período de tiempo a un intervalo móvil, de hace 13 meses a hace 1 mes, y ajuste el intervalo de tiempo a `by month`.
1. Asigne un nombre al informe, como `Page views by month,` y haga clic en **[!UICONTROL Save]**.

**El tercer gráfico observa la tasa de salida hacia otro sitio del último año:**

1. Cree un informe.
1. Haga clic en **[!UICONTROL Add Metric]**, pase el ratón sobre la sección [!DNL Google Analytics] en la parte inferior de la lista desplegable y seleccione _Tasa de salida hacia otro sitio_.
1. Cambie el período de tiempo a un intervalo móvil, de hace 13 meses a hace 1 mes, y ajuste el intervalo de tiempo a `by month`.
1. Asigne un nombre al informe, como `Bounce rate by month`, y haga clic en **[!UICONTROL Save]**.

**Ahora, observe la longitud promedio de sesión de los nuevos visitantes en comparación con los visitantes que regresan:**

1. Cree un informe.
1. Haga clic en **UICONTROL Agregar métrica**, pase el ratón sobre la sección [!DNL Google Analytics] en la parte inferior de la lista desplegable y seleccione `Average Session Length`.
1. ¿Desea cambiar el período de tiempo a un intervalo móvil, de hace 13 meses a hace 1 mes, y ajustar el intervalo de tiempo a `by month`?
1. Agregue un `Group by` y seleccione `New or returning visitor`.  Marque la casilla `Show All` y luego haga clic en **[!UICONTROL Apply]**.
1. Asigne un nombre al informe, como `Average session length`, y haga clic en **[!UICONTROL Save]**.

**A continuación, observe sus dominios de referencia principales en los últimos 30 días:**

1. Cree un informe.
1. Haga clic en **[!UICONTROL Add Metric]**, pase el ratón sobre la sección [!DNL Google Analytics] en la parte inferior de la lista desplegable y seleccione `Sessions`.
1. Cambie el período de tiempo a un intervalo móvil, de hace 31 días a hace 1 día, y ajuste el intervalo de tiempo a `none`.
1. Agregue un `Group by` y seleccione `ga:source`.  Marque la casilla _Mostrar todo_ y luego haga clic en **[!UICONTROL Apply]**.
1. Agregue otro `group by` y seleccione `ga:medium`. Vuelva a marcar la casilla `Show All` y, a continuación, haga clic en **[!UICONTROL Apply]**.
1. Asigne un nombre al informe, como `Top 20 Referring Domains, 30 Days`, y haga clic en **[!UICONTROL Save]**.

**Finalmente, observe la conversión:**

1. Cree un informe.
1. Añada las siguientes métricas:

* `New users`
   * Haga clic en **[!UICONTROL Hide]** debajo del nombre de la métrica

* `Number of orders`
   * Agregue un filtro para `Customer's order number` = 1 y haga clic en **[!UICONTROL Apply]**
   * Cambie el nombre de la métrica haciendo clic en el nombre de la métrica, llamándola `Number of first orders` y luego haga clic en **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** la métrica

* `Users`
   * **[!UICONTROL Hide]** la métrica
   * Cambie el período de tiempo a `24 months ago to now` y ajuste el intervalo de tiempo a `by month`.
   * Agregue las siguientes fórmulas haciendo clic en **[!UICONTROL Formula]**.
   * A/D y haga clic en **[!UICONTROL Apply]**
   * Cambiar nombre de fórmula `Registration conversion`
   * B/D y haga clic en **[!UICONTROL Apply]**
   * Cambiar nombre de fórmula `First order conversion`
   * C/D y haga clic en **[!UICONTROL Apply]**
   * Cambiar nombre de fórmula `Any order conversion`

* Asigne un nombre al informe, como `Conversion by month`, y haga clic en **[!UICONTROL Save]**.

## Pasos siguientes

Ahora que tiene acceso a los datos del tráfico web y a las tasas de conversión, puede empezar a extraer estos datos para tomar decisiones comerciales, como ¿Qué sitios son los mejores para dirigir el tráfico al sitio? o ¿Cuál de sus campañas es más eficaz para adquirir clientes con el alto valor de duración?

A medida que ajusta el gasto en publicidad y la estrategia de marketing, puede seguir realizando un seguimiento de los resultados en [!DNL Commerce Intelligence], iterando en este panel para satisfacer las prioridades en evolución de su empresa.
