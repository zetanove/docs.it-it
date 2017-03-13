---
title: "foreach, in (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "foreach"
  - "foreach_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "foreach (parola chiave) [C#]"
  - "foreach (istruzione) [C#]"
  - "in (parola chiave) [C#]"
ms.assetid: 5a9c5ddc-5fd3-457a-9bb6-9abffcd874ec
caps.latest.revision: 29
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 29
---
# foreach, in (Riferimenti per C#)
L'istruzione `foreach` ripete un gruppo di istruzioni incorporate per ciascun elemento di una matrice o di una raccolta di oggetti che implementa l'interaccia <xref:System.Collections.IEnumerable?displayProperty=fullName> o <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName>.  L'istruzione `foreach` viene utilizzata per scorrere la raccolta e ottenere le informazioni desiderate; non deve tuttavia essere utilizzata per aggiungere o rimuovere elementi nella raccolta di origine allo scopo di evitare effetti indesiderati.  Se è necessario aggiungere o rimuovere elementi nella raccolta di origine, utilizzare un ciclo [for](../../../csharp/language-reference/keywords/for.md).  
  
 L'esecuzione delle istruzioni incorporate viene ripetuta per ciascun elemento della matrice o della raccolta.  Quando l'iterazione è stata completata per tutti gli elementi della raccolta, il controllo viene trasferito alla prima istruzione che segue il blocco `foreach`.  
  
 In corrispondenza di qualsiasi punto all'interno del blocco `foreach` è possibile uscire dal ciclo utilizzando la parola chiave [break](../../../csharp/language-reference/keywords/break.md) o passare direttamente all'iterazione successiva nel ciclo utilizzando la parola chiave [continue](../../../csharp/language-reference/keywords/continue.md).  
  
 È inoltre possibile uscire da un ciclo `foreach` mediante le istruzioni [goto](../../../csharp/language-reference/keywords/goto.md), [return](../../../csharp/language-reference/keywords/return.md) e [throw](../../../csharp/language-reference/keywords/throw.md).  
  
 Per ulteriori informazioni sulla parola chiave `foreach` e per esempi di codice, vedere gli argomenti riportati di seguito:  
  
 [Utilizzo di foreach con matrici](../../../csharp/programming-guide/arrays/using-foreach-with-arrays.md)  
  
 [Procedura: accedere a una classe di raccolte con foreach](../../../csharp/programming-guide/classes-and-structs/how-to-access-a-collection-class-with-foreach.md)  
  
## Esempio  
 Il seguente codice riporta tre esempi:  
  
-   un ciclo `foreach` tipico visualizza il contenuto di una matrice di integer  
  
-   ciclo [for](../../../csharp/language-reference/keywords/for.md) che esegue la stessa operazione  
  
-   ciclo `foreach` che gestisce un conteggio del numero di elementi della matrice  
  
 [!code-cs[csrefKeywordsIteration#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/foreach-in_1.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Istruzioni di iterazione](../../../csharp/language-reference/keywords/iteration-statements.md)   
 [for](../../../csharp/language-reference/keywords/for.md)