---
title: Restricción del acceso a la base de datos
description: Descubra cómo puede restringir el acceso y limitar el acceso al servidor que aloja la base de datos.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Restringir el acceso

Cuando crea un túnel SSH a su servidor, no es necesario [!DNL MBI] para tener acceso a cualquier cosa excepto a la base de datos. Si no lo desea [!DNL MBI] para tener acceso completo al servidor que aloja la base de datos, puede restringir el acceso forzando el [!DNL MBI Linux®] usuario en un [bash shell restringido](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

Puede que haya adivinado por el nombre, pero se usa un shell de bash restringido para configurar un entorno más controlado que el shell estándar. Lo importante de este tipo de shell es que los usuarios de shell restringidos no pueden acceder a las funciones del sistema ni realizar ningún tipo de modificación.

Para restringir el [!DNL MBI Linux®] usuario, debe hacer dos cosas:

1. Cambie la variable de entorno PATH para que sea la cadena vacía. Esto significa que el usuario no puede acceder a los ejecutables del sistema.

1. Asegúrese de que el shell ejecutado sea `bash -r`

Ambos se pueden realizar dentro del `authorized_keys` archivo en el inicio del usuario `dir/.ssh` como parte del comando que se ejecuta cuando el usuario inicia sesión. Tiene un aspecto similar al siguiente:

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

Una vez finalizado, el usuario que ha creado para [!DNL MBI] no puede realizar cambios en el sistema.
