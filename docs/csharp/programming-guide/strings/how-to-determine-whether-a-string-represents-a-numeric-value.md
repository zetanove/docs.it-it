---
title: "Procedura: determinare se una stringa rappresenta un valore numerico (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "stringhe numeriche [C#]"
  - "stringhe [C#], numeriche"
  - "convalida dell'input numerico [C#]"
ms.assetid: a4e84e10-ea0a-489f-a868-503dded9d85f
caps.latest.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 9
---
# Procedura: determinare se una stringa rappresenta un valore numerico (Guida per programmatori C#)
Per determinare se una stringa è una rappresentazione valida di un tipo numerico specificato, utilizzare il metodo `TryParse` statico implementato da tutti i tipi numerici primitivi e anche da tipi come <xref:System.DateTime> e <xref:System.Net.IPAddress>.  Nell'esempio seguente viene illustrato come determinare se "108" è un [int](../../../csharp/language-reference/keywords/int.md) valido.  
  
```  
int i = 0;   
string s = "108";  
bool result = int.TryParse(s, out i); //i now = 108  
```  
  
 Se la stringa contiene caratteri non numerici o il valore numerico è troppo grande o troppo piccolo per il particolare tipo specificato, `TryParse` restituisce false e imposta il parametro out su zero.  In caso contrario, restituisce true e imposta il parametro out sul valore numerico della stringa.  
  
> [!NOTE]
>  Una stringa può contenere solo caratteri numerici e tuttavia non essere valida per il tipo di cui si utilizza il metodo `TryParse`.  Ad esempio, "256" non è un valore valido per `byte`, ma è valido per `int`.    98,6" non è un valore valido per `int`, ma è valido per `decimal`.  
  
## Esempio  
 Negli esempi seguenti è illustrato come utilizzare `TryParse` con rappresentazioni di stringa di valori `long`, `byte` e `decimal`.  
  
 [!code-cs[csProgGuideStrings#14](../../../csharp/programming-guide/strings/codesnippet/csharp/CSRefStrings/Strings.cs#14)]  
  
## Programmazione efficiente  
 I tipi numerici primitivi implementano anche il metodo statico `Parse`, che genera un'eccezione se la stringa non è un numero valido.  `TryParse` è in genere più efficace poiché restituisce semplicemente false se il numero non è valido.  
  
## Sicurezza di .NET Framework  
 Utilizzare sempre i metodi `TryParse` o `Parse` per convalidare l'input dell'utente da controlli quali caselle di testo e caselle combinate.  
  
## Vedere anche  
 [Procedura: convertire una matrice di byte in un Integer](../../../csharp/programming-guide/types/how-to-convert-a-byte-array-to-an-int.md)   
 [Procedura: convertire una stringa in un numero](../../../csharp/programming-guide/types/how-to-convert-a-string-to-a-number.md)   
 [Procedura: eseguire la conversione tra stringhe esadecimali e tipi numerici](../../../csharp/programming-guide/types/how-to-convert-between-hexadecimal-strings-and-numeric-types.md)   
 [Analisi di stringhe numeriche](../Topic/Parsing%20Numeric%20Strings%20in%20the%20.NET%20Framework.md)   
 [Formattazione di tipi](../Topic/Formatting%20Types%20in%20the%20.NET%20Framework.md)