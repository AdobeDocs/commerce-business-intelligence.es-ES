---
source-git-commit: aa7acd0d863a3cd48ff83675b72c2a96eae02b4d
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---
# Documentación técnica de Adobe Commerce Intelligence

Agradecemos las contribuciones de la comunidad, así como de los empleados de Adobe ajenos a los equipos de documentación.

## Código de conducta de Adobe Open Source

Este proyecto ha adoptado el [Código de conducta de Adobe Open Source](code-of-conduct.md) o el Código de conducta de [.NET Foundation](https://dotnetfoundation.org/code-of-conduct). Para obtener más información, consulte el artículo [Contribución](contributing.md).

## Acerca de sus contribuciones al contenido de Adobe

Consulte la [Guía del colaborador de Adobe Docs](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html).

La forma en que contribuya depende de quién sea y del tipo de cambios con los que desee contribuir:

### Cambios menores

Si va a contribuir con actualizaciones menores, visite el artículo y haga clic en el área de comentarios que aparece en la parte inferior del artículo, haga clic en **Opciones de comentarios detalladas** y, a continuación, haga clic en **Sugerir una edición** para ir al archivo de código fuente Markdown en GitHub. Utilice la interfaz de usuario de GitHub para realizar las actualizaciones. Para obtener más información, consulte la [guía para colaboradores de Adobe Docs](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html).

Las correcciones o aclaraciones menores que envíe para la documentación y los ejemplos de código en este repositorio están sujetos a las condiciones de uso de Adobe.

### Cambios importantes o nuevos artículos de los miembros de la comunidad

Si forma parte de la comunidad de Adobe y desea crear un nuevo artículo o enviar cambios importantes, utilice la pestaña Problemas del repositorio Git para enviar un problema e iniciar una conversación con el equipo de documentación. Una vez que haya acordado un plan, deberá trabajar con un empleado para ayudar a incorporar ese nuevo contenido a través de una combinación de trabajo en los repositorios públicos y privados.

### Cambios importantes de los empleados de Adobe

Si es redactor técnico, administrador de programa o desarrollador del equipo de producto para una solución de Adobe Experience Cloud y su trabajo consiste en contribuir a artículos técnicos o crearlos, debe utilizar el repositorio privado en GHEC.

## Herramientas y configuración

Los colaboradores de la comunidad pueden utilizar la interfaz de usuario de GitHub para la edición básica o bifurcar el repositorio para realizar contribuciones importantes.

Consulte la [Guía para colaboradores de Adobe Docs](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html) para obtener más información.

## Utilizar Markdown para dar formato al tema

Todos los artículos de este repositorio utilizan GitHub Flavored Markdown. Si no está familiarizado con el uso de markdown, consulte:

- [Guía de sintaxis de Markdown](https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntax)
- [Hoja de pruebas de sintaxis de Markdown](https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/cheatsheet)

## Enlaces previos a la confirmación para la optimización de imágenes

Este repositorio incluye enlaces automatizados previos a la confirmación que optimizan las imágenes antes de la confirmación. **Todos los colaboradores deben habilitar estos vínculos** para garantizar una optimización de imagen coherente y una reducción del tamaño del repositorio.

### Configuración rápida

Después de clonar el repositorio, ejecute:

```bash
.githooks/setup-hooks.sh
```

### Qué hacen los ganchos

- Detectar automáticamente archivos de imagen clasificados (`.png`, `.jpeg`, `.jpg`, `.gif`, `.svg`)
- Ejecute `image_optim` para comprimir y optimizar las imágenes rasterizadas (`.png`, `.jpeg`, `.jpg`, `.gif`)
- Volver a almacenar automáticamente las imágenes optimizadas
- Asegúrese de que todas las imágenes rasterizadas confirmadas estén optimizadas correctamente
- Comprobar los SVG clasificados con un límite de tamaño y anular la confirmación si se hace referencia a un SVG de gran tamaño desde `help/` (de lo contrario, advertir)

### Ventajas

- Tamaño de repositorio reducido
- Cargas de página más rápidas para la documentación
- Calidad de imagen coherente en todos los colaboradores
- No se requiere optimización manual

Para obtener instrucciones de instalación, solución de problemas y configuración detalladas, consulte [`.githooks/README.md`](.githooks/README.md).

## Guía de creación de Experience League

### Primeros pasos

- [Información general sobre la introducción](https://experienceleague.adobe.com/en/docs/authoring-guide/using/getting-started/getting-started)
- [Configuración de Git](https://experienceleague.adobe.com/en/docs/authoring-guide/using/setup/tools/git-setup)
- [Aspectos básicos de la documentación de Git y GitHub](https://experienceleague.adobe.com/en/docs/authoring-guide/using/setup/tools/git-fundamentals)
- [Vídeos de inicio rápido](https://experienceleague.adobe.com/en/docs/authoring-guide/using/getting-started/quick-start-guides/quick-start-overview)

### Flujos de trabajo

- [Flujo de trabajo para colaboradores poco frecuentes](https://experienceleague.adobe.com/en/docs/authoring-guide/using/editing/git-workflow-infrequent-user)
- [Solicitudes de extracción de GitHub](https://experienceleague.adobe.com/en/docs/authoring-guide/using/editing/public-github)

### Creación

- [Prácticas recomendadas de creación](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/authoring-best-practices)
- [Guía de sintaxis de Markdown](https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntax)
- [Hoja de pruebas de sintaxis de Markdown](https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/cheatsheet)
- [Uso de tablas](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/tables)
- [Adición de vínculos](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/linking)
- [Mover y reestructurar contenido](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/restructure-new)
