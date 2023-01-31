---
title: Tableros incluidos
description: Aprenda a comprobar el estado de las métricas esenciales, como los ingresos acumulados por el usuario, el número de compras repetidas y más, creando así una base sólida para la exploración futura.
exl-id: f50fc417-e5d4-401c-9baa-cda1468196a2
source-git-commit: 3557e6370fae637cd74550b2806847bebe61d5d3
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 0%

---

# Tableros incluidos

Como parte de nuestros servicios, ofrecemos comercio electrónico y `SaaS` Paquetes iniciales. Estos paquetes, creados por nuestros analistas, contienen un conjunto personalizado de paneles e informes para su conjunto de datos. Los análisis contenidos en estos paquetes permiten comprobar el estado de las métricas esenciales, como los ingresos acumulados por el usuario, el número de compras repetidas y más, lo que crea una base sólida para la exploración futura.

>[!NOTE]
>
>La disponibilidad de algunos tableros depende del conjunto de datos.

Si tiene alguna pregunta o está interesado en agregar un paquete a su cuenta, envíe un [ticket de asistencia](../../guide-overview.md) para obtener ayuda.

## Información general sobre el ejecutivo

La variable `executive overview` tablero se crea a partir de gráficos que existen en otros tableros. Este tablero es una descripción general de alto nivel de sus datos y contiene gráficos que se revisarían diariamente, mientras que otros tableros contenían información más detallada. Inicialmente, se establece como panel predeterminado en cada cuenta.

Aunque hemos incluido un conjunto general de gráficos para usted, le recomendamos que adapte este tablero a sus necesidades agregando otros gráficos que utilice con más frecuencia.

## Análisis de cohorte

