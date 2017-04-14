---
title: "Esempio di espressione regolare: modifica dei formati di data | Microsoft Docs"
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
  - "ricerca con espressioni regolari, esempi"
  - "analisi di testo con espressioni regolari, esempi"
  - "espressioni regolari, esempi"
  - "espressioni regolari di .NET Framework, esempi"
  - "espressioni regolari [.NET Framework], esempi"
  - "corrispondenza al modello con espressioni regolari, esempi"
ms.assetid: 5fcc75a5-09d7-45ae-a4c0-9ad6085ac83d
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# Esempio di espressione regolare: modifica dei formati di data
Nell'esempio di codice seguente viene utilizzato il metodo <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=fullName> per sostituire le date nel formato *mm*\/*dd*\/*yy* con date nel formato *dd*\-*mm*\-*yy*.  
  
## Esempio  
 [!code-csharp[RegularExpressions.Examples.ChangeDateFormats#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/cs/Example_ChangeDateFormats1.cs#1)]
 [!code-vb[RegularExpressions.Examples.ChangeDateFormats#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/vb/Example_ChangeDateFormats1.vb#1)]  
  
 Nel codice riportato di seguito viene mostrato come il metodo `MDYToDMY` può essere chiamato in un'applicazione.  
  
 [!code-csharp[RegularExpressions.Examples.ChangeDateFormats#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/cs/Example_ChangeDateFormats1.cs#2)]
 [!code-vb[RegularExpressions.Examples.ChangeDateFormats#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/vb/Example_ChangeDateFormats1.vb#2)]  
  
## Commenti  
 Il modello di espressione regolare `\b(?<month>\d{1,2})/(?<day>\d{1,2})/(?<year>\d{2,4})\b` viene interpretato come illustrato nella tabella seguente.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`\b`|Inizia la corrispondenza sul confine di parola.|  
|`(?<month>\d{1,2})`|Corrisponde a una o due cifre decimali.  Equivale al gruppo acquisito `month`.|  
|`/`|Corrisponde alla barra.|  
|`(?<day>\d{1,2})`|Corrisponde a una o due cifre decimali.  Equivale al gruppo acquisito `day`.|  
|`/`|Corrisponde alla barra.|  
|`(?<year>\d{2,4})`|Trova la corrispondenza con 2\-4 cifre decimali.  Equivale al gruppo acquisito `year`.|  
|`\b`|Termina la corrispondenza sul confine di parola.|  
  
 Il modello `${day}-${month}-${year}` definisce la stringa di sostituzione come illustrato nella tabella seguente.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`$(day)`|Aggiunge la stringa acquisita dal gruppo di acquisizione `day`.|  
|`-`|Aggiunge un trattino.|  
|`$(month)`|Aggiunge la stringa acquisita dal gruppo di acquisizione `month`.|  
|`-`|Aggiunge un trattino.|  
|`$(year)`|Aggiunge la stringa acquisita dal gruppo di acquisizione `year`.|  
  
## Vedere anche  
 [Espressioni regolari di .NET Framework](../../../docs/standard/base-types/regular-expressions.md)