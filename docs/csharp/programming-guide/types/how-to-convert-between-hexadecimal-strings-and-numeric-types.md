---
title: "Procedura: eseguire la conversione tra stringhe esadecimali e tipi numerici (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "conversioni [C#], stringhe esadecimali"
  - "stringhe esadecimali [C#]"
  - "stringhe esadecimali [C#], conversione a tipi numerici"
  - "stringhe [C#], conversione di stringhe esadecimali"
ms.assetid: 7115c49f-7d1d-40c3-8bd9-aae0cc1d46b6
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# Procedura: eseguire la conversione tra stringhe esadecimali e tipi numerici (Guida per programmatori C#)
In questi esempi viene mostrato come effettuare le seguenti attività:  
  
-   Ottenere il valore esadecimale di ogni carattere in un oggetto [string](../../../csharp/language-reference/keywords/string.md).  
  
-   Ottenere l'oggetto [char](../../../csharp/language-reference/keywords/char.md) che corrisponde a ogni valore in una stringa esadecimale.  
  
-   Convertire un oggetto `string` esadecimale in un oggetto [int](../../../csharp/language-reference/keywords/int.md).  
  
-   Convertire un oggetto `string` esadecimale in un oggetto [float](../../../csharp/language-reference/keywords/float.md).  
  
-   Convertire una matrice di [byte](../../../csharp/language-reference/keywords/byte.md) in un oggetto `string` esadecimale.  
  
## Esempio  
 In questo esempio viene restituito il valore esadecimale di ogni carattere in un oggetto `string`.  Viene innanzitutto analizzato l'oggetto `string` in una matrice di caratteri.  Viene quindi chiamato il metodo <xref:System.Convert.ToInt32%28System.Char%29> su ogni carattere per ottenere il valore numerico.  Infine, il numero viene formattato come rappresentazione esadecimale in un oggetto `string`.  
  
 [!code-cs[csProgGuideTypes#30](../../../csharp/programming-guide/nullable-types/codesnippet/csharp/how-to-convert-between-h_1.cs)]  
  
## Esempio  
 In questo esempio viene analizzato un oggetto `string` di valori esadecimali e viene restituito il carattere corrispondente a ogni valore esadecimale.  Viene innanzitutto chiamato il metodo [Split\(Char\<xref:System.String.Split%28System.Char%5B%5D%29> per ottenere ogni valore esadecimale come singolo oggetto `string` in una matrice.  Viene quindi chiamato il metodo <xref:System.Convert.ToInt32%28System.String%2CSystem.Int32%29> per convertire il valore esadecimale in un valore decimale rappresentato come [int](../../../csharp/language-reference/keywords/int.md).  Vengono illustrate due modalità diverse per ottenere il carattere corrispondente al codice di tale carattere.  La prima tecnica utilizza <xref:System.Char.ConvertFromUtf32%28System.Int32%29>, che restituisce il carattere corrispondente all'argomento integer come `string`.  La seconda tecnica esegue il cast in modo esplicito del valore `int` in un valore [char](../../../csharp/language-reference/keywords/char.md).  
  
 [!code-cs[csProgGuideTypes#31](../../../csharp/programming-guide/nullable-types/codesnippet/csharp/how-to-convert-between-h_2.cs)]  
  
## Esempio  
 In questo esempio viene illustrato un modo alternativo per convertire un oggetto `string` esadecimale in un intero, chiamando il metodo <xref:System.Int32.Parse%28System.String%2CSystem.Globalization.NumberStyles%29>.  
  
 [!code-cs[csProgGuideTypes#32](../../../csharp/programming-guide/nullable-types/codesnippet/csharp/how-to-convert-between-h_3.cs)]  
  
## Esempio  
 Nell'esempio seguente viene mostrato come convertire un oggetto `string` esadecimale in un oggetto [float](../../../csharp/language-reference/keywords/float.md) tramite la classe <xref:System.BitConverter?displayProperty=fullName> e il metodo <xref:System.Int32.Parse%2A?displayProperty=fullName>.  
  
 [!code-cs[csProgGuideTypes#39](../../../csharp/programming-guide/nullable-types/codesnippet/csharp/how-to-convert-between-h_4.cs)]  
  
## Esempio  
 Nell'esempio seguente viene mostrato come convertire una matrice di [byte](../../../csharp/language-reference/keywords/byte.md) in una stringa esadecimale tramite la classe <xref:System.BitConverter?displayProperty=fullName>.  
  
 [!code-cs[csProgGuideTypes#38](../../../csharp/programming-guide/nullable-types/codesnippet/csharp/how-to-convert-between-h_5.cs)]  
  
## Vedere anche  
 [Stringhe di formato numerico standard](../Topic/Standard%20Numeric%20Format%20Strings.md)   
 [Tipi](../../../csharp/programming-guide/types/index.md)   
 [Procedura: determinare se una stringa rappresenta un valore numerico](../../../csharp/programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)