---
title: Consolidar las tablas
description: Aprenda a consolidar las tablas y las bases de datos.
exl-id: 6065bed3-fb84-4147-a223-92dc3e1b15a5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Consolidar las tablas

Si opera varias facetas de almacenamiento o en varios mercados, es posible que tenga bases de datos similares almacenadas por separado. En [!DNL MBI], es fácil consolidar tablas similares de diferentes bases de datos juntas.

Por ejemplo, puede tener un `orders` tabla para `Market A`y similar `orders` tabla para `Market B`. [!DNL MBI] puede consolidar ambas tablas y permitir ver los datos de pedidos acumulados desde `Market A` y `B`, además de segmentarlo por mercado específico.

Para que las tablas funcionen, las tablas de entrada deben **estructura similar**. En otras palabras, todas las tablas de entrada deben contener las columnas de datos requeridas en la tabla consolidada.

En este tema se tratan algunos de los casos de uso más comunes de las tablas consolidadas y los siguientes pasos necesarios para crear las suyas.

## Recommendations para saber cuándo utilizar las tablas consolidadas

A continuación se indica cuándo puede ser apropiado utilizar tablas consolidadas en el sistema.

### Integración de datos de varios sitios web

Si vende sus productos en diferentes marcas y sitios web, es probable que las tablas de cada marca o sitio web estén estructuradas de manera similar.

Por ejemplo, puede tener un `orders` tabla para el sitio web `A` y una independiente, pero similar, `orders` tabla para el sitio web `B`. En esta situación, puede resultar útil consolidar el `orders` tablas del sitio web `A` y `B` para poder consultar los ingresos consolidados y el número de pedidos del sitio web `A` y `B`, además de poder segmentar métricas por estos dos sitios web.

### Integración de datos heredados

Muchas empresas han refactorizado sus bases de datos de una u otra vez, y los datos de la antigua base de datos no siempre se convierten al nuevo sistema. Puede utilizar tablas consolidadas para unir las columnas clave de tablas heredadas con las del sistema activo. Esto le permite realizar un análisis unificado de los datos a lo largo del historial.

### Combinación de eventos para el análisis activo del usuario

Imagine un sitio web en el que los usuarios pueden hacer varias cosas: realice una encuesta, juegue un juego, realice una compra, consulte a un amigo, etc. Normalmente, cada uno de estos eventos se almacena en su propia tabla. Esto hace que sea difícil realizar un análisis de cuántos usuarios distintos realizaron al menos una acción de cualquier tipo en un período de tiempo determinado.

Puede utilizar tablas consolidadas para crear una lista unificada de todos los usuarios y cuándo se produjo cualquiera de estos eventos. A continuación, puede ejecutar consultas en la tabla consolidada para realizar fácilmente un análisis de este tipo.

Al igual que con las demás tablas del almacén de datos, puede agregar columnas adicionales para potenciar distintos tipos de gráficos y análisis.

## Creación, visualización o actualización de una tabla consolidada

Si le interesa agregar una tabla consolidada al almacén de datos, póngase en contacto con [!DNL MBI] [support](../guide-overview.md).

>[!NOTE]
>
>Debido a que las tablas consolidadas no se pueden ver en la variable `Data Warehouse Manager`, la visualización y actualización de estas tablas solo se pueden realizar mediante [!DNL MBI] asistencia técnica.
