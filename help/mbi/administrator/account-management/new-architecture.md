---
title: Nueva arquitectura
description: Conozca las ventajas de pasar a la nueva arquitectura.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Nueva arquitectura

Nuestros equipos de Productos e Ingeniería se han centrado en hacer las mejoras más amplias y altamente solicitadas posibles para el último año. Estamos encantados de anunciar la disponibilidad de un nuevo [!DNL MBI] arquitectura del producto que hace que estas mejoras sean una realidad.

## Ventajas de la nueva arquitectura

* Cree nuevos tipos de columnas en el almacén de datos, incluidas las columnas calculadas con SQL.
* Las columnas nuevas están disponibles inmediatamente.
* La latencia de los datos se mejora considerablemente.

## Ventajas técnicas

Las principales diferencias se enumeran más arriba, pero lo que técnicamente ha cambiado es la forma en que realizamos cálculos durante el ciclo de actualización. Los cálculos ya no se ejecutan en cada columna durante cada actualización; en su lugar, se ejecutan bajo demanda desde el Report Builder visual.

### Migración a la nueva arquitectura

Como las cuentas están construidas de forma diferente, no hay ningún proceso automático que podamos emplear para migrar el almacén de datos o los informes a una nueva cuenta de arquitectura, por lo que el paso a la nueva arquitectura requiere una reimplementación de la cuenta existente.

### Costo de transferencia a la nueva arquitectura

¡Sin costo adicional! Crearemos una nueva cuenta para que usted empiece a reimplementarse, lo que es gratuito durante al menos un mes. Esto le permite disponer de tiempo para que ambas cuentas estén abiertas, de modo que pueda realizar la reimplementación con mayor facilidad y garantizar que su equipo no tenga una brecha en el servicio.

### Tiempo necesario para volver a implementar la cuenta en la nueva arquitectura

Los tiempos de reimplementación varían según lo que desee reconstruir. Le recomendamos que realice los siguientes pasos en su cuenta existente para tener una idea de lo que podría implicar su reimplementación:

* Identificar un conjunto central de informes/tableros.
* Identifique las métricas y dimensiones necesarias para crear esos informes.
* Identifique las columnas necesarias para recrear esas métricas y dimensiones.

Cuando esto finalice, sabrá qué datos debe sincronizar con el nuevo almacén de datos de la arquitectura para reconstruir esos informes principales.

### Obtención de ayuda

La variable [!DNL MBI] El equipo de servicios puede realizar la reimplementación por un coste adicional. Póngase en contacto con [Equipo de éxito del cliente](../../guide-overview.md) y estar preparado para proporcionar una lista de tableros e informes que desea priorizar al crear en la nueva cuenta

### Mantener la arquitectura existente

Si estas funciones no son importantes para usted, puede seguir con su cuenta existente. No hay costo adicional para mantener su cuenta existente, y seguiremos apoyando esas cuentas sin cambios.
