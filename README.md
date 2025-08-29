---
source-git-commit: 6233779ba2e2a99ed229f8aa97497eb8d9d877f7
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 5%

---
# Documentación técnica de Adobe Commerce Intelligence

Agradecemos las contribuciones de la comunidad, así como de los empleados de Adobe ajenos a los equipos de documentación.

## Código de conducta de Adobe Open Source

Este proyecto ha adoptado el [Código de conducta de código abierto de Adobe](code-of-conduct.md) o el [Código de conducta de la Fundación .NET](https://dotnetfoundation.org/code-of-conduct). Para obtener más información, consulte el artículo [Colaboración](contributing.md).

## Acerca de sus contribuciones al contenido de Adobe

Consulte la [Guía del colaborador de Adobe Docs](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=es).

La forma en que contribuya depende de quién sea y del tipo de cambios con los que desee contribuir:

### Cambios menores

Si va a contribuir con actualizaciones menores, visite el artículo y haga clic en el área de comentarios que aparece en la parte inferior del artículo, haga clic en **Opciones de comentarios detalladas** y, a continuación, haga clic en **Sugerir una edición** para ir al archivo de código fuente Markdown en GitHub. Utilice la interfaz de usuario de GitHub para realizar las actualizaciones. Para obtener más información, consulte la [guía para colaboradores de Adobe Docs](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=es).

Las correcciones o aclaraciones menores que envíe para la documentación y los ejemplos de código en este repositorio están sujetos a las condiciones de uso de Adobe.

### Cambios importantes o nuevos artículos de los miembros de la comunidad

Si forma parte de la comunidad de Adobe y desea crear un nuevo artículo o enviar cambios importantes, utilice la pestaña Problemas del repositorio Git para enviar un problema e iniciar una conversación con el equipo de documentación. Una vez que haya acordado un plan, deberá trabajar con un empleado para ayudar a incorporar ese nuevo contenido a través de una combinación de trabajo en los repositorios públicos y privados.

### Cambios importantes de los empleados de Adobe

Si es redactor técnico, administrador de programa o desarrollador del equipo de producto para una solución de Adobe Experience Cloud y debe contribuir o crear artículos técnicos, debe utilizar el repositorio privado en `https://git.corp.adobe.com/AdobeDocs`.

## Herramientas y configuración

Los colaboradores de la comunidad pueden utilizar la interfaz de usuario de GitHub para la edición básica o bifurcar el repositorio para realizar contribuciones importantes.

Consulte la [Guía para colaboradores de Adobe Docs](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=es) para obtener más información.

## Utilizar Markdown para dar formato al tema

Todos los artículos de este repositorio utilizan GitHub Flavored Markdown. Si no está familiarizado con el uso de markdown, consulte:

- [Conceptos básicos de Markdown](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)
- [Hoja de trucos de markdown imprimible](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)

## Enlaces previos a la confirmación para la optimización de imágenes

Este repositorio incluye enlaces automatizados previos a la confirmación que optimizan las imágenes antes de la confirmación. **Todos los colaboradores deben habilitar estos vínculos** para garantizar una optimización de imagen coherente y una reducción del tamaño del repositorio.

### Configuración rápida

Después de clonar el repositorio, ejecute:

```bash
.githooks/setup-hooks.sh
```

### Qué hacen los ganchos

- Detectar automáticamente archivos de imagen clasificados (PNG, JPG, JPEG, GIF, SVG)
- Ejecutar `image_optim` para comprimir y optimizar imágenes
- Volver a almacenar automáticamente las imágenes optimizadas
- Asegúrese de que todas las imágenes confirmadas estén optimizadas correctamente

### Ventajas

- Tamaño de repositorio reducido
- Cargas de página más rápidas para la documentación
- Calidad de imagen coherente en todos los colaboradores
- No se requiere optimización manual

Para obtener instrucciones de instalación, solución de problemas y configuración detalladas, consulte [`.githooks/README.md`](.githooks/README.md).
