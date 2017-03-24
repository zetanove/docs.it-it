---
title: "Iterator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Iterator"
helpviewer_keywords: 
  - "Iterator keyword [Visual Basic]"
ms.assetid: 69cb0b04-ac87-49d0-bcfe-810c0d60daff
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# Iterator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica che una funzione o una funzione di accesso di `Get` è un iteratore.  
  
## Note  
 *Un iteratore* esegue un'iterazione personalizzata in una raccolta.  Un iteratore utilizza l'istruzione di [Le prestazioni](../../../visual-basic/language-reference/statements/yield-statement.md) per restituire ogni elemento della raccolta uno alla volta.  Quando un'istruzione di `Yield` viene raggiunto, la posizione corrente nel codice vengono mantenute.  L'esecuzione verrà riavviata da tale percorso alla successiva esecuzione della funzione di iteratore è denominata.  
  
 Un iteratore può essere implementato come funzione o come funzione di accesso di `Get` di una definizione di proprietà.  Il modificatore di `Iterator` viene visualizzato nella dichiarazione della funzione di iteratore o della funzione di accesso di `Get` .  
  
 Chiama un iteratore dal codice client utilizzando [Istruzione For Each...Next](../../../visual-basic/language-reference/statements/for-each-next-statement.md).  
  
 Il tipo restituito di una funzione di iteratore o di funzione di accesso di `Get` può essere <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator>, o <xref:System.Collections.Generic.IEnumerator%601>.  
  
 Un iteratore non può avere parametri di `ByRef` .  
  
 Un iteratore non può verificarsi in un evento, in un costruttore di istanza, in un costruttore statico, o un distruttore statico.  
  
 Un iteratore può essere una funzione anonima.  Per ulteriori informazioni, vedere [Iteratori](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md).  
  
 Per ulteriori informazioni sugli iteratori, vedere [Iteratori](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Utilizzo  
 Il modificatore `Iterator` può essere utilizzato nei seguenti contesti:  
  
-   [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)  
  
-   [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)  
  
## Esempio  
 Nell'esempio seguente viene illustrata una funzione di iteratore.  La funzione di iteratore ha un'istruzione di `Yield` presente in un ciclo di [per… seguente](../../../visual-basic/language-reference/statements/for-next-statement.md) .  Ogni iterazione del corpo dell'istruzione di [For Each](../../../visual-basic/language-reference/statements/for-each-next-statement.md) in `Main` crea una chiamata alla funzione iteratore di `Power` .  Ogni chiamata alla funzione di iteratore consente l'esecuzione dell'dell'istruzione di `Yield` , che si verifica durante l'iterazione successiva del ciclo di `For…Next` .  
  
 [!code-vb[VbVbalrStatements#98](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/iterator_1.vb)]  
  
## Esempio  
 Nell'esempio seguente viene illustrata una funzione di accesso di `Get` che è un iteratore.  Il modificatore di `Iterator` nella dichiarazione di proprietà.  
  
 [!code-vb[VbVbalrStatements#99](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/iterator_2.vb)]  
  
 Per ulteriori esempi, vedere [Iteratori](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Vedere anche  
 <xref:System.Runtime.CompilerServices.IteratorStateMachineAttribute>   
 [Iteratori](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)   
 [Istruzione Yield](../../../visual-basic/language-reference/statements/yield-statement.md)