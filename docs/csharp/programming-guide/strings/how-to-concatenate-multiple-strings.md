---
title: "Procedura: concatenare pi&#249; stringhe (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "concatenazione di stringhe [C#]"
  - "unione di stringhe [C#]"
  - "stringhe [C#], concatenazione"
ms.assetid: 8e16736f-4096-4f3f-be0f-9d4c3ff63520
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# Procedura: concatenare pi&#249; stringhe (Guida per programmatori C#)
La *concatenazione* è il processo di aggiunta di una stringa alla fine di un'altra stringa.  Quando si concatenano valori letterali stringa o costanti di tipo stringa tramite l'operatore `+`, il compilatore crea una singola stringa.  Non si verifica alcuna concatenazione in fase di esecuzione.  Tuttavia, le variabili di tipo stringa possono essere concatenate solo in fase di esecuzione.  In questo caso, è necessario capire gli effetti dei vari approcci sulle prestazioni.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come suddividere un lungo valore letterale stringa in stringhe più piccole, per migliorare la leggibilità nel codice sorgente.  Queste parti verranno concatenate in una singola stringa in fase di compilazione.  Non vi è alcun impatto sulle prestazioni in fase di esecuzione indipendentemente dal numero di stringhe coinvolte.  
  
 [!code-cs[csProgGuideStrings#30](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-concatenate-multiple-strings_1.cs)]  
  
## Esempio  
 Per concatenare variabili di tipo stringa, è possibile utilizzare gli operatori `+` o `+=` o i metodi <xref:System.String.Concat%2A?displayProperty=fullName>, <xref:System.String.Format%2A?displayProperty=fullName> o <xref:System.Text.StringBuilder.Append%2A?displayProperty=fullName>.  L'operatore `+` è facile da utilizzare e rende il codice intuitivo.  Anche se si utilizzano vari operatori \+ in un'istruzione, il contenuto della stringa viene copiato solo una volta.  Ma se questa operazione viene ripetuta più volte, ad esempio in un ciclo, potrebbe causare problemi di efficienza.  Notare, ad esempio, il codice seguente:  
  
 [!code-cs[csProgGuideStrings#23](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-concatenate-multiple-strings_2.cs)]  
  
> [!NOTE]
>  Nelle operazioni di concatenazione di stringhe il compilatore C\# tratta una stringa null come se fosse una stringa vuota, ma non converte il valore della stringa null originale.  
  
 Se non si deve concatenare un elevato numero di stringhe \(ad esempio, in un ciclo\), il costo in termini di prestazioni di questo codice è probabilmente poco rilevante.  La stessa considerazione vale anche per i metodi <xref:System.String.Concat%2A?displayProperty=fullName> e <xref:System.String.Format%2A?displayProperty=fullName>.  
  
 Tuttavia, quando le prestazioni sono importanti, è sempre opportuno utilizzare la classe <xref:System.Text.StringBuilder> per concatenare stringhe.  Nell'esempio di codice riportato di seguito viene utilizzato il metodo <xref:System.Text.StringBuilder.Append%2A> della classe <xref:System.Text.StringBuilder> per concatenare le stringhe senza l'effetto di concatenazione dell'operatore `+`.  
  
 [!code-cs[csProgGuideStrings#22](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-concatenate-multiple-strings_3.cs)]  
  
## Vedere anche  
 <xref:System.String>   
 <xref:System.Text.StringBuilder>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Stringhe](../../../csharp/programming-guide/strings/index.md)