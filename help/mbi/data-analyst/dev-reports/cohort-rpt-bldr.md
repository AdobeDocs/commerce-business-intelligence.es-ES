---
title: Report Builder de cohorte
description: Obtenga información sobre el análisis de grupos de usuarios que comparten características similares a lo largo de sus ciclos de vida.
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 0%

---

# Report Builder de cohorte

¿Alguna vez ha querido estudiar cómo se comportan los distintos subconjuntos de sus usuarios con el tiempo? Por ejemplo, ¿alguna vez se ha preguntado si los usuarios que se registran durante un período de promoción tienen un ingreso promedio de duración mayor que los que no lo tienen? Si la respuesta es `Yes`, luego la variable `Cohort Report Builder` es la herramienta perfecta para usted. [!DNL MBI] está especialmente optimizado para realizar este análisis y hacerlo relevante para su negocio.

## ¿Qué es el análisis de cohorte? {#what}

`Cohort` El análisis puede definirse en términos generales como el análisis de grupos de usuarios que comparten características similares a lo largo de sus ciclos de vida. Permite identificar tendencias de comportamiento en diferentes grupos de usuarios.

Para obtener un manual más detallado sobre `cohort` análisis, [eche un vistazo aquí](https://www.cohortanalysis.com/) - ¡Escribimos el sitio en él!

En [!DNL MBI] tablero, es fácil crear un usuario `cohorts` basado en un `cohort` fecha y una métrica en su cuenta.

## Bueno, ¿por qué es importante el análisis de cohorte? {#important}

Como se ha mencionado anteriormente, `cohort` analysis le permite identificar tendencias de comportamiento entre diferentes grupos de usuarios. Con una comprensión sólida de cómo se comportan ciertos grupos, puede adaptar sus decisiones y gastos para maximizar sus ventas. Consideremos, por ejemplo, los ingresos de por vida `cohort` análisis: aunque este tipo de análisis es beneficioso por muchas razones, el inmediato es tomar mejores decisiones de adquisición de clientes.

## ¿Cómo creo mis propios `cohort` análisis?

### Nueva arquitectura

Estas son las instrucciones para usar la variable `Cohort Report Builder` en el [Nueva arquitectura](../../administrator/account-management/new-architecture.md).

1. Haga clic en **[!UICONTROL Report Builder]** en la pestaña izquierda o **[!UICONTROL Add Report** > **Create Report]** en cualquier tablero.

1. En el `Report Builder` pantalla de selección, haga clic en **[!UICONTROL Create Report]** junto a la variable `Visual Report Builder` .

**Adición de una métrica**

Ahora que estamos en el `Report Builder`, agregamos la métrica en la que queremos realizar el análisis (ejemplo: `Revenue` o `Orders`).

>[!NOTE]
>
>Nativo [!DNL Google Analytics] las métricas no son compatibles con `Cohort Report Builder`.

**Alternar la vista de métrica a`Cohort`**

![](../../assets/visual-report-builder-cohort-toggle.png)

Esto abre una nueva ventana en la que podemos configurar los detalles del `Cohort` Informe.

### Se necesitan cinco especificaciones para crear un `Cohort` informe:

1. Cómo agrupar el `cohorts`
1. La variable `cohort` periodo de tiempo
1. El número de `cohorts` para ver
1. La cantidad mínima de datos de cada `cohort` must contain
1. Intervalo de tiempo después de `cohort` Ocurrencia

#### 1. Agrupación `cohorts`

`Cohorts` se agrupan por una marca de tiempo, como **fecha de registro** o **fecha del primer pedido**.

>[!NOTE]
>
>No puede usar la misma marca de tiempo en la que está creada la métrica para la variable `cohort` fecha. Para un análisis que lo requiera, puede usar la variable `Standard report builder` en su lugar.

#### 2. `Cohort` periodo de tiempo

Elija el período de tiempo para agrupar `cohorts` por. En otras palabras, qué parte de la marca de tiempo seleccionada arriba es más importante; el `week`, `month`, `quarter`o `year`?  El informe mostrará los datos en el intervalo que seleccione aquí

#### 3. y 4. Establezca el número de `cohorts` para ver y cuántos datos cada `cohort` debe tener

Estos parámetros le ayudan a ver únicamente los `cohorts` que le interesa, y que es útil `Preview` en la parte inferior de la ventana, se muestra exactamente qué cohortes se mostrarán en el informe.

De forma predeterminada, la variable `cohort` no se incluirá a menos que cambie la cantidad mínima de datos necesaria para cada `cohort` a `0`. En este caso, la variable `cohort` para el período de tiempo actual solo incluirá datos parciales.

#### 5. Intervalo de tiempo después de `Cohort` Ocurrencia

Esta función le permite establecer el intervalo de tiempo de datos que ve para el `cohorts`. Por ejemplo, si desea ver 24 mensualmente `cohorts` basado en `customer's first order date`, pero solo le interesan los primeros 3 meses de datos de cada `cohort`, puede configurar la variable `number of cohorts to view` a `24` y `time range after cohort occurrence` a `3`.

El intervalo para este valor cambia con el que haya seleccionado en la variable `cohort time period` y el valor se establece en `12` de forma predeterminada; el valor no cambiará a menos que haga clic en el icono del calendario para editarlo.

![](../../assets/cohort-time-range.png)

#### Otras notas

* [!UICONTROL Filters]: aplicadas a sus métricas permanecerán intactas cuando alterne entre `Standard` y `Cohort` vistas.

* Consulte [`Perspectives`](#perspectives).

#### Ejemplo

Aquí hay un ejemplo para unirlo todo. En este ejemplo, deseo comprobar el comportamiento de los pedidos después de `cohort`La primera compra de para ver si esa cohorte está regresando para hacer compras repetidas en los próximos 6 meses.

![Cohorte de pedidos](../../assets/crb_example.gif)

### Arquitectura heredada

#### Arquitectura heredada {#personalinfo}

A continuación encontrará instrucciones específicas de la versión heredada de la `Cohort Report Builder`. Si le interesa utilizar la nueva versión, consulte [Nueva arquitectura](../../administrator/account-management/new-architecture.md) para obtener más información sobre la migración a [!DNL MBI] Nueva cuenta de Arquitectura.

#### ¿Cómo creo mis propios `cohort` análisis? {#create}

![](../../assets/create-cohort-analysis.png)

`Cohort` análisis en acción! Aquí, podemos ver que los ingresos crecen con el tiempo de forma acumulativa y por usuario.

En esta sección, le guiamos a través de la creación de su `cohort` análisis. Para ver ejemplos (y GIF animados que demuestren el proceso), eche un vistazo a la [Sección Ejemplos](#examples) de este artículo.

1. Haga clic en **[!UICONTROL Report Builder]** en la pestaña izquierda o **[!UICONTROL Add Report** > **Create Report]** en cualquier tablero.

1. En el `Report Builder Selection` pantalla, haga clic en **[!UICONTROL Create Report]** junto a la variable `Cohort Analysis` .

#### Adición de una métrica

Ahora que estamos en el `Cohort Report Builder`, vamos a añadir la métrica (ejemplo: `Revenue` o `Number of orders`) en la que queremos realizar el análisis.

>[!NOTE]
>
>Nativo [!DNL Google Analytics] las métricas no son compatibles con `Cohort Report Builder`.

#### Selección de la fecha de cohorte {#date}

El siguiente paso es especificar la variable `cohort date`. Esta es la fecha en la que se agrupan los usuarios. Por ejemplo, puede ser `User's first order date` o `User's registration date`.

>[!NOTE]
>
>No puede usar la misma fecha en la que se creó la métrica (ejemplo: `created at`) como el `cohort date`.

#### Configuración del intervalo y el periodo de tiempo

A continuación, configuramos la variable `Interval` y `Time Period`.

`Interval`
La variable `Interval` permite configurar la variable `length` de su `cohorts`. Por ejemplo, si se configura como `Month`, el informe se medirá en meses.

Puede cambiar la forma en que se muestran estos intervalos en el eje x utilizando la variable **Duración** para abrir el Navegador.

`Time Period`
Utilice la variable `Time Period` para elegir el usuario específico `cohorts` para analizar. Puede mostrar cada `cohort`, elija entre una lista, especifique un intervalo de tiempo o defina un intervalo de tiempo móvil de `cohorts` para incluir. Por ejemplo, si utilizamos la variable `Specific Cohorts` , podemos seleccionar meses específicos para incluirlos en el análisis:

![Al usar la variable `Time Period` para agregar `Cohorts`](../../assets/Cohort_Time_Period.gif)

Si estuviéramos agrupando nuestra `cohorts` por fecha de registro y, a continuación, seleccione abril, mayo y junio en la `Specific Cohorts` cualquier usuario que se haya registrado en esos meses será incluido.

#### Definición del eje X

En `duration`, puede definir la configuración del eje X del gráfico. Es decir, cuántos periodos de tiempo representa cada punto de datos y cuántos puntos de datos incluir en el análisis.

#### Al seleccionar la variable `counting members` tabla

Si optó por agrupar usuarios por un `cohort date` que se ha unido desde otra tabla, es posible que vea una `counting members in the … table` .

![](../../assets/Cohort_Counting_Members_option.png)

Veamos un ejemplo para comprender este ajuste. Supongamos que creó una cohorte de informes de `Revenue` métrica por `Customer's registration date`. También quería usar la perspectiva `Average value per cohort member` para ver los ingresos por comprador a lo largo del tiempo. Para encontrar el valor promedio por comprador, tenemos que decidir el número de compradores que dividir por. ¿Es el número de clientes registrados en su `customers` o es el número de compradores distintos en su `orders table` ¿durante el mismo período de tiempo?

Esta configuración responde a esa pregunta. Recuento de miembros en la variable `customers` incluye a todos los clientes (independientemente de que hayan realizado o no una compra) del promedio. Recuento de miembros en la variable `orders` solo incluye a los clientes que realizaron una compra.

#### Selección de una perspectiva {#perspective}

Una vez que haya definido la métrica y cómo desea analizarla, puede seleccionar la variable `perspective` desea utilizar.

Justo encima de la visualización del informe hay un menú desplegable de `perspective` configuración.

Consulte [Perspectivas](#perspectives).

![](../../assets/Cohort_Perspective_Menu.png)

## Ejemplos de análisis de cohorte {#examples}

Ahora que hemos pasado por cómo crear un `cohort` analicemos algunos ejemplos.

### Quiero saber cómo mi usuario `cohorts` están creciendo con el tiempo.

![Usuario `cohorts` con el tiempo](../../assets/cohort1.gif)

En este ejemplo, analizamos el `Revenue` , agrupa nuestras cohortes por el `customer's first order date`y seleccionó las 8 más recientes `cohorts` (definido en la variable `Time Period` ) para incluir en el análisis. Para ver cómo las cohortes crecieron con el tiempo, usamos la variable `Cumulative Average Value per Cohort Member` `perspective`.

### Quiero saber, en promedio, cuántos pedidos hace un usuario en diferentes momentos de su vida.

!![Average number of orders users make at different points in their lifetimes](../../assets/cohort2.gif)

Para este ejemplo, analizamos el `Number of orders` , agrupa nuestras cohortes por el `customer's first order date`, e incluye las 8 cohortes más recientes (definidas en la variable `Time Period` ) en el análisis. Para ver el número promedio de pedidos para cada cohorte, cambiamos el `perspective` a `Average Value per Cohort Member`.

### Quiero entender cómo se compara la futura actividad de compra de un usuario con la actividad de su primer mes con la del negocio.

![Comparación de la actividad de compra futura de un usuario con su primer mes de actividad](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
Esto muestra la contribución incremental de un grupo de cohortes determinado en cualquier punto de su ciclo de vida. (ejemplo: El punto &quot;Semana 6&quot; muestra todos los puntos de datos realizados por los usuarios en su sexta semana).

`Average Value per Cohort Member`
Esto divide el `Standard cohort` análisis en (1) por número de usuarios en cada `cohort` grupo. Esto puede resultar útil para comparar el rendimiento de una cohorte de manzanas a manzanas, ya que no todos los grupos de cohortes pueden incluir el mismo número de usuarios. Por ejemplo, la semana promedio 6 ingresos por usuario de un determinado `cohort`.

`Cumulative`
Esta `perspective` muestra la `cohort` análisis en un `cumulative` base. En otras palabras, muestra la contribución total de una cohorte determinada hasta la fecha en cualquier momento de su ciclo de vida. Por ejemplo, los ingresos acumulados después de 6 semanas de usuarios de una cohorte determinada.

`Cumulative Average Value per Cohort Member`
Esto divide el `Cumulative` análisis en (3) por número de usuarios en cada `cohort` grupo. Muestra la contribución promedio de duración (a menudo, el ingreso promedio de duración) por `cohort` miembro en cada período de la `cohort's` vida. Por ejemplo, el ingreso promedio de duración después de 6 meses de usuarios que se unieron en junio.

`Percent of First Value (show first value)`
Esto analiza el agregado `cohort` contribución en un momento específico `cohort's` ciclo de vida como porcentaje de su contribución en el primer período. Por ejemplo, los ingresos del mes 6 se dividieron entre los ingresos del mes 1 de los usuarios que se unieron en junio.

`Percent of First Value (hide first value)`
Es igual que la variable `perspective` arriba, excepto que el valor del primer periodo de tiempo del 100 % está oculto.

## Ajuste {#finish}

La variable `Cohort Report Builder` actualmente está optimizado para agrupar usuarios por un común `cohort date`. Puede que le interese agrupar a los usuarios por una actividad o atributo similar: si ese es el caso, nos encantaría ayudarle. Recomendamos que verifique [este tutorial sobre cohortes cualitativas](../dev-reports/create-qual-cohort-analysis.md) para empezar.
