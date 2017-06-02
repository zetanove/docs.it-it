---
title: "Procedura: Rimuovere caratteri non validi da una stringa | Microsoft Docs"
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
  - "espressioni regolari, esempi"
  - "pulitura input"
  - "input utente, esempi"
  - "espressioni regolari di .NET Framework, esempi"
  - "espressioni regolari [.NET Framework], esempi"
  - "Regex.Replace (metodo)"
  - "rimozione dei caratteri non validi"
  - "Replace (metodo)"
  - "convalida dell'input utente"
ms.assetid: b4319c8a-9032-4129-a9d5-6f6fc28e7f32
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: Rimuovere caratteri non validi da una stringa
Nell'esempio seguente viene utilizzato il metodo statico <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=fullName> per eliminare i caratteri non validi da una stringa.  
  
## Esempio  
 È possibile utilizzare il metodo `CleanInput` definito in questo esempio per rimuovere i caratteri potenzialmente dannosi immessi in un campo di testo che accetta input dell'utente.  In questo caso, `CleanInput` rimuove tutti i caratteri non alfanumerici eccetto i punti \(.\), i simboli della chiocciola \(@\) e i trattini \(\-\) e restituisce la stringa restante.  Tuttavia, è possibile modificare il modello di espressione regolare in modo da rimuovere tutti i caratteri che non devono essere inclusi in una stringa di input.  
  
 [!code-csharp[RegularExpressions.Examples.StripChars#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.StripChars/cs/Example.cs#1)]
 [!code-vb[RegularExpressions.Examples.StripChars#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.StripChars/vb/Example.vb#1)]  
  
 Il modello di espressione regolare `[^\w\.@-]` corrisponde a qualsiasi carattere che non sia un carattere alfanumerico, un punto, un simbolo @ o un trattino.  Un carattere alfanumerico è una lettera, una cifra decimale o un connettore di punteggiatura quale il carattere di sottolineatura.  Qualsiasi carattere corrispondente a questo modello viene sostituito da <xref:System.String.Empty?displayProperty=fullName>, vale a dire la stringa definita dal modello di sostituzione.  Per consentire ulteriori caratteri nell'input dell'utente, aggiungere tali caratteri alla classe di caratteri nel modello di espressione regolare.  Ad esempio, il modello di espressione regolare `[^\w\.@-\\%]` consente inoltre un simbolo di percentuale e una barra rovesciata in una stringa di input.  
  
## Vedere anche  
 [Espressioni regolari di .NET Framework](../../../docs/standard/base-types/regular-expressions.md)