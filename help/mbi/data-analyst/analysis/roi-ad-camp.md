---
title: Aumento del ROI en las campañas publicitarias
description: Obtenga información sobre varios métodos diferentes para evaluar el rendimiento de la campaña.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 0%

---

# Campañas publicitarias y ROI

MBI le permite [combinar datos de costes de publicidad y datos de ingresos](../../data-analyst/importing-data/integrations/google-adwords.md) de la base de datos. Esto le ayudará a identificar qué campañas tienen el ROI más alto. En este artículo, exploramos varios métodos diferentes para evaluar el rendimiento de su campaña.

## Requisitos previos

* Importe sus datos de coste publicitario:
   * [Conecte su [!DNL Google AdWords] a [!DNL MBI]](../importing-data/integrations/google-adwords.md): Esto sincronizará automáticamente su [!DNL Adwords] gastar en [!DNL MBI]
   * [Cargar otros datos de costes de publicidad](../importing-data/connecting-data/import-offline-ad-data.md): Esto se recomienda para los canales sin un conector directo a [!DNL MBI]
   * Si importa datos de costes de varias fuentes, podemos [consolidar](../../best-practices/consolidating-your-tables.md) los datos de [!DNL MBI]. Simplemente [enviar un ticket de asistencia](../../guide-overview.md).
* [Seguimiento de datos del canal de adquisición de usuarios](../analysis/google-track-user-acq.md)

## Campañas de adquisición de usuarios

Las campañas dirigidas a la adquisición de usuarios se pueden medir desde muchas perspectivas, entre ellas:

1. El número de usuarios nuevos adquiridos de las campañas
1. La tasa de conversión de registro a compra de campañas
1. El ROI de las campañas basadas en el valor de duración promedio del usuario (LTV)

Los análisis (1) y (2) anteriores se exploran en un tutorial independiente sobre [identificación de los canales de marketing principales](../analysis/most-value-source-channel.md). Aquí, analizamos el análisis (3) para medir el ROI de la campaña a lo largo del tiempo. Esto responderá si los usuarios adquiridos a partir de una campaña en particular generaron suficientes ingresos de por vida para cubrir su coste de adquisición.

>[!NOTE]
>
>Asumiremos que todos los costes de campaña se utilizaron exclusivamente para adquirir nuevos usuarios. En realidad, el coste de la campaña también se comparte con la adquisición de visitas no convertidas, compradores repetidos, etc. Sin embargo, suponiendo que todo el coste se utiliza para adquirir nuevos usuarios registrados, el ROI resultante representará el peor escenario (el mayor coste por adquisición), por lo que puede estar seguro de que su ROI real es mayor que nuestro cálculo.
>
>Ejemplo: Suponiendo que gastó 20 dólares en una campaña que generó 10 nuevos usuarios y 10 compradores repetidos, el coste real por cada nuevo usuario es de 1 dólar, pero bajo nuestro supuesto de que todo el coste se destinó a adquirir nuevos usuarios, el coste por adquisición es de 2 dólares).

**1. Comience creando un gráfico que segmente su Coste de publicidad por Campañas:**

1. Cree un [!UICONTROL Metric] que suma su gasto a lo largo del tiempo
1. Vaya a [!UICONTROL Data > Metrics]
1. Select `Add New Metric` y seleccione [!DNL `Adwords...`] tabla que registra su [!DNL AdWords] datos de costes.
1. En el editor de métricas, asigne un nombre a la métrica (por ejemplo, [!UICONTROL AdWord Cost])
1. Con los desplegables, realice una **Sum** en el `adCost` en la columna [!DNL Adwords...] tabla (cambio) ordenada por el `date` para abrir el Navegador.
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. hemos terminado. Haga clic en `Back to Metric List` en la parte superior y vaya a cualquier panel.

1. Cree un informe que contenga segmentos gastados por campañas
1. En cualquier tablero, haga clic en [!UICONTROL Add Report > Create new report]
1. Seleccione el [!UICONTROL Adword Cost] métrica que acabamos de crear
1. Configure las variables [!UICONTROL Time period] a `All-time`y [!UICONTROL Interval] a `None`
1. En el `Group by` ficha, agregar `campaign` como [!UICONTROL grouping field]y haga clic en `Add All` en la casilla .
1. Este informe mostrará su [!DNL AdWords] coste por campañas

