---
title: checked (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- checked_CSharpKeyword
- checked
dev_langs:
- CSharp
helpviewer_keywords:
- checked keyword [C#]
ms.assetid: 718a1194-988d-48a3-b089-d6ee8bd1608d
caps.latest.revision: 24
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
ms.openlocfilehash: 5826c8e6f99352c730824bb504a168226b9e6600
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="checked-c-reference"></a>checked (Riferimenti per C#)
La parola chiave `checked` viene usata per abilitare in modo esplicito il controllo dell'overflow per le conversioni e le operazioni aritmetiche di tipo integrale.  
  
 Per impostazione predefinita, un'espressione che contiene solo valori costanti provoca un errore di compilazione se l'espressione produce un valore che non è incluso nell'intervallo del tipo di destinazione. Se l'espressione contiene uno o più valori non costanti, il compilatore non rileva l'overflow. La valutazione dell'espressione assegnata a `i2` nell'esempio seguente non genera un errore di compilazione.  
  
 [!code-cs[csrefKeywordsChecked#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/checked_1.cs)]  
  
 Per impostazione predefinita, in queste espressioni non costanti non viene verificato l'overflow in fase di esecuzione e non vengono generate eccezioni di overflow. Nell'esempio precedente viene visualizzato il valore -2,147,483,639 come somma di due numeri interi positivi.  
  
 Il controllo dell'overflow può essere abilitato tramite le opzioni del compilatore, la configurazione dell'ambiente o l'uso della parola chiave `checked`. Gli esempi seguenti illustrano come usare un'espressione `checked` o un blocco `checked` per rilevare l'overflow generato dalla somma precedente in fase di esecuzione. Entrambi gli esempi generano un'eccezione di overflow.  
  
 [!code-cs[csrefKeywordsChecked#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/checked_2.cs)]  
  
 La parola chiave [unchecked](../../../csharp/language-reference/keywords/unchecked.md) può essere usata per impedire il controllo dell'overflow.  
  
## <a name="example"></a>Esempio  
 Questo esempio illustra come usare `checked` per abilitare il controllo dell'overflow in fase di esecuzione.  
  
 [!code-cs[csrefKeywordsChecked#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/checked_3.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Checked e unchecked](../../../csharp/language-reference/keywords/checked-and-unchecked.md)   
 [unchecked](../../../csharp/language-reference/keywords/unchecked.md)
