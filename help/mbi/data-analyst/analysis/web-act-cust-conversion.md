---
title: Análisis de la actividad del sitio web y las tasas de conversión de los clientes
description: Obtenga información sobre cómo configurar un tablero que rastree la actividad del sitio web (incluidas las vistas de página, las sesiones y los usuarios), así como la tasa de conversión de los clientes a lo largo del tiempo.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# Análisis de la actividad del sitio web

[!DNL MBI] le permite integrar fácilmente sus datos de costes publicitarios con el resto de sus datos. Esto no solo le permite comprender la actividad del sitio web, sino que también le permite obtener el porcentaje de visitantes del sitio web que se convierten en usuarios registrados o que realizan una compra.

En este artículo, demostramos cómo configurar un tablero que rastree la actividad de su sitio web, incluidas las vistas de páginas, las sesiones y los usuarios, así como la tasa de conversión de sus clientes a lo largo del tiempo.

## Requisitos previos

**Importar los datos de coste publicitario** - Conectar [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) a [!DNL MBI] - esto sincroniza automáticamente su [!DNL AdWords] gastar en BI.

**Seguimiento de datos del canal de adquisición de usuarios** - Para atar su [!DNL Google AdWords] datos de pedidos específicos de la base de datos, necesitamos [seguimiento de la adquisición de usuarios](../analysis/google-track-user-acq.md) via [!DNL Google Analytics E-commerce], permitiéndonos conectar cada pedido con un origen y medio utm.

## Campañas de adquisición de usuarios

Esta colección de informes se crea con lo siguiente:

* Métricas que se generan automáticamente al conectar su [!DNL Google AdWords] data
* Métricas básicas que ya deberían estar disponibles en su cuenta, como `Number of orders` y `New users`
* Dimension creados al unirse a su [!DNL Google Analytics Ecommerce] datos de la base de datos, como el medio utm source del pedido y utm del pedido. Póngase en contacto con el equipo de asistencia si estos campos no están disponibles actualmente en su cuenta

## Creación de informes

**Comience creando un informe que muestre la cantidad de vistas de página, sesiones y usuarios a lo largo del tiempo:**

1. Cree un nuevo informe.
1. Haga clic en **[!UICONTROL Add Metric]** y pase el ratón por encima de [!DNL Google Analytics] en la parte inferior de la lista desplegable y seleccione `Page Views`.
1. Agregue otra métrica, pasando de nuevo el ratón por encima del [!DNL Google Analytics] sección, esta vez seleccionando `Sessions`.
1. Añada una tercera métrica, pasando de nuevo el ratón por encima del [!DNL Google Analytics] sección, esta vez seleccionando `Users`.
1. Ahora cambie su período de tiempo a un intervalo móvil, de hace 31 días a hace 1 día, y ajuste el intervalo de tiempo a `by day`.
1. Asigne un nombre al informe (por ejemplo, `Page views, sessions and users by day`) y haga clic en **[!UICONTROL Save]**.

**Nuestro segundo informe analizará la cantidad de vistas de páginas durante el año pasado:**

1. Cree un nuevo informe.
1. Haga clic en **[!UICONTROL Add Metric]**, pase el ratón por encima de [!DNL Google Analytics] en la parte inferior de la lista desplegable y seleccione _Vistas de páginas_.
1. Cambie el período de tiempo a un intervalo móvil, de hace 13 meses a hace 1 mes, y ajuste el intervalo de tiempo a `by month`.
1. Asigne un nombre al informe, como `Page views by month,` y haga clic en **[!UICONTROL Save]**.

**El tercer gráfico muestra la tasa de devolución del último año:**

1. Cree un nuevo informe.
1. Haga clic en **[!UICONTROL Add Metric]**, pase el ratón por encima de [!DNL Google Analytics] en la parte inferior de la lista desplegable y seleccione _Porcentaje de rebote_.
1. Cambie el período de tiempo a un intervalo móvil, de hace 13 meses a hace 1 mes, y ajuste el intervalo de tiempo a `by month`.
1. Asigne un nombre al informe, como `Bounce rate by month`y haga clic en **[!UICONTROL Save]**.

**Ahora, observe la longitud promedio de sesión de los nuevos visitantes en comparación con los visitantes que regresan:**

1. Cree un nuevo informe.
1. Haga clic en **UICONTROL Agregar métrica**, pase el ratón por encima de [!DNL Google Analytics] en la parte inferior de la lista desplegable y seleccione `Average Session Length`.
1. Cambie el período de tiempo a un intervalo móvil, de hace 13 meses a hace 1 mes, y ajuste el intervalo de tiempo a `by month`?
1. Agregue un `Group by` y seleccione `New or returning visitor`.  Marque la `Show All` casilla; a continuación, haga clic en **[!UICONTROL Apply]**.
1. Asigne un nombre al informe, como `Average session length`y haga clic en **[!UICONTROL Save]**.

**A continuación, eche un vistazo a los dominios de referencia principales en los últimos 30 días:**

1. Cree un nuevo informe.
1. Haga clic en **[!UICONTROL Add Metric]**, pase el ratón por encima de [!DNL Google Analytics] en la parte inferior de la lista desplegable y seleccione `Sessions`.
1. Cambie el período de tiempo a un intervalo móvil, de hace 31 días a hace 1 día, y ajuste el intervalo de tiempo a `none`.
1. Agregue un `Group by` y seleccione `ga:source`.  Marque la _Mostrar todo_ casilla; a continuación, haga clic en **[!UICONTROL Apply]**.
1. Agregue otro `group by` y seleccione `ga:medium`. De nuevo, compruebe el `Show All` casilla; a continuación, haga clic en **[!UICONTROL Apply]**.
1. Asigne un nombre al informe, como `Top 20 Referring Domains, 30 Days`y haga clic en **[!UICONTROL Save]**.

**Finalmente, eche un vistazo a la conversión:**

1. Cree un nuevo informe.
1. Agregue las métricas siguientes:

* `New users`
   * Haga clic en **[!UICONTROL Hide]** debajo del nombre de la métrica

* `Number of orders`
   * Añadir un filtro para `Customer's order number` = 1 y haga clic en **[!UICONTROL Apply]**
   * Para cambiar el nombre de la métrica, haga clic en el nombre de la métrica y llámele `Number of first orders`y haga clic en **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** la métrica

* `Users`
   * **[!UICONTROL Hide]** la métrica
   * Cambie el periodo de tiempo a `24 months ago to now`y ajustar el intervalo de tiempo a `by month`.
   * Agregue las siguientes fórmulas haciendo clic en **[!UICONTROL Formula]**.
   * A/D y haga clic en **[!UICONTROL Apply]**
   * Cambiar el nombre de la fórmula `Registration conversion`
   * B/D y haga clic en **[!UICONTROL Apply]**
   * Cambiar el nombre de la fórmula `First order conversion`
   * C/D y haga clic en **[!UICONTROL Apply]**
   * Cambiar el nombre de la fórmula `Any order conversion`

* Asigne un nombre al informe, como `Conversion by month`y, a continuación, haga clic en **[!UICONTROL Save]**.

## Pasos siguientes

Ahora que tiene acceso a los datos de sus tasas de conversión y tráfico web, puede empezar a aprovecharlos para dirigir las decisiones comerciales. ¿Qué sitios son los mejores para conducir el tráfico a su sitio?  ¿Cuál de sus campañas es la más efectiva para adquirir clientes con el alto valor de duración?

Al ajustar la inversión en publicidad y la estrategia de marketing, puede seguir realizando un seguimiento de los resultados en [!DNL MBI], iterando en este tablero para satisfacer las cambiantes prioridades de su empresa.
