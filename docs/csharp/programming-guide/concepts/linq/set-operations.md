---
title: Operazioni sui set (C#) | Documentazione Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 7c589367-ef8f-4161-9050-642c47e6bf63
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 37841cde3aa5e4aaa6545b3a160422d024be5842
ms.lasthandoff: 03/13/2017

---
# <a name="set-operations-c"></a>Operazioni sui set (C#)
Le operazioni sui set in LINQ si riferiscono alle operazioni di query che generano un set di risultati basato sulla presenza o sull'assenza di elementi equivalenti all'interno delle stesse Collection oppure di Collection (o set) distinte.  
  
 La sezione seguente elenca i metodi dell'operatore query standard che eseguono operazioni sui set.  
  
## <a name="methods"></a>Metodi  
  
|Nome metodo|Descrizione|Sintassi di espressione della query C#|Altre informazioni|  
|-----------------|-----------------|---------------------------------|----------------------|  
|Distinct|Rimuove i valori duplicati da una Collection.|Non applicabile.|<xref:System.Linq.Enumerable.Distinct%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Distinct%2A?displayProperty=fullName>|  
|Eccezione|Restituisce la differenza dei set, ovvero gli elementi di una Collection che non sono presenti in una seconda Collection.|Non applicabile.|<xref:System.Linq.Enumerable.Except%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Except%2A?displayProperty=fullName>|  
|Interseca|Restituisce l'intersezione di set, ovvero gli elementi presenti in ognuna delle due Collection.|Non applicabile.|<xref:System.Linq.Enumerable.Intersect%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Intersect%2A?displayProperty=fullName>|  
|Unione|Restituisce l'unione di set, ovvero gli elementi univoci presenti in una delle due Collection.|Non applicabile.|<xref:System.Linq.Enumerable.Union%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Union%2A?displayProperty=fullName>|  
  
## <a name="comparison-of-set-operations"></a>Confronto tra le operazioni sui set  
  
### <a name="distinct"></a>Distinct  
 La figura seguente illustra il comportamento del metodo <xref:System.Linq.Enumerable.Distinct%2A?displayProperty=fullName> su una sequenza di caratteri. La sequenza restituita contiene gli elementi univoci dalla sequenza di input.  
  
 ![Grafico che mostra il comportamento di Distinct&#40;&#41;.](../../../../csharp/programming-guide/concepts/linq/media/distinct.png "Distinct")  
  
### <a name="except"></a>Eccezione  
 La figura seguente illustra il comportamento di <xref:System.Linq.Enumerable.Except%2A?displayProperty=fullName>. La sequenza restituita contiene solo gli elementi dalla prima sequenza di input che non sono presenti nella seconda sequenza di input.  
  
 ![Grafico che mostra l'azione di Except&#40;&#41;.](../../../../csharp/programming-guide/concepts/linq/media/except.png "Except")  
  
### <a name="intersect"></a>Interseca  
 La figura seguente illustra il comportamento di <xref:System.Linq.Enumerable.Intersect%2A?displayProperty=fullName>. La sequenza restituita contiene gli elementi comuni a entrambe le sequenze di input.  
  
 ![Grafico che mostra l'intersezione di due sequenze.](../../../../csharp/programming-guide/concepts/linq/media/intersect.png "Intersect")  
  
### <a name="union"></a>Unione  
 La figura seguente illustra un'operazione di unione tra due sequenze di caratteri. La sequenza restituita contiene gli elementi univoci da entrambe le sequenze di input.  
  
 ![Grafico che mostra l'unione di due sequenze.](../../../../csharp/programming-guide/concepts/linq/media/union.png "Union")  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq>   
 [Cenni preliminari sugli operatori di query standard (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Procedura: Combinare e confrontare Collection di stringhe (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-combine-and-compare-string-collections-linq.md)   
 [Procedura: Trovare la differenza dei set tra due elenchi (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-find-the-set-difference-between-two-lists-linq.md)
