---
title: Informazioni di riferimento di global.json | Microsoft Docs
description: Informazioni di riferimento di global.json
keywords: .NET, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 11/02/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 96102f96-d403-4385-8ef6-5d80e406eb0c
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: b814bfc79c2fcd0fd15b9494c18c6d0443a70fb1

---

# <a name="globaljson-reference-net-core-tools-rc4"></a>Informazioni di riferimento di global.json (strumenti di .NET Core RC4)

> [!WARNING]
> Questo argomento si applica agli strumenti di .NET Core RC4. Per gli strumenti dell'anteprima 2 di .NET Core, vedere l'argomento [Informazioni di riferimento di global.json](../../tools/global-json.md).

Il file global.json continua a essere presente nella versione RC4 della riga di comando di .NET Core. Tuttavia, lo scopo principale di tale file non è definire i metadati della soluzione come nelle versioni precedenti, ma consentire la selezione della versione dell'interfaccia della riga di comando usata tramite la proprietà `sdk`. 

Queste informazioni di riferimento si basano su quanto appena descritto. 

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


