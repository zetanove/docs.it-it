---
title: Informazioni di riferimento di global.json | Microsoft Docs
description: Informazioni di riferimento di global.json
keywords: .NET, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 04/05/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 96102f96-d403-4385-8ef6-5d80e406eb0c
ms.translationtype: Human Translation
ms.sourcegitcommit: ec7028d43e7236056e5a53160f6017edadfec8c2
ms.openlocfilehash: a35938d355cb86205e9c822736862298508cf861
ms.contentlocale: it-it
ms.lasthandoff: 04/06/2017

---

# <a name="globaljson-reference"></a>Informazioni di riferimento di global.json

Il file *global.json* consente di selezionare la versione degli strumenti di .NET Core usata nella proprietà `sdk`.

Gli strumenti CLI di .NET Core cercano questo file nella directory di lavoro corrente (che non corrisponde necessariamente alla directory del progetto) o in una delle directory padre.

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