**2. A continuación, crearemos un informe que cuente los nuevos usuarios por campañas:**

1. En cualquier tablero, haga clic en **[!UICONTROL Add Report > Create new report]**
1. Seleccione el `New users` métrica que cuenta el número de usuarios registrados nuevos a lo largo del tiempo
1. Configure las variables [!UICONTROL Time period] a `All-time`y [!UICONTROL Interval] a `None`
1. En el `Group by` ficha, agregar `campaign` como `grouping field`y haga clic en **`Add All`** en el cuadro
1. Este informe muestra los usuarios registrados por campaña

**3. También vamos a crear un informe que segmente el promedio de LTV de los usuarios por campañas:**

1. En cualquier tablero, haga clic en **[!UICONTROL Add Report > Create new report]**
1. Seleccione el `Average lifetime revenue` métrica que calcula el ingreso promedio de un usuario
1. Configure las variables [!UICONTROL Time period] a `All-time`y [!UICONTROL Interval] a `None`
1. En el `Group by` ficha, agregar `campaign` o `utm\_campaign` como [!UICONTROL grouping field]y haga clic en `Add All` en el cuadro
1. Este informe mostrará los ingresos promedio de duración del usuario por campañas

**Finalmente, calcularemos el ROI de la campaña reuniendo estos tres análisis en un solo informe:**

1. En cualquier tablero, haga clic en **[!UICONTROL Add Report > Create new report]**
1. Agregue como entrada las tres métricas que hemos utilizado anteriormente. A cada uno se le asignará una letra (por ejemplo,\[`A`\], \[`B`\] y \[`C`\])
1. [!UICONTROL Cost]: Agregue la métrica Costo de AdWords : será la variable \[A\]. Esto simplemente devolverá el coste por campañas.
1. [!UICONTROL Users]: Agregue la métrica Nuevos usuarios: será la variable \[B\]. Esto simplemente devolverá el número de usuarios por campaña.
1. [!UICONTROL LTV]: Agregar la métrica Ingresos promedio de duración: será la variable \[`C`\]. Esto simplemente devolverá LTV mediante campañas.

1. Haga clic en el icono ocultar situado junto a la palabra Gráfico para centrarse en la tabla
1. Ahora usaremos `Add Formula` para combinar estas métricas, de la siguiente manera:
1. [!UICONTROL ROI]: Introduzca la fórmula `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`, si \[`A`\] representa `Ad Cost by Campaigns`, \[`B`\] representa `New users by campaigns`y \[`C`\] `LTV by campaigns`. Esto devolverá la proporción de (LTV de usuario promedio - coste promedio por adquisición) / (coste promedio por adquisición)
1. [!UICONTROL Avg Return per User]: Introduzca la fórmula **\[`C`\]-(\[`A`\]/\[`B`\])**. Esto devolverá el margen promedio hecho en un usuario mediante el cálculo (usuario promedio LTV) - (coste promedio por adquisición).
1. [!UICONTROL CPA]: Introduzca la fórmula **`\[A\]/\[B\]`**. Esto devolverá el coste por adquisición de la campaña real.
1. Otras métricas potenciales de las que se puede incluir [!DNL AdWords] los datos incluyen sumas de  `Impressions` y `adClicks` (de [!DNL AdWords] datos), junto con el total `number of orders` realizada a través de una campaña en particular.
1. También puede ser interesante calcular el ROI en base a LTV 30 días y 90 días después de que un usuario se registre o realice una primera compra.

1. Puede hacer clic y arrastrar las métricas y fórmulas para reordenar las columnas del informe
1. Asigne un nombre al informe y asegúrese de guardar como tabla.

## Campañas de productos

¿Está ejecutando anuncios específicos de productos? Si es así, puede medir el ROI de esas campañas calculando los ingresos y el coste de productos específicos.

>[!NOTE]
>
>Asumiremos que todos los costes de campaña se utilizaron exclusivamente para generar compras de productos específicos. Suponiendo que todo el coste se gastó en la generación de compras, el ROI resultante representará el peor escenario (el mayor coste por compra), por lo que puede estar seguro de que el ROI real es mayor que este cálculo. Ejemplo: Suponiendo que haya gastado 20 dólares en una campaña que generó 10 usuarios nuevos y 10 compras, el coste real por compra es de 1 dólar, pero asumiendo que todo el coste se destinó a adquirir nuevos usuarios, el coste por compra es de 2 dólares).*

