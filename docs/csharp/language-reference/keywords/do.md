---
title: do (Riferimenti per C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- do_CSharpKeyword
- do
dev_langs:
- CSharp
helpviewer_keywords:
- do keyword [C#]
ms.assetid: 50725f79-9ba6-4898-aa78-6e331568a1bb
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
ms.openlocfilehash: 95655432bde750de54996daaa2e9457a420d7c80
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="do-c-reference"></a>do (Riferimenti per C#)
L'istruzione `do` esegue ripetutamente un'istruzione o un blocco di istruzioni finché un'espressione specificata non restituisce `false`. Il corpo del ciclo deve essere racchiuso tra parentesi graffe, `{}`, a meno che sia costituito da una singola istruzione. In tal caso le parentesi graffe sono facoltative.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono eseguite le istruzioni del ciclo `do-while` fino a quando la variabile `x` è minore di 5.  
  
 [!code-cs[csrefKeywordsIteration#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/do_1.cs)]  
  
 A differenza dell'istruzione [while](../../../csharp/language-reference/keywords/while.md), un ciclo `do-while` viene eseguito una sola volta prima che sia valutata l'espressione condizionale.  
  
 In qualsiasi momento nel blocco `do-while` è possibile uscire dal ciclo usando l'istruzione [break](../../../csharp/language-reference/keywords/break.md). Si può eseguire direttamente l'istruzione di valutazione dell'espressione `while` usando l'istruzione [continue](../../../csharp/language-reference/keywords/continue.md). Se l'espressione `while` restituisce true, l'esecuzione continua con la prima istruzione del ciclo. Se l'espressione restituisce false, l'esecuzione continua con la prima istruzione dopo il ciclo `do-while`.  
  
 È possibile uscire da un ciclo `do-while` anche con le istruzioni [goto](../../../csharp/language-reference/keywords/goto.md), [return](../../../csharp/language-reference/keywords/return.md) o [throw](../../../csharp/language-reference/keywords/throw.md).  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Istruzione do-while (C++)](https://docs.microsoft.com/cpp/cpp/do-while-statement-cpp)   
 [Istruzioni di iterazione](../../../csharp/language-reference/keywords/iteration-statements.md)
