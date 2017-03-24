---
title: Operazioni di aggregazione (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 0f47e92c-5dd2-4007-baf4-c5fe5dc3b4a8
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 17d1f18f9acc2f3a62c106f7cff2cf68f8f58a07
ms.lasthandoff: 03/13/2017

---
# <a name="aggregation-operations-visual-basic"></a>Operazioni di aggregazione (Visual Basic)
Un'operazione di aggregazione calcola un singolo valore da una raccolta di valori. Un esempio di operazione di aggregazione è rappresentato dal calcolo della temperatura media giornaliera dai valori della temperatura giornaliera di un mese.  
  
 Nella figura seguente mostra i risultati di due operazioni di aggregazione diversa in una sequenza di numeri. La prima operazione somma i numeri. La seconda operazione restituisce il valore massimo nella sequenza.  
  
 ![Operazioni di aggregazione LINQ](../../../../csharp/programming-guide/concepts/linq/media/linq_aggregation.png "LINQ_Aggregation")  
  
 Nella sezione seguente sono elencati i metodi di operatore query standard che eseguono operazioni di aggregazione.  
  
## <a name="methods"></a>Metodi  
  
|Nome metodo|Descrizione|Sintassi delle espressioni di Query Visual Basic|Altre informazioni|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|Aggregate|Esegue un'operazione di aggregazione personalizzata sui valori di una raccolta.|Non applicabile.|<xref:System.Linq.Enumerable.Aggregate%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Aggregate%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Aggregate%2A?displayProperty=fullName></xref:System.Linq.Queryable.Aggregate%2A?displayProperty=fullName>|  
|Media|Calcola il valore medio di una raccolta di valori.|`Aggregate … In … Into Average()`|<xref:System.Linq.Enumerable.Average%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Average%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Average%2A?displayProperty=fullName></xref:System.Linq.Queryable.Average%2A?displayProperty=fullName>|  
|Conteggio|Conta gli elementi in una raccolta, facoltativamente, solo gli elementi che soddisfano una funzione di predicato.|`Aggregate … In … Into Count()`|<xref:System.Linq.Enumerable.Count%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Count%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Count%2A?displayProperty=fullName></xref:System.Linq.Queryable.Count%2A?displayProperty=fullName>|  
|LongCount|Conta gli elementi in una raccolta di grandi dimensioni, facoltativamente, solo gli elementi che soddisfano una funzione di predicato.|`Aggregate … In … Into LongCount()`|<xref:System.Linq.Enumerable.LongCount%2A?displayProperty=fullName></xref:System.Linq.Enumerable.LongCount%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.LongCount%2A?displayProperty=fullName></xref:System.Linq.Queryable.LongCount%2A?displayProperty=fullName>|  
|Max|Determina il valore massimo in una raccolta.|`Aggregate … In … Into Max()`|<xref:System.Linq.Enumerable.Max%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Max%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Max%2A?displayProperty=fullName></xref:System.Linq.Queryable.Max%2A?displayProperty=fullName>|  
|Min|Determina il valore minimo in una raccolta.|`Aggregate … In … Into Min()`|<xref:System.Linq.Enumerable.Min%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Min%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Min%2A?displayProperty=fullName></xref:System.Linq.Queryable.Min%2A?displayProperty=fullName>|  
|Sum|Calcola la somma dei valori in una raccolta.|`Aggregate … In … Into Sum()`|<xref:System.Linq.Enumerable.Sum%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Sum%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Sum%2A?displayProperty=fullName></xref:System.Linq.Queryable.Sum%2A?displayProperty=fullName>|  
  
## <a name="query-expression-syntax-examples"></a>Esempi di sintassi delle espressioni di query  
  
### <a name="average"></a>Average  
 Nell'esempio di codice viene illustrato come utilizzare il `Aggregate Into Average` clausola [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per calcolare la temperatura media in una matrice di numeri che rappresentano le temperature.  
  
 [!code-vb[CsLINQAggregating n.&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/aggregation-operations_1.vb)]  
  
### <a name="count"></a>Conteggio  
 Nell'esempio di codice viene illustrato come utilizzare il `Aggregate Into Count` clausola [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per contare il numero di valori in una matrice che sono maggiori o uguali a 80.  
  
 [!code-vb[CsLINQAggregating n.&2;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/aggregation-operations_2.vb)]  
  
### <a name="longcount"></a>LongCount  
 Nell'esempio di codice viene illustrato come utilizzare il `Aggregate Into LongCount` clausola per contare il numero di valori in una matrice.  
  
 [!code-vb[CsLINQAggregating n.&3;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/aggregation-operations_3.vb)]  
  
### <a name="max"></a>Max  
 Nell'esempio di codice viene illustrato come utilizzare il `Aggregate Into Max` clausola per calcolare la temperatura massima in una matrice di numeri che rappresentano le temperature.  
  
 [!code-vb[CsLINQAggregating n.&4;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/aggregation-operations_4.vb)]  
  
### <a name="min"></a>Min  
 Nell'esempio di codice viene illustrato come utilizzare il `Aggregate Into Min` clausola per calcolare la temperatura minima in una matrice di numeri che rappresentano le temperature.  
  
 [!code-vb[CsLINQAggregating n.&5;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/aggregation-operations_5.vb)]  
  
### <a name="sum"></a>Sum  
 Nell'esempio di codice viene illustrato come utilizzare il `Aggregate Into Sum` clausola per calcolare la quantità totale spesa da una matrice di valori che rappresentano le spese.  
  
 [!code-vb[6 CsLINQAggregating](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/aggregation-operations_6.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq></xref:System.Linq>   
 [Cenni preliminari sugli operatori di Query standard (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Clausola Aggregate](../../../../visual-basic/language-reference/queries/aggregate-clause.md)   
 [Procedura: calcolare i valori di colonna in un File di testo CSV (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-compute-column-values-in-a-csv-text-file-linq.md)   
 [Procedura: conteggio, somma o Media di dati](../../../../visual-basic/programming-guide/language-features/linq/how-to-count-sum-or-average-data-by-using-linq.md)   
 [Procedura: trovare il valore minimo o massimo in un risultato di Query](../../../../visual-basic/programming-guide/language-features/linq/how-to-find-the-minimum-or-maximum-value-in-a-query-result.md)   
 [Procedura: eseguire una Query per il più grande o più file in una struttura di Directory (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-for-the-largest-file-or-files-in-a-directory-tree.md)   
 [Procedura: eseguire una Query per il numero totale di byte in un Set di cartelle (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-for-the-total-number-of-bytes-in-a-set-of-folders.md)
