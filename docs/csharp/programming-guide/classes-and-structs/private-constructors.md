---
title: Costruttori privati (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- C# language, private constructors
- private constructors [C#]
ms.assetid: 29eeaa7d-8d81-453c-94b9-0e2800172621
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
ms.sourcegitcommit: a5ed524a1b17f7be8903f998cbd732594faab831
ms.openlocfilehash: e2ac39bc642cf5379d4a8e8f9c74068b93b0b5b4
ms.contentlocale: it-it
ms.lasthandoff: 05/15/2017

---
# <a name="private-constructors-c-programming-guide"></a>Costruttori privati (Guida per programmatori C#)
Un costruttore privato è un costruttore di istanza speciale. Viene generalmente usato in classi contenenti solo membri statici. Se una classe ha uno o più costruttori privati ma non include alcun costruttore pubblico, le altre classi, ad eccezione di quelle annidate, non potranno creare istanze della classe. Ad esempio:  
  
 [!code-cs[csProgGuideObjects#11](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/private-constructors_1.cs)]  
  
 La dichiarazione del costruttore vuoto impedisce la generazione automatica di un costruttore predefinito. Tenere presente che se non si usa un modificatore di accesso con il costruttore, questo rimarrà di tipo privato per impostazione predefinita. Tuttavia, il modificatore [private](../../../csharp/language-reference/keywords/private.md) viene solitamente usato in modo esplicito per specificare che non è possibile creare un'istanza della classe.  
  
 I costruttori privati vengono usati per impedire la creazione di istanze di una classe in assenza di metodi e campi di istanza, ad esempio la classe <xref:System.Math>, oppure quando viene chiamato un metodo per ottenere un'istanza di una classe. Se tutti i metodi della classe sono statici, è consigliabile rendere statica l'intera classe. Per altre informazioni, vedere [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato l'esempio di una classe che usa un costruttore privato.  
  
 [!code-cs[csProgGuideObjects#12](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/private-constructors_2.cs)]  
  
 Se si rimuove il commento dall'istruzione dell'esempio riportata di seguito, verrà generato un errore poiché non è possibile accedere al costruttore a causa del livello di protezione:  
  
 [!code-cs[csProgGuideObjects#13](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/private-constructors_3.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [Finalizzatori](../../../csharp/programming-guide/classes-and-structs/destructors.md)   
 [private](../../../csharp/language-reference/keywords/private.md)   
 [public](../../../csharp/language-reference/keywords/public.md)
