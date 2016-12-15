---
title: "Procedura: Analizzare le stringhe con String.Split (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "separazione di stringhe [C#]"
  - "Split (metodo) [C#]"
  - "stringhe [C#], separazione"
  - "analizzare le stringhe"
ms.assetid: 729c2923-4169-41c6-9c90-ef176c1e2953
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: Analizzare le stringhe con String.Split (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'esempio di codice seguente mostra come analizzare una stringa con il metodo <xref:System.String.Split%2A?displayProperty=fullName>.<xref:System.String.Split%2A> accetta come input una matrice di caratteri che indica quali caratteri separano le sottostringhe rilevanti della stringa di destinazione.  La funzione restituisce una matrice di sottostringhe.  
  
 Questo esempio usa spazi, virgole, punti, due punti e tabulazioni, tutti passati in una matrice che contiene questi caratteri di separazione per <xref:System.String.Split%2A>.  Ogni parola nella frase della stringa di destinazione viene visualizzata separatamente rispetto alla matrice di stringhe risultante.  
  
## Esempio  
 [!code-cs[csProgGuideStrings#16](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-parse-strings-using-string-split_1.cs)]  
  
## Esempio  
 Per impostazione predefinita, String.Split restituisce stringhe vuote quando vengono visualizzati due caratteri di separazione adiacenti nella stringa di destinazione.  È possibile passare un parametro facoltativo StringSplitOptions.RemoveEmptyEntries per escludere le stringhe vuote nell'output.  
  
 String.Split può accettare una matrice di stringhe \(sequenze di caratteri, al posto di caratteri singoli, che fungono da separatori per l'analisi della stringa di destinazione\).  
  
```c#  
class TestStringSplit { static void Main() { char[] separatingChars = { "<<", "..." }; string text = "one<<two......three<four"; System.Console.WriteLine("Original text: '{0}'", text); string[] words = text.Split(separatingChars, System.StringSplitOptions.RemoveEmptyEntries ); System.Console.WriteLine("{0} substrings in text:", words.Length); foreach (string s in words) { System.Console.WriteLine(s); } // Keep the console window open in debug mode. System.Console.WriteLine("Press any key to exit."); System.Console.ReadKey(); } } /* Output: Original text: 'one<<two......three<four' 3 words in text: one two three<four */  
  
```  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Stringhe](../../../csharp/programming-guide/strings/index.md)   
 [Espressioni regolari di .NET Framework](../Topic/.NET%20Framework%20Regular%20Expressions.md)