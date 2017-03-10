---
title: "unchecked (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "unchecked_CSharpKeyword"
  - "unchecked"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "unchecked (parola chiave) [C#]"
ms.assetid: 0c021f7c-923f-4b3d-a58f-55336f5ac27e
caps.latest.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 23
---
# unchecked (Riferimenti per C#)
La parola chiave `unchecked` viene utilizzata per eliminare il controllo dell'overflow nelle conversioni e nelle operazioni aritmetiche di tipo integrale.  
  
 In un contesto non controllato, o di tipo unchecked, se un'espressione produce un valore non compreso nell'intervallo del tipo di destinazione, l'overflow non viene contrassegnato.  Poiché, ad esempio, il calcolo nell'esempio seguente viene eseguito in un 'espressione o blocco di tipo `unchecked`, il fatto che il risultato sia troppo grande per un tipo Integer viene ignorato e a `int1` viene assegnato il valore \-2.147.483.639.  
  
 [!code-cs[csrefKeywordsChecked#5](../../../csharp/language-reference/keywords/codesnippet/csharp/unchecked_1.cs)]  
  
 Se l'ambiente `unchecked` viene rimosso, si verifica un errore di compilazione.  È possibile rilevare l'overflow in fase di compilazione perché tutti i termini dell'espressione sono costanti.  
  
 Le espressioni che contengono termini non costanti non vengono controllate per impostazione predefinita in fase di compilazione e di esecuzione.  Per informazioni sull'abilitazione di un ambiente controllato, o di tipo checked, vedere [checked](../../../csharp/language-reference/keywords/checked.md).  
  
 Poiché il controllo dell'overflow richiede tempo, l'utilizzo di codice non controllato in situazioni in cui non vi è pericolo di overflow potrebbe consentire un miglioramento delle prestazioni.  Se tuttavia è possibile che si verifichi un overflow, è necessario utilizzare un ambiente controllato.  
  
## Esempio  
 In questo esempio viene illustrato come utilizzare la parola chiave `unchecked`.  
  
 [!code-cs[csrefKeywordsChecked#2](../../../csharp/language-reference/keywords/codesnippet/csharp/unchecked_2.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Checked e Unchecked](../../../csharp/language-reference/keywords/checked-and-unchecked.md)   
 [checked](../../../csharp/language-reference/keywords/checked.md)