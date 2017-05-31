---
title: 'Procedura: Accedere a una classe Collection con foreach (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- collection classes [C#], foreach statement
ms.assetid: a6b9cf5c-6c8d-4223-b12c-288949434493
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
ms.openlocfilehash: 841132b5181c5e17d1eabae11d3550811aa959ec
ms.contentlocale: it-it
ms.lasthandoff: 03/24/2017

---
# <a name="how-to-access-a-collection-class-with-foreach-c-programming-guide"></a>Procedura: accedere a una classe Collection con foreach (Guida per programmatori C#)
Nell'esempio di codice seguente viene illustrato come scrivere una classe Collection non generica che può essere usata con [foreach](../../../csharp/language-reference/keywords/foreach-in.md) e viene definita una classe tokenizer di stringa.  
  
> [!NOTE]
>  La procedura riportata in questo esempio è consigliata solo quando non è possibile usare una classe Collection generica. Per un esempio su come implementare una classe Collection generica indipendente dai tipi che supporta <xref:System.Collections.Generic.IEnumerable%601>, vedere [Iteratori](http://msdn.microsoft.com/library/f45331db-d595-46ec-9142-551d3d1eb1a7).  
  
 Nell'esempio il segmento di codice seguente usa la classe `Tokens` per suddividere la frase "This is a sample sentence" in token usando ' ' e '-' come separatori. Il codice consente di visualizzare tali token tramite un'istruzione `foreach`.  
  
 [!code-cs[csProgGuideCollections#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-access-a-collection-class-with-foreach_1.cs)]  
  
## <a name="example"></a>Esempio  
 Internamente la classe `Tokens` usa una matrice per archiviare i token. Poiché le matrici implementano <xref:System.Collections.IEnumerator> e <xref:System.Collections.IEnumerable>, l'esempio di codice avrebbe potuto usare i metodi di enumerazione della matrice (<xref:System.Collections.IEnumerable.GetEnumerator%2A>, <xref:System.Collections.IEnumerator.MoveNext%2A>, <xref:System.Collections.IEnumerator.Reset%2A> e <xref:System.Collections.IEnumerator.Current%2A>) anziché definirli nella classe `Tokens`. Le definizioni dei metodi sono incluse nell'esempio per chiarire come vengono definiti i metodi e lo scopo di ognuno di essi.  
  
 [!code-cs[csProgGuideCollections#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-access-a-collection-class-with-foreach_2.cs)]  
  
 In C# non è necessario che una classe Collection implementi <xref:System.Collections.IEnumerable> e <xref:System.Collections.IEnumerator> per essere compatibile con `foreach`. Se la classe include i membri <xref:System.Collections.IEnumerable.GetEnumerator%2A>, <xref:System.Collections.IEnumerator.MoveNext%2A>, <xref:System.Collections.IEnumerator.Reset%2A> e <xref:System.Collections.IEnumerator.Current%2A> necessari, funzionerà con `foreach`. L'omissione delle interfacce consente di definire come tipo restituito per `Current` un tipo più specifico di <xref:System.Object>. In questo modo viene garantita l'indipendenza dai tipi.  
  
 Modificare ad esempio le righe seguenti dell'esempio precedente.  
  
```csharp  
  
// Change the Tokens class so that it no longer implements IEnumerable.  
public class Tokens  
{  
    // . . .  
  
    // Change the return type for the GetEnumerator method.  
    public TokenEnumerator GetEnumerator()  
    {   }  
  
    // Change TokenEnumerator so that it no longer implements IEnumerator.  
    public class TokenEnumerator  
    {  
        // . . .  
  
        // Change the return type of method Current to string.  
        public string Current  
        {   }  
    }  
 }  
  
```  
  
 Poiché `Current` restituisce una stringa, il compilatore può rilevare l'eventuale uso di un tipo non compatibile in un'istruzione `foreach`, come illustrato nel codice seguente.  
  
```csharp  
  
// Error: Cannot convert type string to int.  
foreach (int item in f)    
```  
  
 L'omissione di <xref:System.Collections.IEnumerable> e <xref:System.Collections.IEnumerator> impedisce tuttavia l'interoperabilità della classe Collection con le istruzioni `foreach` o con istruzioni equivalenti di altri linguaggi compatibili con Common Language Runtime.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Collections.Generic>   
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Matrici](../../../csharp/programming-guide/arrays/index.md)   
 [Raccolte](http://msdn.microsoft.com/library/e76533a9-5033-4a0b-b003-9c2be60d185b)
