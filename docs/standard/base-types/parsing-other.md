---
title: "Analisi di altre stringhe in .NET Framework | Microsoft Docs"
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
  - "tipo di dati Char, analisi di stringhe"
  - "enumerazioni [.NET Framework], analisi di stringhe"
  - "tipi di base, analisi di stringhe"
  - "analisi di stringhe, altre stringhe"
  - "tipo di dati booleano, analisi di stringhe"
ms.assetid: d139bc00-3c4e-4d78-ac9a-5c951b258d28
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Analisi di altre stringhe in .NET Framework
Oltre alle stringhe numeriche e a quelle <xref:System.DateTime>, è possibile analizzare le stringhe che rappresentano i tipi <xref:System.Char>, <xref:System.Boolean> e <xref:System.Enum>.  
  
## Char  
 Il metodo statico Parse associato al tipo di dati **Char** risulta utile per la conversione di una stringa formata da un singolo carattere nel valore Unicode corrispondente.  Nell'esempio seguente viene illustrata la conversione di una stringa in un carattere Unicode.  
  
 [!code-cpp[Conceptual.String.Parse#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.parse/cpp/parse.cpp#2)]
 [!code-csharp[Conceptual.String.Parse#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.parse/cs/parse.cs#2)]
 [!code-vb[Conceptual.String.Parse#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.parse/vb/parse.vb#2)]  
  
## Boolean  
 Nel tipo di dati **Boolean** è disponibile un metodo **Parse** che consente di convertire una stringa che rappresenta un valore Boolean in un tipo **Boolean** effettivo.  Questo metodo non fa distinzione tra maiuscole e minuscole e consente di analizzare correttamente un stringa contenente un valore "True" o "False." Il metodo **Parse** associato al tipo **Boolean** consente inoltre di analizzare stringhe precedute e seguite da spazi.  Se viene passata qualsiasi altra stringa, viene generata un'eccezione <xref:System.FormatException>.  
  
 Nell'esempio riportato di seguito viene utilizzato il metodo **Parse** per convertire una stringa in un valore Boolean.  
  
 [!code-cpp[Conceptual.String.Parse#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.parse/cpp/parse.cpp#3)]
 [!code-csharp[Conceptual.String.Parse#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.parse/cs/parse.cs#3)]
 [!code-vb[Conceptual.String.Parse#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.parse/vb/parse.vb#3)]  
  
## Enumerazione  
 È possibile utilizzare il metodo **Parse** statico per inizializzare un tipo di enumerazione sul valore di una stringa.  Questo metodo accetta il tipo di enumerazione che si sta analizzando, la stringa da analizzare e un flag Boolean facoltativo che indica se viene fatta distinzione tra maiuscole e minuscole.  La stringa che si analizza può contenere più valori separati da virgole che possono essere preceduti o seguiti da uno o più spazi.  Quando la stringa contiene più valori, il valore dell'oggetto restituito corrisponde a tutti i valori specificati combinati mediante un'operazione OR bit per bit.  
  
 Nell'esempio riportato di seguito viene utilizzato il metodo **Parse** per convertire una rappresentazione di stringa in un valore di enumerazione.  L'enumerazione <xref:System.DayOfWeek> viene inizializzata su **Thursday** da una stringa.  
  
 [!code-cpp[Conceptual.String.Parse#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.parse/cpp/parse.cpp#4)]
 [!code-csharp[Conceptual.String.Parse#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.parse/cs/parse.cs#4)]
 [!code-vb[Conceptual.String.Parse#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.parse/vb/parse.vb#4)]  
  
## Vedere anche  
 [Analisi di stringhe](../../../docs/standard/base-types/parsing-strings.md)   
 [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md)   
 [Conversione di tipi in .NET Framework](../../../docs/standard/base-types/type-conversion.md)