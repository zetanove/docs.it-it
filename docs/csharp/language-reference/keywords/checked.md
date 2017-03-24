---
title: "checked (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "checked_CSharpKeyword"
  - "checked"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "checked (parola chiave) [C#]"
ms.assetid: 718a1194-988d-48a3-b089-d6ee8bd1608d
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# checked (Riferimenti per C#)
La parola chiave `checked` viene utilizzata per abilitare in modo esplicito il controllo dell'overflow nelle conversioni e nelle operazioni aritmetiche di tipo integrale.  
  
 Per impostazione predefinita, un'espressione che contiene solo valori costanti provoca un errore del compilatore se produce un valore che non rientra nell'intervallo del tipo di destinazione.  Se l'espressione contiene uno o più valori non costanti, l'overflow non viene rilevato dal compilatore.  La valutazione dell'espressione assegnata a `i2` nell'esempio seguente non provoca un errore del compilatore.  
  
 [!code-cs[csrefKeywordsChecked#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/checked_1.cs)]  
  
 Per impostazione predefinita, in queste espressioni non costanti non viene eseguito il controllo dell'overflow nemmeno in fase di esecuzione e le espressioni non generano eccezioni di overflow.  Nell'esempio precedente viene indicato il valore \-2.147.483.639 come somma di due numeri interi positivi.  
  
 Il controllo dell'overflow può essere abilitato tramite le opzioni del compilatore, la configurazione dell'ambiente o l'utilizzo della parola chiave `checked`.  Negli esempi seguenti viene illustrato come utilizzare un'espressione `checked` o un blocco `checked` per rilevare l'overflow prodotto in fase di esecuzione dalla somma precedente.  Entrambi gli esempi generano un'eccezione di overflow.  
  
 [!code-cs[csrefKeywordsChecked#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/checked_2.cs)]  
  
 La parola chiave [unchecked](../../../csharp/language-reference/keywords/unchecked.md) può essere utilizzata per impedire il controllo dell'overflow.  
  
## Esempio  
 In questo esempio viene illustrato come utilizzare `checked` per abilitare il controllo dell'overflow in fase di esecuzione.  
  
 [!code-cs[csrefKeywordsChecked#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/checked_3.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Checked e Unchecked](../../../csharp/language-reference/keywords/checked-and-unchecked.md)   
 [unchecked](../../../csharp/language-reference/keywords/unchecked.md)