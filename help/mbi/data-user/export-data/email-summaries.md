---
title: Crear resúmenes de correo electrónico automatizados
description: Obtenga información sobre cómo crear resúmenes de correo electrónico automatizados.
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: a65ededb203b7551fdfcb31cff130ef85b01fbe3
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# Crear resúmenes de correo electrónico automatizados

Los resúmenes de correo electrónico son una potente herramienta de comunicación que puede utilizar para compartir el estado y las tendencias de su negocio con las partes interesadas clave. Con los resúmenes de correo electrónico, puede:

* Resúmenes gráficos de correo electrónico que incluyen informes
* Incluir o excluir al autor del resumen del correo electrónico de la recepción del correo electrónico
* Programar cuando se envíe el correo electrónico
* Editar, eliminar y pausar resúmenes de correo electrónico programados existentes

## Crear nuevo resumen de correo electrónico

1. Haga clic en **[!DNL Manage Data]** y luego en **[!UICONTROL Email Summary]** en la barra lateral.

   Si es la primera vez que crea un resumen de correo electrónico, esta página no muestra ningún resumen guardado.

1. Haga clic en **[!UICONTROL Create New Email Summary]**, en la esquina superior derecha.

1. Introduzca un nombre para el resumen.

   Elija un nombre que transmita lo que se incluye en el resumen. Por ejemplo, `AOV Comparison`.

1. En la sección `Choose Content`, seleccione los informes que desee incluir en el resumen.

   Tiene dos opciones para agregar contenido:

   * **Seleccionar informes individuales** - Elegir informes específicos de sus paneles
   * **Seleccionar todo el panel**: incluya todos los informes de un panel tal y como aparecen en el diseño del panel

   Puede seleccionar hasta diez informes de su propiedad. Después de seleccionar un informe, utilice los iconos que aparecen para seleccionar si desea que ese informe se envíe como una tabla o un gráfico. Si ha guardado el informe como un número, solo puede enviarlo como un número. Para obtener información sobre cómo enviar un resumen de correo electrónico que contenga un informe con datos antiguos, consulte [Administrar la configuración de la cuenta](../../administrator/account-management/managing-account-settings.md).

   Para agregar paneles completos, tiene las siguientes opciones de formato y eliminación:

   * Cambiar el formato del informe a un gráfico o una tabla
   * Eliminar informes para que no se incluyan en el correo electrónico
   * Seleccione esta opción para incluir un archivo CSV para informes tabulares: esto permite a los destinatarios acceder a datos sin procesar y exportables directamente desde su bandeja de entrada.

   >[!NOTE]
   >
   >Los informes de `Cohort` solo están disponibles si utiliza la nueva arquitectura.

   >[!NOTE]
   >
   >Los archivos adjuntos CSV grandes son compatibles con un total combinado de 25 MB por correo electrónico.

1. (Opcional) Seleccione `Send Email To Me` si desea recibir el correo electrónico.

1. Para incluir a otros usuarios en el correo electrónico, escriba sus direcciones de correo electrónico en el campo `Add Email Recipients` separadas por comas, espacios, tabulaciones o punto y coma.

## Programar resumen de correo electrónico

En el campo `Set when to send the Email Summary`, puede especificar cuándo enviar los resúmenes de correo electrónico. Las opciones son:

* `Manual`
* `Once`
* `Repeating`

### Guardar resumen de correo electrónico para enviarlo más tarde

1. Seleccione `Manual` del campo `Set when to send the Email Summary`.

1. Haga clic en **[!UICONTROL Save]**.

   Esto guarda el resumen en la lista de resúmenes de correo electrónico.

1. Cuando esté listo para enviar el resumen, haga clic en el icono de engranaje y seleccione `Send Now`.

### Enviar resumen por correo electrónico una vez

1. Seleccione `Once` del campo `Set when to send the Email Summary`.

1. Especifique la fecha de inicio en el calendario `Select Start Date`.

1. Especifique la hora a la que enviar el correo electrónico en el campo `Select time to send`.

### Crear programación repetida

1. Seleccione `Repeating` del campo `Set when to send the Email Summary`.

1. En el campo `Set Frequency`, seleccione `Daily`, `Weekly` o `Monthly`.

1. Especifique la fecha de inicio en el calendario `Select Start Date`.

1. Especifique la hora a la que enviar el correo electrónico en el campo `Select time to send`.

1. (Opcional) Para especificar una fecha de finalización, seleccione `End Date` y seleccione la fecha de finalización en el calendario.

## Modificar resumen de correo electrónico existente

Después de crear y guardar un resumen de correo electrónico, la página `Email Summaries` muestra una lista de todos los resúmenes guardados. Puede expandir (`+`) en cada fila para obtener más información. Las columnas de esta vista son las siguientes:

* `Email Name` - Nombre del resumen del correo electrónico
* `Content`: tipo de contenido dentro del resumen, como los nombres de cualquier informe
* `Scheduled` - Frecuencia, fecha y hora en que se envía el resumen de correo electrónico
* `Recipients` - Destinatarios del resumen del correo electrónico
* `Created Date` - Fecha en que se creó el resumen de correo electrónico
* `Status` - `Paused` o `Active`

>[!NOTE]
>
>Para obtener información sobre cómo enviar un resumen de correo electrónico que contenga un informe con datos antiguos, consulte [Administrar la configuración de la cuenta](../../administrator/account-management/managing-account-settings.md).

Haga clic en el icono de engranaje a la derecha de cada fila para:

* `Send Now` - Enviar el resumen de correo electrónico inmediatamente a todos los destinatarios especificados
* `Edit` - Modificar los detalles del resumen del correo electrónico
* `Pause/Active` - Pausar o activar el envío de resumen de correo electrónico
* `Delete` - Eliminar el resumen del correo electrónico
