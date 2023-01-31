---
title: Modelado de datos MongoDB
description: Aprenda a evitar patrones de datos que planteen un problema.
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# [!DNL MongoDB] Modelado de datos

When [!DNL MBI] extrae [!DNL MongoDB] , esos datos se traducen en un modelo relacional.

Las malas noticias: Aunque la mayoría de los patrones de datos no plantean un problema, hay algunos que, debido a la traducción a un modelo relacional, [!DNL MBI] no es compatible.

La buena noticia: Se pueden evitar todos estos patrones.

## Matrices subanidadas {#subnested}

Si la colección tiene el aspecto siguiente, [!DNL MBI] solo replicará los datos en la matriz de elementos. No se extraerán datos de la matriz de subelementos.

```bash
    {
        _id: 0000000000000001
        items: [
            {
                _id: 0000000000000002
               subItems: [
                   {
                       _id: 0000000000000003
                      name: "Donut"
                      description: "glazed"
                   }
               ]
            }
        ]
    }
```

## Claves de objeto de variable {#varobjectkeys}

Las colecciones que incluyen objetos con claves de objeto de variable no se replican en [!DNL MBI]. Por ejemplo:

```bash
    {
        _id: 0000000000000001
        friends: {
            0000000000000002: "Jimmy",
            0000000000000004: "Roger",
            0000000000000005: "Susan"
        },
    }
```

Esto suele ocurrir cuando se utiliza un objeto y una matriz sería más adecuada. Ahora, retrabajaremos el ejemplo anterior:

```bash
    {
        _id: 0000000000000001
        friends: [
            { friend_id: 0000000000000002, name: "Jimmy" },
            { friend_id: 0000000000000004, name: "Roger" },
            { friend_id: 0000000000000005, name: "Susan"}
        ]
    }
```
