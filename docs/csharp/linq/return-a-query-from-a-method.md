---
title: Ottenere una query da un metodo
description: Come ottenere una query.
keywords: .NET, .NET Core, C#
author: BillWagner
manager: wpickett
ms.author: wiwagn
ms.date: 11/30/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: db220f79-c35b-41f2-886c-cd068672d42d
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0a83e3cc0e131351ef581fc15c68a3d0fda2bcce
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-return-a-query-from-a-method-c-programming-guide"></a>Procedura: ottenere una query da un metodo (Guida per programmatori C#)
In questo esempio viene illustrato come ottenere una query da un metodo come valore restituito e come parametro `out`.  
  
 Gli oggetti di query sono componibili, vale a dire che è possibile ottenere una query da un metodo. Gli oggetti che rappresentano le query non memorizzano la raccolta risultante, ma piuttosto i passaggi da eseguire per ottenere i risultati quando necessario. Il vantaggio di ottenere oggetti query dai metodi è che gli oggetti possono essere ulteriormente composti o modificati. Di conseguenza, qualsiasi valore restituito o parametro `out` di un metodo che restituisce una query deve contenere anche quel tipo. Se un metodo materializza una query in un oggetto <xref:System.Collections.Generic.List%601> concreto o un tipo <xref:System.Array>, si ritiene che restituisca i risultati della query anziché la query stessa. Una variabile di query che viene restituita da un metodo può ancora essere composta o modificata.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente il primo metodo restituisce una query come valore restituito e il secondo metodo restituisce una query come parametro `out`. Notare che in entrambi i casi è una query che viene restituita, non i risultati della query.  
  
 [!code-cs[csProgGuideLINQ#80](../../../samples/snippets/csharp/concepts/linq/how-to-return-a-query-from-a-method_1.cs)]  

## <a name="see-also"></a>Vedere anche  
 [Espressioni di query LINQ](index.md)
