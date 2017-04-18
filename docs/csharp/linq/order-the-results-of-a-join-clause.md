---
title: Ordinare i risultati di una clausola join
description: Come ordinare i risultati di una clausola join.
keywords: .NET, .NET Core, C#
author: BillWagner
manager: wpickett
ms.author: wiwagn
ms.date: 12/1/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: a7458901-1201-4c25-b8d9-c04ca52e0eb9
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0252dd62e5638ffd1ab4eeebcfc2382a65997e30
ms.lasthandoff: 03/13/2017

---
# <a name="order-the-results-of-a-join-clause"></a>Ordinare i risultati di una clausola join
Questo esempio descrive come ordinare i risultati di un'operazione di join. Si noti che l'ordinamento viene eseguito dopo l'operazione di join. In genere, sebbene sia possibile, non è consigliabile usare una clausola `orderby` con una o più sequenze di origine prima dell'operazione di join. Alcuni provider LINQ potrebbero non mantenere tale ordinamento dopo l'operazione di join.  
  
## <a name="example"></a>Esempio  
 Questa query crea un join di gruppo e quindi ordina i gruppi in base all'elemento categoria che è ancora nell'ambito. Nell'inizializzatore di tipi anonimi una sottoquery ordina tutti gli elementi corrispondenti della sequenza di prodotti.  
  
 [!code-cs[csProgGuideLINQ#81](../../../samples/snippets/csharp/concepts/linq/how-to-order-the-results-of-a-join-clause_1.cs)]  
 
## <a name="see-also"></a>Vedere anche  
 [Espressioni di query LINQ](index.md)   
 [Clausola orderby](../language-reference/keywords/orderby-clause.md)   
 [Clausola join](../language-reference/keywords/join-clause.md) 