Antes de empezar, [enviar un ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) para unir las siguientes dimensiones a la tabla de elementos de línea (`sales\_flat\_order\_item, order\_item`):

* Origen del pedido (si solo rastrea el origen de referencia a nivel de usuario, únase al origen del usuario)
* Campaña del pedido (si solo realiza el seguimiento del origen de referencia a nivel de usuario, únase a la campaña del usuario)
* Medio del pedido (si solo realiza el seguimiento del origen de referencia a nivel de usuario, únase al medio del usuario)

**1. Ahora comience creando un gráfico que devuelva ingresos por campaña para productos específicos:**

1. En cualquier tablero, haga clic en **[!UICONTROL Add Report > Create new report]**
1. Seleccione el `Revenue by items` métrica que calcula los ingresos en el nivel de elementos de línea
1. Configure las variables [!UICONTROL Time period] a `All-time`y [!UICONTROL Interval] a `None`
1. En el `Filter by` ficha, agregar `product name 'IN'` Product `A`, Producto `B`, Producto `C`, ...&quot; e incluir todos los nombres de producto dirigidos por su campaña separados por una coma (por ejemplo, `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. En el `Group by` ficha, agregar `order's campaign` o `order's utm\_campaign` como `grouping` y haga clic en **[!UICONTROL Add All]** en el cuadro
1. Este informe muestra los ingresos para productos específicos por campañas

**2. Para calcular el ROI, una vez más combinaremos las métricas en un informe:**

1. En cualquier tablero, haga clic en **[!UICONTROL Add Report > Create new report]**
1. Agregue la variable `Revenue by items` , siga el filtro y agrupe por instrucciones de la campaña para el informe de productos específicos que se muestra arriba y haga clic en **[!UICONTROL Hide]** debajo del valor escalar de la métrica
1. Ahora, agregue la variable [!DNL AdWords Cost] , siguiendo el filtro y agrupe según las instrucciones de la `Ad cost by campaigns` informe que exploramos en la `User acquisition campaigns` sección anterior; a continuación, haga clic en **[!UICONTROL Hide]** debajo del valor escalar de la métrica
1. Con estas métricas en su lugar, agregaremos fórmulas:
1. [!UICONTROL ROI]: Introduzca la fórmula `\[A\]/\[B\]`, si `\[A\]` representa `Revenue per campaign for specific product(s)` y `\[B\]` representa `Ad cost by campaigns`. Esto devolverá la proporción de (Ingresos para productos específicos) / (Coste de campaña)
1. [!UICONTROL Return]: Introduzca la fórmula `\[A\]-\[B\]`. Esto devolverá el margen promedio hecho en un usuario mediante el cálculo (usuario promedio LTV) - (coste promedio por adquisición)
1. (Opcional) [!UICONTROL Revenue]: Mostrar `Revenue by items` para ver los ingresos de productos específicos por campaña
1. (Opcional) [!UICONTROL Cost]: Mostrar `AdWords Cost` para ver el coste de las campañas

1. Asigne un nombre al informe y asegúrese de guardarlo como una tabla

**3. Repita los pasos 1 y 2 anteriores para cada uno de los productos o grupos de productos anunciados.**

## Documentación relacionada

* [Rastrear la fuente de referencia de pedidos a través de [!DNL Google Analytics] Comercio electrónico](../importing-data/integrations/google-ecommerce.md)
* [Seguimiento del origen de referencia del usuario en la base de datos](../analysis/google-track-user-acq.md)
* [Seguimiento de datos de dispositivos de usuario, exploradores y sistemas operativos en la base de datos](../analysis/track-usr-dev-browser.md)
* [Descubra las fuentes y canales de adquisición más valiosos](../analysis/most-value-source-channel.md)
* [Conecte su [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [¿Cómo [!DNL Google Analytics] ¿Funciona la atribución de UTM?](../analysis/utm-attributes.md)
* [5 prácticas recomendadas para el etiquetado UTM en [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
