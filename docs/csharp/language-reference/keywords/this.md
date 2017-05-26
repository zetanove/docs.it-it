---
title: this (Riferimenti per C#) | Documentazione Microsoft
description: Parola chiave this (Riferimenti per C#)
keywords: this (C#), parola chiave this (C#), parola chiave this (Riferimenti per C#), parola chiave this (Riferimenti per il linguaggio C#)
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- this
- this_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- this keyword [C#]
ms.assetid: d4f827fe-4710-410b-89b8-867dad44b8a3
caps.latest.revision: 19
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
ms.openlocfilehash: 8e14a32f11b9661ae18fd718fb1a72385fa7f3a7
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="this-c-reference"></a>this (Riferimenti per C#)
La parola chiave `this` fa riferimento all'istanza corrente della classe e viene anche usata come modificatore del primo parametro di un metodo di estensione.  
  
> [!NOTE]
>  Questo articolo illustra l'uso di `this` con istanze della classe. Per altre informazioni sull'uso nei metodi di estensione, vedere [Metodi di estensione](../../../csharp/programming-guide/classes-and-structs/extension-methods.md).  
  
 Di seguito sono riportati gli usi comuni di `this`:  
  
-   Per qualificare i membri nascosti da nomi simili, ad esempio:  
  
 [!code-cs[csrefKeywordsAccess#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/this_1.cs)]  
  
-   Per passare un oggetto come parametro ad altri metodi, ad esempio:  
  
    ```  
    CalcTax(this);  
    ```  
  
-   Per dichiarare gli indicizzatori, ad esempio:  
  
 [!code-cs[csrefKeywordsAccess#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/this_2.cs)]  
  
 Le funzioni del membro statico, perché esistono a livello di classe e non come parte di un oggetto, non dispongono di un puntatore `this`. È un errore fare riferimento a `this` in un metodo statico.  
  
## <a name="example"></a>Esempio  
 In questo esempio, `this` viene usato per qualificare i membri della classe `Employee`, `name` e `alias`, che sono nascosti da nomi simili. Viene anche usato per passare un oggetto al metodo `CalcTax`, che appartiene a un'altra classe.  
  
 [!code-cs[csrefKeywordsAccess#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/this_3.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [base](../../../csharp/language-reference/keywords/base.md)   
 [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)
