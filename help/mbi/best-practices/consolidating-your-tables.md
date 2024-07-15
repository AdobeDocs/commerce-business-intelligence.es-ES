---
title: Consolidar las tablas
description: Aprenda a consolidar tablas y bases de datos.
exl-id: 6065bed3-fb84-4147-a223-92dc3e1b15a5
role: Admin, User
feature: Commerce Tables, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Consolidar las tablas

Si opera varios frentes de tiendas o en varios mercados, es posible que tenga bases de datos similares almacenadas por separado. En [!DNL Adobe Commerce Intelligence], es fácil consolidar juntas tablas similares de diferentes bases de datos.

Por ejemplo, puede tener una tabla `orders` para `Market A` y una tabla `orders` similar para `Market B`. [!DNL Commerce Intelligence] puede consolidar ambas tablas y permitirle ver los datos de pedidos agregados de `Market A` y `B`, además de segmentarlos por mercado específico.

Para que funcione la consolidación de tablas, las tablas de entrada deben estar **estructuradas de manera similar**. Es decir, todas las tablas de entrada deben contener las columnas de datos requeridas en la tabla consolidada.

En este tema se describen algunos de los casos de uso más comunes de las tablas consolidadas y los pasos siguientes necesarios para crear las suyas propias.

## Recommendations para saber cuándo usar tablas consolidadas

A continuación se explica cuándo puede ser apropiado utilizar tablas consolidadas en el sistema.

### Integración de datos de varios sitios web

Si vende sus productos bajo diferentes marcas y sitios web, es probable que las tablas para cada marca o sitio web tengan una estructura similar.

Por ejemplo, puede tener una tabla `orders` para el sitio web `A` y una tabla `orders` independiente, pero similar, para el sitio web `B`. En este caso, puede resultar útil consolidar las tablas `orders` del sitio web `A` y `B`. Esto le permite observar los ingresos consolidados y el número de pedidos del sitio web `A` y `B`, además de poder segmentar las métricas mediante estos dos sitios web.

### Integración de datos heredados

Muchas empresas han refactorizado sus bases de datos en un momento u otro, y los datos de la antigua base de datos no siempre se convierten al nuevo sistema. Puede utilizar tablas consolidadas para unir las columnas clave de tablas heredadas con las del sistema activo. Esto le permite realizar un análisis unificado de los datos a lo largo del historial.

### Combinación de eventos para el análisis activo del usuario

Imagine un sitio web en el que los usuarios puedan hacer varias cosas: realizar una encuesta, jugar un juego, realizar una compra, recomendar a un amigo, etc. Normalmente, cada uno de estos eventos se almacena en su propia tabla. Esto dificulta realizar un análisis de cuántos usuarios diferentes tomaron al menos una acción de cualquier tipo en un período de tiempo determinado.

Puede utilizar tablas consolidadas para crear una lista unificada de todos los usuarios y cuándo se produjo cualquiera de estos eventos. A continuación, puede ejecutar consultas en la tabla consolidada para realizar fácilmente dicho análisis.

Al igual que con todas las demás tablas de la Data Warehouse, puede agregar columnas adicionales para generar diferentes tipos de gráficos y análisis.

## Creación, Consulta o Actualización de una Tabla Consolidada

Si está interesado en agregar una tabla consolidada a su Data Warehouse, comuníquese con [!DNL Commerce Intelligence] [soporte técnico](../guide-overview.md#Submitting-a-Support-Ticket).

>[!NOTE]
>
>Dado que las tablas consolidadas no se pueden ver en `Data Warehouse Manager`, la visualización y actualización de estas tablas sólo se puede realizar mediante la compatibilidad con [!DNL Commerce Intelligence].
