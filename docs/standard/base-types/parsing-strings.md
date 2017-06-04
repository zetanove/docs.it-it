---
title: "Analisi di stringhe in .NET Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "analisi di stringhe, informazioni"
  - "IFormatProvider (interfaccia), analisi di stringhe"
  - "tipi di base, analisi di stringhe"
  - "Parse (metodo)"
  - "analisi di stringhe"
ms.assetid: 5e758b41-db93-456b-8999-99b7304b090d
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Analisi di stringhe in .NET Framework
Un'operazione di analisi converte una stringa che rappresenta un tipo di base .NET Framework in tale tipo di base.  Un'operazione di analisi viene utilizzata, ad esempio, per convertire una stringa in un numero a virgola mobile o in un valore di data e ora.  Il metodo utilizzato più di frequente per eseguire un'operazione di analisi è il metodo `Parse`.  Poiché l'analisi è l'operazione inversa alla formattazione, che consiste nel convertire un tipo di base nella relativa rappresentazione di stringa, trovano in essa applicazione molte delle stesse regole e convenzioni.  Come nella formattazione viene utilizzato un oggetto che implementa l'interfaccia <xref:System.IFormatProvider> per fornire le informazioni di formattazione dipendenti dalle impostazioni cultura, anche nell'analisi viene utilizzato un oggetto che implementa l'interfaccia <xref:System.IFormatProvider> per determinare come interpretare una rappresentazione di stringa.  Per ulteriori informazioni, vedere [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md).  
  
## In questa sezione  
 [Analisi di stringhe numeriche](../../../docs/standard/base-types/parsing-numeric.md)  
 Viene descritta la conversione delle stringhe nei tipi numerici .NET Framework.  
  
 [Analisi delle stringhe di data e ora](../../../docs/standard/base-types/parsing-datetime.md)  
 Viene descritta la conversione delle stringhe nei tipi **DateTime** di .NET Framework.  
  
 [Analisi di altre stringhe](../../../docs/standard/base-types/parsing-other.md)  
 Viene descritta la conversione delle stringhe nei tipi **Char**, **Boolean** e **Enum**.  
  
## Sezioni correlate  
 [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md)  
 Vengono descritti i concetti di base sulla formattazione, quali gli identificatori e i provider di formato.  
  
 [Conversione di tipi in .NET Framework](../../../docs/standard/base-types/type-conversion.md)  
 Viene descritto come convertire i tipi.  
  
 [Tipi di base](../../../docs/standard/base-types/index.md)  
 Vengono descritte le operazioni comuni che è possibile eseguire sui tipi di base di .NET Framework.