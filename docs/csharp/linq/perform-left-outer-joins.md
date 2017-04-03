---
title: Eseguire left outer join
description: Come eseguire i left outer join.
keywords: .NET, .NET Core, C#
author: stevehoag
manager: wpickett
ms.author: wiwagn
ms.date: 12/1/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: f542cee6-3169-4dcf-a631-3a6a79ccd473
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6ba90a6fe16d4ba33e8b9e55c93f7365b6bc905b
ms.lasthandoff: 03/13/2017

---
# <a name="perform-left-outer-joins"></a>Eseguire left outer join
Un left outer join è un join in cui viene restituito ogni elemento della prima raccolta, anche se non ha elementi correlati nella seconda raccolta. È possibile usare LINQ per eseguire un left outer join chiamando il metodo <xref:System.Linq.Enumerable.DefaultIfEmpty%2A> nei risultati di un join di gruppo.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra come usare il metodo <xref:System.Linq.Enumerable.DefaultIfEmpty%2A> nei risultati di un join di gruppo per eseguire un left outer join.  
  
 Il primo passaggio nella produzione di un left outer join di due raccolte consiste nell'esecuzione di un inner join usando un join di gruppo. Per una descrizione di questo processo, vedere [Eseguire inner join](perform-inner-joins.md). In questo esempio l'elenco di oggetti `Person` è unito tramite inner join all'elenco di oggetti `Pet` basati su un oggetto `Person` che corrisponde a `Pet.Owner`.  
  
 Il secondo passaggio consiste nell'includere ogni elemento della prima raccolta di sinistra nel set di risultati anche se l'elemento non ha corrispondenze nella raccolta di destra. Questa operazione viene eseguita chiamando <xref:System.Linq.Enumerable.DefaultIfEmpty%2A> in ogni sequenza di elementi corrispondenti dal join di gruppo. In questo esempio <xref:System.Linq.Enumerable.DefaultIfEmpty%2A> viene chiamato in ogni sequenza di oggetti `Pet` corrispondenti. Il metodo restituisce una raccolta che contiene un solo valore predefinito se la sequenza di oggetti `Pet` corrispondenti è vuota per qualsiasi oggetto `Person`, assicurando in questo modo che ogni oggetto `Person` sia rappresentato nella raccolta di risultati.  
  
> [!NOTE]
>  Il valore predefinito per un tipo di riferimento è `null`. Di conseguenza, l'esempio cerca un riferimento Null prima di accedere a ogni elemento di ogni raccolta `Pet`.  
  
 [!code-cs[CsLINQProgJoining#7](../../../samples/snippets/csharp/concepts/linq/how-to-perform-left-outer-joins_1.cs)]  
 
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq.Enumerable.Join%2A>   
 <xref:System.Linq.Enumerable.GroupJoin%2A>   
 [Eseguire inner join](perform-inner-joins.md)   
 [Eseguire join raggruppati](perform-grouped-joins.md)   
 [Tipi anonimi](../programming-guide/classes-and-structs/anonymous-types.md)   
 
