---
title: Optimización de la base de datos para análisis
description: Aprenda a optimizar la base de datos para su análisis.
exl-id: e73e1a1e-c933-476d-97bc-bd8f52bb2fa1
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---

# Optimizar la base de datos

La principal ventaja de utilizar una base de datos operativa para inteligencia empresarial es que no es necesario crear ni modificar nada para recopilar datos. Ya se dispone de información valiosa; todo lo que debe hacer es desbloquearlo.

Este tema contiene algunas recomendaciones para ayudarle a optimizar la base de datos para su análisis y extraer perspectivas procesables a partir de los datos sin procesar.

## No eliminar datos

>[!TIP]
>
>Las leyes locales e internacionales que afectan a su negocio (y a sus propios términos de servicio) pueden afectar a los tipos de datos que puede conservar y por cuánto tiempo puede conservarlos. El cumplimiento de estas leyes debería ser su primera prioridad.

Cuando se cancela un pedido, un usuario desactiva su cuenta o se interrumpe el tratamiento de un producto, resulta tentador eliminar la información asociada de la base de datos. Las tablas crecen y eliminar el desorden parece una idea prudente. Sin embargo, la eliminación de filas significa que esta información se pierde para siempre o que tendrá que escarbar en las copias de seguridad antiguas para encontrarla.

En su lugar, puede agregar una columna de estado a la tabla que indicará cuándo la fila ya no está activa ni es relevante. También se recomienda añadir una columna que almacene la fecha en la que se realizó el cambio o crear un registro para los cambios históricos. Si las tablas crecen lo suficiente como para que el rendimiento empiece a verse afectado, considere archivar los datos antiguos en una tabla utilizada para el análisis.

## Sobrescribir datos con poca frecuencia

La sobrescritura de datos debe hacerse con moderación y precaución.

Si utilizamos las fechas de inicio de sesión como ejemplo, muchas empresas almacenarán la fecha del último inicio de sesión en lugar de una tabla de inicios de sesión históricos. Aunque es posible que solo necesite la fecha del último inicio de sesión para fines funcionales, los datos sobrescritos supone una gran pérdida desde el punto de vista analítico. Al no mantener un registro completo de estas acciones, se elimina la posibilidad de ver cuántos usuarios permanecieron fuera durante largos períodos de tiempo y luego se reactivaron. También hace que sea imposible crear elementos como análisis de cohorte de participación del usuario basados en inicios de sesión.

Como regla general, si está actualizando un registro debido a algún tipo de acción del usuario, no sobrescriba la información sobre una acción anterior o independiente del usuario.

## Incluir `Updated_at` Columnas de datos actualizados con el tiempo

Si las filas de una tabla tienen valores que cambian con el tiempo, por ejemplo, **order\_status** cambia de`processing` a `complete`, incluya un **actualizado\_at** para registrar cuándo se produce el último cambio. Asegúrese de que **actualizado\_at** está disponible cuando se inserta por primera vez la nueva fila de datos, en cuyo momento la variable **actualizado\_at** date corresponde a la **created\_at** fecha.

Además de optimizar para análisis, **actualizado\_at** también le permiten utilizar [Métodos de replicación incremental](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md), lo que puede ayudarle a reducir la duración de los ciclos de actualización.

## Fuente de adquisición de usuario de tienda

Uno de los errores más comunes es el [fuente de adquisición de usuario](../data-analyst/analysis/google-track-user-acq.md) (UAS) no almacenado en la base de datos operativa. En la mayoría de las situaciones en las que esto es un problema, solo se está realizando un seguimiento de los UAS [!DNL Google Analytics] o alguna otra herramienta de análisis web. Si bien estas herramientas pueden ser extremadamente valiosas, existen algunos inconvenientes para almacenar UAS exclusivamente en ellas; por ejemplo, no puede extraer datos de nivel de usuario de estas herramientas. Cuando es posible, suele ser un proceso difícil. Debe ser fácil obtener esta información y asociarla con datos de otras fuentes, como la información de comportamiento y transaccional también almacenada en la base de datos.

Almacenar UAS en su propia base de datos es a menudo la mayor mejora que una empresa en línea puede hacer a sus capacidades analíticas. Esto permite el análisis de ventas, participación del usuario, periodos de devolución, valor de duración del cliente, pérdida y otras métricas críticas por parte de UAS. [Estos datos son cruciales para decidir dónde invertir los recursos de marketing](../data-analyst/analysis/most-value-source-channel.md).

Demasiadas empresas se centran únicamente en encontrar canales que proporcionen nuevos usuarios al menor costo, pero si no rastrea la calidad de los usuarios adquiridos en cada canal, corre el riesgo de atraer usuarios que no generan valor comercial.

## Configuración de tabla de datos

### Establecer una clave principal

A [clave principal](http://en.wikipedia.org/wiki/Unique_key) es una columna (o conjunto de columnas) que produce valores únicos dentro de una tabla. Las claves principales son increíblemente importantes, ya que garantizan que las tablas se replicen correctamente en [!DNL MBI].

Al crear claves principales, utilice un tipo de datos entero para la columna que aumenta automáticamente. También se recomienda evitar el uso de claves principales de varias columnas siempre que sea posible.

Si la tabla es una vista SQL, agregue una columna que pueda actuar como clave principal. [!DNL MBI] podrá identificar automáticamente esta columna como clave principal.

### Asignar un tipo de datos a la columna de datos

Si una columna de datos no tiene una asignación [tipo de datos](http://en.wikipedia.org/wiki/Data_type), [!DNL MBI] adivinará qué tipo de datos usar. Si el sistema adivina incorrectamente, es posible que no pueda realizar los análisis relevantes hasta que nuestro equipo de asistencia ajuste la columna al tipo de datos correcto. Por ejemplo, si una columna de fecha se calcula como un tipo de datos numérico, puede analizar la tendencia a lo largo del tiempo mediante esa dimensión de fecha.

### Añadir Prefijos a las tablas de datos si tiene varias bases de datos

Si tiene más de una base de datos conectada a [!DNL MBI], recomendamos añadir prefijos a las tablas para evitar confusiones. Los prefijo le ayudarán a recordar de dónde provienen las métricas o las dimensiones de datos.
