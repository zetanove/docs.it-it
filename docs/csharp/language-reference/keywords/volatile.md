---
title: volatile (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- volatile_CSharpKeyword
- volatile
dev_langs:
- CSharp
helpviewer_keywords:
- volatile keyword [C#]
ms.assetid: 78089bc7-7b38-4cfd-9e49-87ac036af009
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
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 801187b1fcc25a1eea1f40ec8ac4c67af42e5880
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="volatile-c-reference"></a>volatile (Riferimenti per C#)
La parola chiave `volatile` indica che un campo potrebbe essere modificato da più thread eseguiti contemporaneamente. Un campo dichiarato `volatile` non è soggetto a ottimizzazioni del compilatore che presuppongono l'accesso da parte di un singolo thread. Ciò garantisce che il valore più aggiornato sia sempre presente nel campo.  
  
 Il modificatore `volatile` si usa in genere per un campo a cui accedono più thread senza usare l'istruzione [lock](../../../csharp/language-reference/keywords/lock-statement.md) per serializzare l'accesso.  
  
 La parola chiave `volatile` può essere applicata ai campi di questi tipi:  
  
-   Tipi di riferimento.  
  
-   Tipi di puntatore (in un contesto non sicuro). Si noti che sebbene il puntatore in sé possa essere volatile, non può esserlo l'oggetto a cui punta. In altre parole, non è possibile dichiarare un "puntatore a volatile".  
  
-   Tipi come sbyte, byte, short, ushort, int, uint, char, float e bool.  
  
-   Un tipo enum con uno dei seguenti tipi di base: byte, sbyte, short, ushort, int o uint.  
  
-   Parametri di tipo generico noti come tipi di riferimento.  
  
-   <xref:System.IntPtr> e <xref:System.UIntPtr>.  
  
 La parola chiave volatile può essere applicata solo a campi di una classe o struct. Le variabili locali non possono essere dichiarate `volatile`.  
  
## <a name="example"></a>Esempio  
 Nell'esempio riportato di seguito viene illustrato come dichiarare `volatile` una variabile di campo pubblico.  
  
 [!code-cs[csrefKeywordsModifiers#24](../../../csharp/language-reference/keywords/codesnippet/CSharp/volatile_1.cs)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come un thread di lavoro o ausiliario può essere creato e usato per eseguire l'elaborazione in parallelo con quella del thread principale. Per informazioni di base sul multithreading, vedere [Threading](../../../standard/threading/index.md) and [Threading](http://msdn.microsoft.com/library/552f6c68-dbdb-4327-ae36-32cf9063d88c).  
  
 [!code-cs[csProgGuideThreading#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/volatile_2.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)
