---
title: Gestire le eccezioni nelle espressioni di query
description: Come gestire le eccezioni nelle espressioni di query.
keywords: .NET, .NET Core, C#
author: BillWagner
manager: wpickett
ms.author: wiwagn
ms.date: 12/1/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 2bf0c397-13fb-4f68-bc2b-531c6c88a167
ms.translationtype: Human Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: d13387c4468a5c89cbe838139c767f0f95ab418d
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="handle-exceptions-in-query-expressions"></a>Gestire le eccezioni nelle espressioni di query

Nel contesto di un'espressione di query è possibile chiamare qualsiasi metodo. È tuttavia consigliabile non chiamare in un'espressione di query i metodi che possono creare un effetto collaterale, ad esempio la modifica del contenuto dell'origine dati o la generazione di un'eccezione. In questo esempio viene illustrato come evitare di generare eccezioni quando si chiamano i metodi in un'espressione di query senza violare le linee guida generali di .NET Framework sulla gestione delle eccezioni. Tali linee guida stabiliscono che è accettabile intercettare un'eccezione specifica quando è evidente il motivo per cui verrà generata in un contesto specificato. Per altre informazioni, vedere [Suggerimenti per le eccezioni](../../standard/exceptions/best-practices-for-exceptions.md).  
  
 Nell'esempio finale viene illustrato come gestire quei casi in cui è necessario generare un'eccezione durante l'esecuzione di una query.  
  
## <a name="example"></a>Esempio  

 Nell'esempio seguente viene illustrato come spostare codice di gestione dell'eccezione al di fuori di un'espressione di query. Questa operazione è possibile solo quando il metodo non dipende da variabili locali per la query.  
  
 [!code-cs[csProgGuideLINQ#10](../../../samples/snippets/csharp/concepts/linq/how-to-handle-exceptions-in-query-expressions_1.cs)]  
  
## <a name="example"></a>Esempio 

 In alcuni casi la migliore risposta a un'eccezione generata all'interno di una query potrebbe essere l'arresto immediato dell'esecuzione della query. Nell'esempio seguente viene illustrato come gestire le eccezioni che potrebbero essere generate all'interno del corpo di una query. Si supponga che `SomeMethodThatMightThrow` possa potenzialmente generare un'eccezione che richiede l'arresto dell'esecuzione della query.  
  
 Si noti che il blocco `try` racchiude il ciclo `foreach` e non la query stessa, in quanto il ciclo `foreach` è il punto in corrispondenza del quale la query viene effettivamente eseguita. Per altre informazioni, vedere [Introduzione alle query LINQ](../programming-guide/concepts/linq/introduction-to-linq-queries.md).  
  
 [!code-cs[csProgGuideLINQ#12](../../../samples/snippets/csharp/concepts/linq/how-to-handle-exceptions-in-query-expressions_2.cs)]  
  

## <a name="see-also"></a>Vedere anche  
 [Espressioni di query LINQ](index.md)
