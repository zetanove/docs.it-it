---
title: Gestire i valori Null nelle espressioni di query
description: Come gestire i valori Null nelle espressioni di query.
keywords: .NET, .NET Core, C#
author: stevehoag
manager: wpickett
ms.author: wiwagn
ms.date: 12/1/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: ac63ae8b-724d-4251-9334-528f4e884ae7
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 14b64bf8d3590f4f7dc3d1b00cb50d0bc421d9bc
ms.lasthandoff: 03/13/2017

---
# <a name="handle-null-values-in-query-expressions"></a>Gestire i valori Null nelle espressioni di query

In questo esempio viene illustrato come gestire i possibili valori Null nelle raccolte di origine. Una raccolta di oggetti quale <xref:System.Collections.Generic.IEnumerable%601> può contenere elementi il cui valore è [Null](../language-reference/keywords/null.md). Se una raccolta di origine è Null o contiene un elemento il cui valore è Null e la query non gestisce valori Null, verrà generata un'eccezione <xref:System.NullReferenceException> quando si esegue la query.  
  
## <a name="example"></a>Esempio

 È possibile codificare in modo sicuro per evitare un'eccezione di riferimento Null come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideLINQ#82](../../../samples/snippets/csharp/concepts/linq/how-to-handle-null-values-in-query-expressions_1.cs)]  
  
 Nell'esempio precedente la clausola `where` esclude tutti gli elementi Null nella sequenza di categorie. Questa tecnica è indipendente dal controllo Null nella clausola join. In questo esempio è possibile usare l'espressione condizionale con Null poiché `Products.CategoryID` è di tipo `int?`, vale a dire una sintassi abbreviata di `Nullable<int>`.  
  
## <a name="example"></a>Esempio

 Se in una clausola join solo una delle chiavi di confronto è un tipo di valore nullable, è possibile eseguire il cast delle altre chiavi a un tipo nullable nell'espressione di query. Nell'esempio seguente si supponga che `EmployeeID` sia una colonna contenente valori di tipo `int?`:  
  
 [!code-cs[csProgGuideLINQ#83](../../../samples/snippets/csharp/concepts/linq/how-to-handle-null-values-in-query-expressions_2.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Nullable%601>   
 [Espressioni di query LINQ](index.md)   
 [Tipi nullable](../programming-guide/nullable-types/index.md)
