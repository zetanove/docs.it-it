---
title: Informazioni di riferimento di global.json | .NET Core
description: Informazioni di riferimento di global.json
keywords: .NET, .NET Core
author: aL3891
ms.author: mairaw
manager: wpickett
ms.date: 11/02/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: e1ac9659-425f-4486-a376-c12ca942ead8
translationtype: Human Translation
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: 281f1b717a0e220e533078e973711977617a1401

---

# <a name="globaljson-reference"></a>Informazioni di riferimento di global.json

Il file global.json continua a essere presente nell'anteprima 3 della riga di comando di .NET Core. Tuttavia, lo scopo principale di tale file non è definire i metadati della soluzione come nelle versioni precedenti, ma consentire la selezione della versione dell'interfaccia della riga di comando usata tramite la proprietà `sdk`. 

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



<!--HONumber=Nov16_HO3-->


