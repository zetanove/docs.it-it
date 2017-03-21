---
title: Partizionamento dei dati (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 69c59379-b66e-422c-b324-5b5c07760ef7
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
ms.openlocfilehash: a746ce3e24812d1df6b6e221cca0364bf2cc7f1c
ms.lasthandoff: 03/13/2017

---
# <a name="partitioning-data-visual-basic"></a>Partizionamento dei dati (Visual Basic)
Il partizionamento in LINQ si riferisce all'operazione di divisione di una sequenza di input in due sezioni, senza ridisporre gli elementi e restituendo quindi una delle sezioni.  
  
 Nella figura seguente mostra i risultati di tre diverse operazioni di partizionamento su una sequenza di caratteri. La prima operazione restituisce i primi tre elementi nella sequenza. La seconda operazione ignora i primi tre elementi e restituisce gli elementi rimanenti. La terza operazione ignora i primi due elementi nella sequenza e restituisce i tre elementi successivi.  
  
 ![Operazioni di partizionamento LINQ](../../../../csharp/programming-guide/concepts/linq/media/linq_partition.png "LINQ_Partition")  
  
 Nella sezione seguente sono elencati i metodi degli operatori query standard che le sequenze di partizione.  
  
## <a name="operators"></a>Operatori  
  
|Nome dell'operatore|Descrizione|Sintassi delle espressioni di Query Visual Basic|Altre informazioni|  
|-------------------|-----------------|------------------------------------------|----------------------|  
|Skip|Ignora gli elementi fino a una posizione specificata in una sequenza.|`Skip`|<xref:System.Linq.Enumerable.Skip%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Skip%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Skip%2A?displayProperty=fullName></xref:System.Linq.Queryable.Skip%2A?displayProperty=fullName>|  
|SkipWhile|Ignora gli elementi basati su una funzione predicativa finché un elemento non soddisfa la condizione.|`Skip While`|<xref:System.Linq.Enumerable.SkipWhile%2A?displayProperty=fullName></xref:System.Linq.Enumerable.SkipWhile%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.SkipWhile%2A?displayProperty=fullName></xref:System.Linq.Queryable.SkipWhile%2A?displayProperty=fullName>|  
|Take|Accetta gli elementi fino a una posizione specificata in una sequenza.|`Take`|<xref:System.Linq.Enumerable.Take%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Take%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Take%2A?displayProperty=fullName></xref:System.Linq.Queryable.Take%2A?displayProperty=fullName>|  
|TakeWhile|Accetta gli elementi basati su una funzione predicativa finché un elemento non soddisfa la condizione.|`Take While`|<xref:System.Linq.Enumerable.TakeWhile%2A?displayProperty=fullName></xref:System.Linq.Enumerable.TakeWhile%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.TakeWhile%2A?displayProperty=fullName></xref:System.Linq.Queryable.TakeWhile%2A?displayProperty=fullName>|  
  
## <a name="query-expression-syntax-examples"></a>Esempi di sintassi delle espressioni di query  
  
### <a name="skip"></a>Skip  
 Nell'esempio di codice viene illustrato come utilizzare il `Skip` clausola [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per ignorare le prime quattro stringhe in una matrice di stringhe prima di restituire le stringhe rimanenti della matrice.  
  
 [!code-vb[CsLINQPartitioning n.&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/partitioning-data_1.vb)]  
  
### <a name="skipwhile"></a>SkipWhile  
 Nell'esempio di codice viene illustrato come utilizzare il `Skip While` clausola [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per ignorare le stringhe in una matrice durante la prima lettera della stringa è "a". Le stringhe rimanenti della matrice vengono restituite.  
  
 [!code-vb[CsLINQPartitioning n.&2;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/partitioning-data_2.vb)]  
  
### <a name="take"></a>Take  
 Nell'esempio di codice viene illustrato come utilizzare il `Take` clausola [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per restituire le prime due stringhe in una matrice di stringhe.  
  
 [!code-vb[CsLINQPartitioning n.&3;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/partitioning-data_3.vb)]  
  
### <a name="takewhile"></a>TakeWhile  
 Nell'esempio di codice viene illustrato come utilizzare il `Take While` clausola [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per restituire le stringhe da una matrice, mentre la lunghezza della stringa è di cinque o meno.  
  
 [!code-vb[CsLINQPartitioning n.&4;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/partitioning-data_4.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq></xref:System.Linq>   
 [Cenni preliminari sugli operatori di Query standard (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Clausola Skip](../../../../visual-basic/language-reference/queries/skip-clause.md)   
 [Clausola Skip While](../../../../visual-basic/language-reference/queries/skip-while-clause.md)   
 [Clausola Take](../../../../visual-basic/language-reference/queries/take-clause.md)   
 [Clausola Take While](../../../../visual-basic/language-reference/queries/take-while-clause.md)
