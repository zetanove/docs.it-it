---
title: foreach, in (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- foreach
- foreach_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- foreach keyword [C#]
- foreach statement [C#]
- in keyword [C#]
ms.assetid: 5a9c5ddc-5fd3-457a-9bb6-9abffcd874ec
caps.latest.revision: 29
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: aa5408dbe214af2c21edd394f74fb8b675f2a099
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="foreach-in-c-reference"></a>foreach, in (Riferimenti per C#)
L'istruzione `foreach` ripete un gruppo di istruzioni incorporate per ogni elemento di una matrice o di una raccolta di oggetti che implementa l'interfaccia <xref:System.Collections.IEnumerable?displayProperty=fullName> o <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName>. L'istruzione `foreach` viene usata per eseguire l'iterazione della raccolta e ottenere le informazioni desiderate. Per evitare effetti indesiderati, non deve tuttavia essere usata per aggiungere o rimuovere elementi dalla raccolta di origine. Se è necessario aggiungere o rimuovere elementi dalla raccolta di origine, usare il ciclo [for](../../../csharp/language-reference/keywords/for.md).  
  
 L'esecuzione delle istruzioni incorporate viene ripetuta per ogni elemento nella matrice o nella raccolta. Quando l'iterazione è stata completata per tutti gli elementi nella raccolta, il controllo viene trasferito alla prima istruzione che segue il blocco `foreach`.  
  
 In un punto qualsiasi all'interno del blocco `foreach` è possibile uscire dal ciclo usando la parola chiave [break](../../../csharp/language-reference/keywords/break.md) o passare all'iterazione successiva nel ciclo con la parola chiave [continue](../../../csharp/language-reference/keywords/continue.md).  
  
 È anche possibile uscire da un ciclo `foreach` tramite le istruzioni [goto](../../../csharp/language-reference/keywords/goto.md), [return](../../../csharp/language-reference/keywords/return.md) o [throw](../../../csharp/language-reference/keywords/throw.md).  
  
 Per altre informazioni sulla parola chiave `foreach` e per esempi di codice, vedere gli argomenti riportati di seguito:  
  
 [Uso di foreach con matrici](../../../csharp/programming-guide/arrays/using-foreach-with-arrays.md)  
  
 [Procedura: Accedere a una classe Collection con foreach](../../../csharp/programming-guide/classes-and-structs/how-to-access-a-collection-class-with-foreach.md)  
  
## <a name="example"></a>Esempio  
 Il codice seguente illustra tre esempi:  
  
-   Un ciclo `foreach` tipico che visualizza il contenuto di una matrice di numeri interi  
  
-   Un ciclo [for](../../../csharp/language-reference/keywords/for.md) che esegue la stessa operazione  
  
-   Un ciclo `foreach` che gestisce un conteggio del numero di elementi nella matrice  
  
 [!code-cs[csrefKeywordsIteration#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/foreach-in_1.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Istruzioni di iterazione](../../../csharp/language-reference/keywords/iteration-statements.md)   
 [for](../../../csharp/language-reference/keywords/for.md)
