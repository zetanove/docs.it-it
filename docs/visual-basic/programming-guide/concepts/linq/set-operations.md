---
title: Operazioni (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 2b06e822-e030-438f-9db7-ee402bd3a706
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e835737b388427445a15b6658c7d148801f29b79
ms.lasthandoff: 03/13/2017

---
# <a name="set-operations-visual-basic"></a>Operazioni sui set (Visual Basic)
Operazioni set in LINQ si riferiscono alle operazioni di query che producono un set di risultati che si basa sulla presenza o assenza di elementi equivalenti all'interno della stessa o separato raccolte (o set).  
  
 Nella sezione seguente sono elencati i metodi di operatore query standard che eseguono le operazioni di impostazione.  
  
## <a name="methods"></a>Metodi  
  
|Nome metodo|Descrizione|Sintassi delle espressioni di Query Visual Basic|Altre informazioni|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|Distinct|Rimuove i valori duplicati da una raccolta.|`Distinct`|<xref:System.Linq.Enumerable.Distinct%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Distinct%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Distinct%2A?displayProperty=fullName></xref:System.Linq.Queryable.Distinct%2A?displayProperty=fullName>|  
|Eccezione|Restituisce la differenza di set, ovvero gli elementi di una raccolta che non vengono visualizzati in un secondo insieme.|Non applicabile.|<xref:System.Linq.Enumerable.Except%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Except%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Except%2A?displayProperty=fullName></xref:System.Linq.Queryable.Except%2A?displayProperty=fullName>|  
|Interseca|Restituisce l'intersezione di set, ovvero gli elementi presenti in ciascuna delle due raccolte.|Non applicabile.|<xref:System.Linq.Enumerable.Intersect%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Intersect%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Intersect%2A?displayProperty=fullName></xref:System.Linq.Queryable.Intersect%2A?displayProperty=fullName>|  
|Unione|Restituisce l'unione di set, ovvero gli elementi univoci presenti in uno di due raccolte.|Non applicabile.|<xref:System.Linq.Enumerable.Union%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Union%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Union%2A?displayProperty=fullName></xref:System.Linq.Queryable.Union%2A?displayProperty=fullName>|  
  
## <a name="comparison-of-set-operations"></a>Confronto tra le operazioni di impostazione  
  
### <a name="distinct"></a>Distinct  
 Nella figura seguente viene illustrato il comportamento di <xref:System.Linq.Enumerable.Distinct%2A?displayProperty=fullName>metodo in una sequenza di caratteri.</xref:System.Linq.Enumerable.Distinct%2A?displayProperty=fullName> La sequenza restituita contiene gli elementi univoci della sequenza di input.  
  
 ![Grafica che mostra il comportamento di Distinct (). ] (../../../../csharp/programming-guide/concepts/linq/media/distinct.png "Distinti")  
  
### <a name="except"></a>Eccezione  
 Nella figura seguente viene illustrato il comportamento di <xref:System.Linq.Enumerable.Except%2A?displayProperty=fullName>.</xref:System.Linq.Enumerable.Except%2A?displayProperty=fullName> La sequenza restituita contiene solo gli elementi dalla sequenza di input prima che non sono presenti nella seconda sequenza di input.  
  
 ![Rappresentazione grafica dell'azione di Except (). ](../../../../csharp/programming-guide/concepts/linq/media/except.png "Except")  
  
### <a name="intersect"></a>Interseca  
 Nella figura seguente viene illustrato il comportamento di <xref:System.Linq.Enumerable.Intersect%2A?displayProperty=fullName>.</xref:System.Linq.Enumerable.Intersect%2A?displayProperty=fullName> La sequenza restituita contiene gli elementi che sono comuni a entrambe le sequenze di input.  
  
 ![Grafica che mostra l'intersezione di due sequenze. ] (../../../../csharp/programming-guide/concepts/linq/media/intersect.png "Si intersecano")  
  
### <a name="union"></a>Unione  
 Nella figura seguente viene illustrata un'operazione di unione di due sequenze di caratteri. La sequenza restituita contiene gli elementi univoci di entrambe le sequenze di input.  
  
 ![Grafica che mostra l'unione di due sequenze. ](../../../../csharp/programming-guide/concepts/linq/media/union.png "Union")  
  
## <a name="query-expression-syntax-example"></a>Esempio di sintassi di espressione di query  
 Nell'esempio seguente viene utilizzata la `Distinct` clausola in una query LINQ per restituire i numeri univoci da un elenco di numeri interi.  
  
 [!code-vb[CsLINQSetOps n.&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/set-operations_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq></xref:System.Linq>   
 [Cenni preliminari sugli operatori di Query standard (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Clausola DISTINCT](../../../../visual-basic/language-reference/queries/distinct-clause.md)   
 [Procedura: combinare e confrontare raccolte di stringhe (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-combine-and-compare-string-collections-linq.md)   
 [Procedura: trovare la differenza dei Set tra due elenchi (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-find-the-set-difference-between-two-lists-linq.md)
