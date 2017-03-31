---
title: void (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- void_CSharpKeyword
- void
dev_langs:
- CSharp
helpviewer_keywords:
- void keyword [C#]
ms.assetid: 0d2d8a95-fe20-4fbd-bf5d-c1e54bce71d4
caps.latest.revision: 15
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b4aa3c7c54e5e4d53975262adbbd9b54c701a69e
ms.lasthandoff: 03/13/2017

---
# <a name="void-c-reference"></a>void (Riferimenti per C#)
Quando viene usato come tipo restituito per un metodo `void` specifica che il metodo non restituisce un valore.  
  
 L'uso di `void` non è consentito nell'elenco di parametri di un metodo. Un metodo che non accetta parametri e non restituisce alcun valore viene dichiarato come segue:  
  
```  
public void SampleMethod()  
{  
    // Body of the method.  
}  
  
```  
  
 `void` si usa inoltre in un contesto unsafe per dichiarare un puntatore a un tipo sconosciuto. Per altre informazioni, vedere [Tipi di puntatori](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md).  
  
 `void` è un alias per il tipo <xref:System.Void?displayProperty=fullName> di .NET Framework.  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Tipi di riferimento](../../../csharp/language-reference/keywords/reference-types.md)   
 [Tipi di valore](../../../csharp/language-reference/keywords/value-types.md)   
 [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [Codice unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md)
