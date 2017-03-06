---
title: Analisi di stringhe in .NET
description: Analisi di stringhe in .NET
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/22/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 8103c0a6-61d3-40dd-a3e9-2a32ba6a4c05
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: c741ae793d491f691a355df6ad064b81d609c7e5
ms.lasthandoff: 03/03/2017

---

# <a name="parsing-strings-in-net"></a>Analisi di stringhe in .NET

Un'operazione di analisi converte una stringa che rappresenta un tipo di base .NET in quel tipo di base. Ad esempio, un'operazione di analisi viene usata per convertire una stringa in un numero a virgola mobile o in un valore di data e ora. Il metodo più comunemente usato per eseguire un'operazione di analisi è il metodo `Parse`. Poiché l'analisi è l'operazione inversa della formattazione (che comporta la conversione di un tipo di base nella relativa rappresentazione di stringa), vengono applicate molte delle stesse regole e convenzioni. Se la formattazione usa un oggetto che implementa l'interfaccia [IFormatProvider](xref:System.IFormatProvider) per visualizzare informazioni di formattazione dipendenti dalle impostazioni cultura, l'analisi usa anche un oggetto che implementa l'interfaccia [IFormatProvider](xref:System.IFormatProvider) per stabilire come interpretare una rappresentazione di stringa. Per altre informazioni, vedere [Formattazione di tipi in .NET](formatting-types.md).

## <a name="in-this-section"></a>Contenuto della sezione

[Analisi di stringhe numeriche in .NET](parsing-numeric.md): viene descritto come convertire le stringhe in tipi numerici di .NET.

[Analisi di stringhe di data e ora in .NET](parsing-datetime.md): viene descritto come convertire le stringhe in tipi `DateTime` di .NET.

[Analisi di altre stringhe in .NET](parsing-other.md): viene descritto come convertire le stringhe nei tipi [Char](xref:System.Char), [Boolean](xref:System.Boolean) ed [Enum](xref:System.Enum).

[Formattazione di tipi in .NET](formatting-types.md): descrive i concetti di formattazione di base, come identificatori di formato e provider di formato.

[Conversione di tipi in .NET](type-conversion.md): viene descritta la procedura di conversione dei tipi.

[Uso dei tipi di base in .NET](index.md): descrive le operazioni comuni che è possibile eseguire sui tipi di base di .NET.


