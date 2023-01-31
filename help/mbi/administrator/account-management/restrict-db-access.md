---
title: Restricción del acceso a la base de datos
description: Descubra cómo puede restringir el acceso, limitando el acceso al servidor que aloja la base de datos.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# Restringir acceso

Cuando creamos un túnel SSH en su servidor, no hay necesidad de [!DNL MBI] para tener acceso a cualquier cosa que no sea la base de datos. Si no desea [!DNL MBI] para tener acceso completo al servidor que aloja su base de datos, puede restringir el acceso forzando el [!DNL MBI Linux] en un [shell bash restringido](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

Puede que haya adivinado por el nombre, pero se usa un shell de bash restringido para configurar un entorno más controlado que el shell estándar. Lo importante de este tipo de shell es que los usuarios de shell restringidos no pueden acceder a las funciones del sistema ni realizar ningún tipo de modificaciones.

Para restringir el [!DNL MBI Linux] usuario, debe hacer dos cosas:

1. Cambie la variable de entorno PATH para que sea la cadena vacía. Esto significa que el usuario no podrá acceder a los ejecutables del sistema.

1. Asegúrese de que el shell ejecutado es `bash -r`

Ambos se pueden hacer dentro de la `authorized_keys` en la página principal del usuario `dir/.ssh` como parte del comando que se ejecuta cuando el usuario inicia sesión. Se parecerá a esto:

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

Una vez completada, el usuario creado para [!DNL MBI] no podrá realizar ningún cambio en su sistema.
