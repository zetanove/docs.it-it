---
title: 'Procedura: Eseguire l&quot;override del metodo ToString (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- ToString method, overriding in C#
- inheritance [C#], overriding OnPaint and ToString
ms.assetid: 8016db69-1f19-420c-8e17-98e8bebb7749
caps.latest.revision: 21
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
ms.sourcegitcommit: 400dfda51d978f35c3995f90840643aaff1b9c13
ms.openlocfilehash: 2dde281d439a07d7736949294772a57e926eb587
ms.contentlocale: it-it
ms.lasthandoff: 03/24/2017

---
# <a name="how-to-override-the-tostring-method-c-programming-guide"></a>Procedura: eseguire l'override del metodo ToString (Guida per programmatori C#)
Ogni classe o struct in C# eredita in modo implicito la classe <xref:System.Object>. Ogni oggetto in C# ottiene pertanto il metodo <xref:System.Object.ToString%2A>, che restituisce una rappresentazione di stringa dell'oggetto. Ad esempio, tutte le variabili di tipo `int` hanno un metodo `ToString` che consente loro di restituire il rispettivo contenuto sotto forma di stringa:  
  
 [!code-cs[csProgGuideInheritance#37](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-override-the-tostring-method_1.cs)]  
  
 Quando si crea una classe o uno struct personalizzato, eseguire l'override del metodo <xref:System.Object.ToString%2A> per comunicare informazioni sul tipo al codice client.  
  
 Per informazioni sull'uso di stringhe di formato e altri tipi di formattazione personalizzata con il metodo `ToString`, vedere [Formattazione di tipi](../../../standard/base-types/formatting-types.md).  
  
> [!IMPORTANT]
>  Dopo aver deciso quali informazioni comunicare tramite questo metodo, considerare se la classe o lo struct sarà usato da codice non attendibile. Verificare attentamente di non indicare informazioni che potrebbero essere sfruttate da malware.  
  
### <a name="to-override-the-tostring-method-in-your-class-or-struct"></a>Per eseguire l'override del metodo ToString nella classe o nello struct  
  
1.  Dichiarare un metodo `ToString` con i modificatori e il tipo restituito seguenti:  
  
    ```csharp  
    public override string ToString(){}  
    ```  
  
2.  Implementare il metodo in modo che restituisca una stringa.  
  
     L'esempio seguente restituisce il nome della classe oltre ai dati specifici per una particolare istanza della classe.  
  
     [!code-cs[csProgGuideInheritance#36](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-override-the-tostring-method_2.cs)]  
  
     È anche possibile testare il metodo `ToString` come illustrato nel codice di esempio seguente:  
  
     [!code-cs[csProgGuideInheritance#38](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-override-the-tostring-method_3.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.IFormattable>   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Stringhe](../../../csharp/programming-guide/strings/index.md)   
 [string](../../../csharp/language-reference/keywords/string.md)   
 [new](../../../csharp/language-reference/keywords/new.md)   
 [override](../../../csharp/language-reference/keywords/override.md)   
 [virtual](../../../csharp/language-reference/keywords/virtual.md)   
 [Formattazione di tipi](../../../standard/base-types/formatting-types.md)
