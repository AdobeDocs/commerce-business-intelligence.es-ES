---
title: Restricción del acceso a la base de datos
description: Descubra cómo puede restringir el acceso y limitar el acceso al servidor que aloja la base de datos.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
role: Admin, User
feature: Accounts, User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Restringir el acceso

Cuando crea un túnel SSH al servidor, no es necesario que [!DNL Adobe Commerce Intelligence] tenga acceso a nada excepto a la base de datos. Si no desea que [!DNL Commerce Intelligence] tenga acceso total al servidor que aloja su base de datos, puede restringir el acceso forzando al usuario [!DNL Commerce Intelligence Linux] a un [shell de bash restringido](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

Puede que haya adivinado por el nombre, pero se usa un shell de bash restringido para configurar un entorno más controlado que el shell estándar. Lo importante de este tipo de shell es que los usuarios de shell restringidos no pueden acceder a las funciones del sistema ni realizar ningún tipo de modificación.

Para restringir el usuario [!DNL Commerce Intelligence Linux], debe hacer dos cosas:

1. Cambie la variable de entorno PATH para que sea la cadena vacía. Esto significa que el usuario no puede acceder a los ejecutables del sistema.

1. Asegúrese de que el shell ejecutado sea `bash -r`

Ambos se pueden realizar dentro del archivo `authorized_keys` en el directorio principal `dir/.ssh` del usuario como parte del comando que se ejecuta cuando el usuario inicia sesión. Tiene un aspecto similar al siguiente:

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

Cuando se complete esto, el usuario que creó para [!DNL Commerce Intelligence] no podrá realizar cambios en el sistema.
