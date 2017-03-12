---
title: "Procedura: Eseguire la ricerca di stringhe tramite espressioni regolari (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "ricerca di stringhe [C#]"
  - "stringhe [C#], ricerca con RegEx"
ms.assetid: dcab2150-a4a2-4fe4-87e3-83b83b58d84a
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# Procedura: Eseguire la ricerca di stringhe tramite espressioni regolari (Guida per programmatori C#)
La classe <xref:System.Text.RegularExpressions.Regex?displayProperty=fullName> può essere utilizzata per eseguire la ricerca di stringhe.  Queste ricerche possono essere molto semplici oppure basate sull'uso delle espressioni regolari.  Di seguito sono riportati due esempi di ricerca di stringhe tramite la classe <xref:System.Text.RegularExpressions.Regex>.  Per ulteriori informazioni, vedere [Espressioni regolari di .NET Framework](../Topic/.NET%20Framework%20Regular%20Expressions.md).  
  
## Esempio  
 Il codice riportato di seguito rappresenta un'applicazione console che esegue una semplice ricerca di stringhe in una matrice, senza distinzione tra maiuscole e minuscole.  Il metodo statico <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=fullName> esegue la ricerca date la stringa da cercare e una stringa contenente il modello di ricerca.  In questo caso, viene utilizzato un terzo argomento per indicare che le lettere maiuscole\/minuscole devono essere ignorate.  Per ulteriori informazioni, vedere <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>.  
  
 [!code-cs[csProgGuideStrings#17](../../../csharp/programming-guide/strings/codesnippet/csharp/CSRefStrings/Strings.cs#17)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrata un'applicazione console che usa espressioni regolari per convalidare il formato di tutte le stringhe in una matrice.  Per la convalida è necessario che tutte le stringhe assumano il formato di un numero di telefono costituito da tre gruppi di cifre separate da trattini, in cui i primi due gruppi contengono tre cifre e il terzo ne contiene quattro.  Questa operazione viene eseguita usando l'espressione regolare `^\\d{3}-\\d{3}-\\d{4}$`.  Per ulteriori informazioni, vedere [Linguaggio di espressioni regolari \- Riferimento rapido](../Topic/Regular%20Expression%20Language%20-%20Quick%20Reference.md).  
  
 [!code-cs[csProgGuideStrings#18](../../../csharp/programming-guide/strings/codesnippet/csharp/CSRefStrings/Strings.cs#18)]  
  
## Vedere anche  
 <xref:System.Text.RegularExpressions.Regex?displayProperty=fullName>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Stringhe](../../../csharp/programming-guide/strings/index.md)   
 [Espressioni regolari di .NET Framework](../Topic/.NET%20Framework%20Regular%20Expressions.md)   
 [Linguaggio di espressioni regolari \- Riferimento rapido](../Topic/Regular%20Expression%20Language%20-%20Quick%20Reference.md)