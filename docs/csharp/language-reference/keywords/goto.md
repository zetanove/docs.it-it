---
title: goto (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- goto_CSharpKeyword
- goto
dev_langs:
- CSharp
helpviewer_keywords:
- goto keyword [C#]
ms.assetid: 2c03c9c1-8119-44ef-b740-fb3d287a42fe
caps.latest.revision: 22
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
ms.openlocfilehash: 700376096d969052a9f4633f565f9d9fd4dfec46
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="goto-c-reference"></a>goto (Riferimenti per C#)
L'istruzione `goto` passa direttamente il controllo del programma a un'istruzione con etichetta.  
  
 L'istruzione `goto` viene generalmente usata per trasferire il controllo a un'etichetta switch case specifica o all'etichetta predefinita di un'istruzione `switch`.  
  
 L'istruzione `goto` viene anche usata per uscire da cicli annidati più interni.  
  
## <a name="example"></a>Esempio  
 Nell'esempio riportato di seguito viene illustrato l'uso di `goto` in un'istruzione [switch](../../../csharp/language-reference/keywords/switch.md).  
  
 [!code-cs[csrefKeywordsJump#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/goto_1.cs)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio riportato di seguito viene illustrato come usare `goto` per uscire da cicli annidati.  
  
 [!code-cs[csrefKeywordsJump#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/goto_2.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Istruzione goto](https://docs.microsoft.com/cpp/cpp/goto-statement-cpp)   
 [Istruzioni di spostamento](../../../csharp/language-reference/keywords/jump-statements.md)