La variable `cohort analysis` tablero incluye un conjunto de gráficos que muestran el crecimiento promedio de ingresos de por vida del usuario y el crecimiento incremental de ingresos agrupados por cohortes de registro. Esto revela si el valor de vida del cliente (LTV), el valor de un cliente para una empresa, aumenta con el tiempo y también identifica tendencias en el crecimiento de LTV. Tenga en cuenta que de forma predeterminada, *estamos contabilizando a todos los usuarios registrados (compradores y no compradores)* en el cálculo promedio de LTV (consulte la [tema de análisis de cohorte](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Este tablero también puede incluir gráficos de cohorte que analizan los ingresos de por vida de los usuarios a partir de una fuente de adquisición, canal o demografía específicos (por ejemplo, Nueva York o California). Esto es para demostrar cómo puede analizar LTV para segmentos muy específicos de su base de usuarios y ver si un grupo u otro produce más LTV a lo largo del tiempo.

Para obtener más información sobre las cohortes, consulte [Realización de análisis de cohorte](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Si actualmente no realiza el seguimiento de la fuente de adquisición de usuario, consulte la [Información general sobre el seguimiento de fuentes de adquisición de usuarios](../../data-analyst/analysis/google-track-user-acq.md).

## Resumen de correo electrónico

La variable `Email Summary` tablero incluye un conjunto de gráficos de muestra que se pueden utilizar en un resumen diario automatizado por correo electrónico. Consulte [creación de resúmenes de correo electrónico automatizados](../../data-user/export-data/email-summaries.md) para obtener más información sobre la configuración de los resúmenes de correo electrónico.  

## Mantenimiento de la retención

La variable `Retention health` tablero revela el comportamiento de compra repetido de la base de usuarios.

La variable `Time between orders` el gráfico muestra el tiempo promedio y/o medio transcurrido entre el primer y el segundo orden, el segundo y el tercer orden de un usuario, etc. Puede [considere la posibilidad de utilizar estos datos para configurar sus campañas de marketing por correo electrónico](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/).

La variable `Users by lifetime number of orders` gráfico enumera el número total de usuarios para cada número de pedidos acumulado para proporcionar una visión general del comportamiento de compra repetido.  

La variable `Repeat order probability` muestra la probabilidad de que un usuario con un determinado número de pedido repita una compra. Para ver la probabilidad de los clientes que `x` pedidos para realizar `(x+1)` órdenes, simplemente divida el número de personas que han hecho al menos `(x+1)` compras por número de personas que han realizado al menos `x` compras.

### Ejemplo

Número de clientes que han realizado una compra durante su vida útil: `90`

Número de clientes que han realizado dos compras durante su vida útil: `30`

Número de clientes que han realizado tres compras durante su vida útil: `10`

En este ejemplo, la probabilidad de pedidos repetidos de los clientes que han realizado una compra durante su vida útil para realizar una segunda compra es: `(30 + 10) / (30+10+90) = 30.77%`.

## Crecimiento de LTV para clientes

La variable `Customer LTV growth` tablero incluye un conjunto de gráficos que encuentra el ingreso promedio por usuario. Los gráficos se segmentan en función de los ingresos promedio que se generan durante los primeros 30, 60, 90 o 365 días después del registro.  

La fila inferior de gráficos muestra estos promedios segmentados por fuentes de adquisición o demografía para revelar qué grupos de usuarios generan la mayor cantidad de ingresos con el tiempo.

## Rendimiento del producto

La variable `Product Performance` el tablero incluye gráficos que revelan el rendimiento general del producto al mostrar el número de artículos vendidos y los ingresos por artículo, así como la identificación de los productos de mayor rendimiento.

## Actividad reciente

La variable `Recent Activity` tablero muestra los datos de rendimiento de los últimos 30 días.

## Salud transaccional

La variable `Transaction Health` tablero incluye gráficos generales de ingresos, pedidos y valor de pedido promedio. Estos gráficos pueden segmentarse por canales de marketing, demografía o códigos de cupones especiales.

## Usuarios a quienes dirigirse

La variable `Users to target` tablero incluye gráficos de estilo de tabla que enumeran usuarios con comportamientos de compra específicos en común. Algunos ejemplos son:

* Lista de compradores únicos que compran `X` hace meses (que puede que desee reactivar)

* Lista de gastadores principales (a los que puede que desee seguir contentos)

* Lista de los principales gastadores que estuvieron activos en el pasado `X` días (a los que quizá quiera recompensar)

Con nuestras herramientas de exportación de datos, es fácil [crear listas de correo electrónico de usuarios con un comportamiento de compra similar para el marketing de destino](http://blog.rjmetrics.com/creating-contact-lists-for-top-customers/).

## Actividad del usuario

La variable `User activity` tablero incluye gráficos que segmentan a los usuarios según una variedad de datos, incluyendo la fuente de adquisición, la información demográfica y el promedio de la primera vez que se realiza el pedido. También incluye el análisis de cohorte de usuarios, incluido el promedio general de ingresos por vida por mes de registro de los usuarios.

La variable `% of cohort members who have purchased` es especialmente valioso, ya que muestra la proporción de conversión (entre 0 y 1) de usuarios en función del momento en el que se registran (cada línea representa una cohorte de usuarios) y el momento en el que realizan la primera compra (por ejemplo, en el mes 1, 2, 3... después del registro). Esto puede mostrarle que el 10% de los usuarios se activaron en el mes 1, mientras que este número crece en el mes 2, 3, 4... y puede que se estabilice más adelante.

Normalmente, las líneas de este gráfico se vuelven horizontales después de un periodo de tiempo, lo que indica que pocos miembros de cohorte adicionales se están convirtiendo orgánicamente después de ese punto (es decir, la mayoría de los usuarios que van a realizar una compra ya lo han hecho). En este punto, es muy poco probable que estos miembros se conviertan a compradores sin intervención. [Llegar a ellos con promociones personalizadas o correos electrónicos con objetivos específicos es una forma extremadamente de bajo riesgo de impulsar la conversión de esta población.](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/)
