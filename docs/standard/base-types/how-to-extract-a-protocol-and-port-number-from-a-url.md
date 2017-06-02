---
title: "Procedura: Estrarre un protocollo e un numero di porta da un URL | Microsoft Docs"
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
  - "espressioni regolari di .NET Framework, esempi"
  - "analisi di testo con espressioni regolari, esempi"
  - "corrispondenza al modello con espressioni regolari, esempi"
  - "espressioni regolari [.NET Framework], esempi"
  - "espressioni regolari, esempi"
  - "ricerca con espressioni regolari, esempi"
ms.assetid: ab7f62b3-6d2c-4efb-8ac6-28600df5fd5c
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: Estrarre un protocollo e un numero di porta da un URL
Nell'esempio seguente vengono estratti un protocollo e un numero di porta da un URL.  
  
## Esempio  
 Nell'esempio viene utilizzato il metodo <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=fullName> per restituire il protocollo seguito da due punti seguiti dal numero di porta.  
  
 [!code-csharp[RegularExpressions.Examples.Protocol#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/cs/Example.cs#1)]
 [!code-vb[RegularExpressions.Examples.Protocol#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/vb/Example.vb#1)]  
  
 Il modello di espressione regolare `^(?<proto>\w+)://[^/]+?(?<port>:\d+)?/` può essere interpretato come illustrato nella tabella seguente.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`^`|Iniziare la ricerca della corrispondenza all'inizio della stringa.|  
|`(?<proto>\w+)`|Trova la corrispondenza di uno o più caratteri alfanumerici.  Assegnare al gruppo il nome `proto`.|  
|`://`|Trovare la corrispondenza di due punti seguiti da due barre.|  
|`[^/]+?`|Trovare la corrispondenza di una o più occorrenze \(ma il minor numero possibile\) di qualsiasi carattere diverso da una barra.|  
|`(?<port>:\d+)?`|Trovare la corrispondenza di zero o una occorrenza di due punti seguiti da una o più cifre.  Assegnare al gruppo il nome `port`.|  
|`/`|Trovare la corrispondenza di una barra.|  
  
 Il metodo <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=fullName> espande la sequenza di sostituzione `${proto}${port}` che concatena il valore dei due gruppi denominati acquisiti nel modello di espressione regolare.  Si tratta di una comoda alternativa alla concatenazione esplicita delle stringhe recuperate dall'oggetto Collection restituito dalla proprietà <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=fullName>.  
  
 Nell'esempio viene utilizzato il metodo <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=fullName> con due sostituzioni, `${proto}` e `${port}`, per includere i gruppi acquisiti nella stringa di output.  È possibile invece recuperare i gruppi acquisiti dall'oggetto <xref:System.Text.RegularExpressions.GroupCollection> della corrispondenza, come viene illustrato dal codice seguente.  
  
 [!code-csharp[RegularExpressions.Examples.Protocol#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/cs/example2.cs#2)]
 [!code-vb[RegularExpressions.Examples.Protocol#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.Protocol/vb/example2.vb#2)]  
  
## Vedere anche  
 [Espressioni regolari di .NET Framework](../../../docs/standard/base-types/regular-expressions.md)