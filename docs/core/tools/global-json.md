---
title: Informazioni di riferimento di global.json | Microsoft Docs
description: Informazioni di riferimento di global.json
keywords: .NET, .NET Core
author: aL3891
ms.author: mairaw
ms.date: 11/02/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: e1ac9659-425f-4486-a376-c12ca942ead8
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: a6b0ad546a8a121ad5ea4642c11842a8dccf7055

---

# <a name="globaljson-reference"></a>Informazioni di riferimento di global.json

> [!WARNING]
> Questo argomento si applica agli strumenti dell'anteprima 2 di .NET Core. Per gli strumenti di .NET Core versione RC4, vedere l'argomento [Informazioni di riferimento di global.json (strumenti di .NET Core RC4)](../preview3/tools/global-json.md).

Il file global.json viene usato in progetti .NET Core per definire i metadati della soluzione. Questo file viene usato quando il comando [dotnet-restore](dotnet-restore.md) viene richiamato per ripristinare le dipendenze di un progetto .NET Core.
In questo argomento di riferimento verrà presentato l'elenco delle proprietà che è possibile definire nel file global.json.

## <a name="projects"></a>progetti
Tipo: String[]

Specifica le cartelle in cui il sistema di compilazione deve cercare i progetti durante la risoluzione delle dipendenze. Il sistema di compilazione eseguirà solo la ricerca delle cartelle figlio di livello più alto.

Ad esempio:

```json
{
    "projects": [ "src", "test" ]
}
```

## <a name="packages"></a>pacchetti
Tipo: String

Il percorso per archiviare i pacchetti.

Ad esempio:
```json
{
    "packages": "packages-dir"
}
```

## <a name="sdk"></a>SDK
Tipo: Object

Specifica le informazioni sull'SDK.

### <a name="version"></a>version
Tipo: String

La versione dell'SDK da usare.

Ad esempio:

```json
{
    "sdk": {
        "version": "1.0.0-preview2-003121"
    }
}
```



<!--HONumber=Feb17_HO2-->


