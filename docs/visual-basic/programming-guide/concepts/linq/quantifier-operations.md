---
title: Operazioni quantificatore (Visual Basic) | Documenti di Microsoft
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
ms.assetid: ae1a2b73-503c-4f4b-a3fd-31b5adbee67c
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
ms.openlocfilehash: 7f69aed2e0e6791ca7f17c3420ff75a1ba220187
ms.lasthandoff: 03/13/2017

---
# <a name="quantifier-operations-visual-basic"></a>Operazioni quantificatore (Visual Basic)
Operazioni del quantificatore restituiscono un <xref:System.Boolean>valore che indica se alcuni o tutti gli elementi in una sequenza soddisfano una condizione.</xref:System.Boolean>  
  
 La figura seguente illustra due diverse operazioni del quantificatore due sequenze di origine diversa. La prima operazione viene chiesto se uno o più elementi sono il carattere 'A' e il risultato è `true`. La seconda operazione viene chiesto se tutti gli elementi sono il carattere 'A' e il risultato è `true`.  
  
 ![Operazioni con quantificatore LINQ](../../../../csharp/programming-guide/concepts/linq/media/linq_quantifier.png "LINQ_Quantifier")  
  
 Nella sezione seguente sono elencati i metodi di operatore query standard che eseguono operazioni con quantificatore.  
  
## <a name="methods"></a>Metodi  
  
|Nome metodo|Descrizione|Sintassi delle espressioni di Query Visual Basic|Altre informazioni|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|Tutti|Determina se tutti gli elementi in una sequenza soddisfano una condizione.|`Aggregate … In … Into All(…)`|<xref:System.Linq.Enumerable.All%2A?displayProperty=fullName></xref:System.Linq.Enumerable.All%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.All%2A?displayProperty=fullName></xref:System.Linq.Queryable.All%2A?displayProperty=fullName>|  
|Qualsiasi|Determina se tutti gli elementi in una sequenza soddisfano una condizione.|`Aggregate … In … Into Any()`|<xref:System.Linq.Enumerable.Any%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Any%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Any%2A?displayProperty=fullName></xref:System.Linq.Queryable.Any%2A?displayProperty=fullName>|  
|Contiene|Determina se una sequenza contiene un elemento specificato.|Non applicabile.|<xref:System.Linq.Enumerable.Contains%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Contains%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Contains%2A?displayProperty=fullName></xref:System.Linq.Queryable.Contains%2A?displayProperty=fullName>|  
  
## <a name="query-expression-syntax-examples"></a>Esempi di sintassi delle espressioni di query  
 Negli esempi viene utilizzata la `Aggregate` clausola in Visual Basic come parte della condizione di filtro in una query LINQ.  
  
 Nell'esempio seguente viene utilizzata la `Aggregate` clausola e <xref:System.Linq.Enumerable.All%2A>metodo di estensione per restituire un insieme le persone con animali domestici tutti a una data specificata.</xref:System.Linq.Enumerable.All%2A>  
  
 [!code-vb[CsLINQAnyAll n.&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/quantifier-operations_1.vb)]  
  
 Nell'esempio successivo viene utilizzata la `Aggregate` clausola e <xref:System.Linq.Enumerable.Any%2A>metodo di estensione per restituire da una raccolta di coloro che hanno almeno un animale che è precedente rispetto a un periodo di validità specificato.</xref:System.Linq.Enumerable.Any%2A>  
  
 [!code-vb[CsLINQAnyAll n.&2;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/quantifier-operations_2.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq></xref:System.Linq>   
 [Cenni preliminari sugli operatori di Query standard (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Clausola Aggregate](../../../../visual-basic/language-reference/queries/aggregate-clause.md)   
 [Procedura: eseguire una Query per trovare frasi che contengono un Set specificato di parole (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-for-sentences-that-contain-a-specified-set-of-words.md)
