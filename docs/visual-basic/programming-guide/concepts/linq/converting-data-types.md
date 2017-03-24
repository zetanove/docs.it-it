---
title: Conversione di tipi di dati (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 9b0cf1ab-de48-4c6e-9f00-05b40fade46e
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
ms.openlocfilehash: 53d8ad292891a567e13ec8a5396bcc114b379351
ms.lasthandoff: 03/13/2017

---
# <a name="converting-data-types-visual-basic"></a>La conversione dei tipi di dati (Visual Basic)
Metodi di conversione modificano il tipo di oggetti di input.  
  
 Le operazioni di conversione nelle query LINQ sono utili in un'ampia gamma di applicazioni. Di seguito sono riportati alcuni esempi:  
  
-   Il <xref:System.Linq.Enumerable.AsEnumerable%2A?displayProperty=fullName>metodo può essere utilizzato per nascondere l'implementazione personalizzata di un tipo di un operatore di query standard.</xref:System.Linq.Enumerable.AsEnumerable%2A?displayProperty=fullName>  
  
-   Il <xref:System.Linq.Enumerable.OfType%2A?displayProperty=fullName>metodo può essere utilizzato per abilitare le raccolte senza parametri per l'esecuzione di query LINQ.</xref:System.Linq.Enumerable.OfType%2A?displayProperty=fullName>  
  
-   Il <xref:System.Linq.Enumerable.ToArray%2A?displayProperty=fullName>, <xref:System.Linq.Enumerable.ToDictionary%2A?displayProperty=fullName>, <xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName>, e <xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=fullName>possono essere utilizzati per forzare l'esecuzione immediata della query anziché rinviare, fino a che la query viene enumerata.</xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=fullName> </xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName> </xref:System.Linq.Enumerable.ToDictionary%2A?displayProperty=fullName> </xref:System.Linq.Enumerable.ToArray%2A?displayProperty=fullName>  
  
## <a name="methods"></a>Metodi  
 Nella tabella seguente sono elencati i metodi di operatore di query standard che eseguono conversioni di tipi di dati.  
  
 I metodi di conversione in questa tabella i cui nomi iniziano con "As" modificano il tipo statico dell'insieme di origine ma non lo enumerano. Digitare i metodi i cui nomi iniziano con "A enumerare la raccolta di origine e inserire gli elementi nella raccolta corrispondente".  
  
|Nome metodo|Descrizione|Sintassi delle espressioni di Query Visual Basic|Altre informazioni|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|AsEnumerable|Restituisce l'input digitato come <xref:System.Collections.Generic.IEnumerable%601>.</xref:System.Collections.Generic.IEnumerable%601>|Non applicabile.|<xref:System.Linq.Enumerable.AsEnumerable%2A?displayProperty=fullName></xref:System.Linq.Enumerable.AsEnumerable%2A?displayProperty=fullName>|  
|AsQueryable|Converte un (generici) <xref:System.Collections.IEnumerable>in un <xref:System.Linq.IQueryable>.</xref:System.Linq.IQueryable> (generico)</xref:System.Collections.IEnumerable>|Non applicabile.|<xref:System.Linq.Queryable.AsQueryable%2A?displayProperty=fullName></xref:System.Linq.Queryable.AsQueryable%2A?displayProperty=fullName>|  
|Cast|Esegue il cast di elementi di una raccolta in un tipo specificato.|`From … As …`|<xref:System.Linq.Enumerable.Cast%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Cast%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Cast%2A?displayProperty=fullName></xref:System.Linq.Queryable.Cast%2A?displayProperty=fullName>|  
|OfType|Filtra i valori, a seconda della loro capacità di eseguire il cast a un tipo specificato.|Non applicabile.|<xref:System.Linq.Enumerable.OfType%2A?displayProperty=fullName></xref:System.Linq.Enumerable.OfType%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.OfType%2A?displayProperty=fullName></xref:System.Linq.Queryable.OfType%2A?displayProperty=fullName>|  
|ToArray|Converte una raccolta in una matrice. Questo metodo impone l'esecuzione di query.|Non applicabile.|<xref:System.Linq.Enumerable.ToArray%2A?displayProperty=fullName></xref:System.Linq.Enumerable.ToArray%2A?displayProperty=fullName>|  
|ToDictionary|Inserisce gli elementi in un <xref:System.Collections.Generic.Dictionary%602>in base a una funzione selettore di chiave.</xref:System.Collections.Generic.Dictionary%602> Questo metodo impone l'esecuzione di query.|Non applicabile.|<xref:System.Linq.Enumerable.ToDictionary%2A?displayProperty=fullName></xref:System.Linq.Enumerable.ToDictionary%2A?displayProperty=fullName>|  
|ToList|Converte una raccolta a un <xref:System.Collections.Generic.List%601>.</xref:System.Collections.Generic.List%601> Questo metodo impone l'esecuzione di query.|Non applicabile.|<xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName></xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName>|  
|ToLookup|Inserisce gli elementi in un <xref:System.Linq.Lookup%602>(un dizionario uno-a-molti) in base a una funzione selettore di chiave.</xref:System.Linq.Lookup%602> Questo metodo impone l'esecuzione di query.|Non applicabile.|<xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=fullName></xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=fullName>|  
  
## <a name="query-expression-syntax-example"></a>Esempio di sintassi di espressione di query  
 Nell'esempio di codice viene illustrato come utilizzare il `From As` clausola per eseguire il cast di un tipo a un sottotipo prima di accedere a un membro che è disponibile solo nel sottotipo.  
  
```vb  
Class Plant  
    Public Property Name As String  
End Class  
  
Class CarnivorousPlant  
    Inherits Plant  
    Public Property TrapType As String  
End Class  
  
Sub Cast()  
  
    Dim plants() As Plant = {   
        New CarnivorousPlant With {.Name = "Venus Fly Trap", .TrapType = "Snap Trap"},   
        New CarnivorousPlant With {.Name = "Pitcher Plant", .TrapType = "Pitfall Trap"},   
        New CarnivorousPlant With {.Name = "Sundew", .TrapType = "Flypaper Trap"},   
        New CarnivorousPlant With {.Name = "Waterwheel Plant", .TrapType = "Snap Trap"}}  
  
    Dim query = From plant As CarnivorousPlant In plants   
                Where plant.TrapType = "Snap Trap"   
                Select plant  
  
    Dim sb As New System.Text.StringBuilder()  
    For Each plant In query  
        sb.AppendLine(plant.Name)  
    Next  
  
    ' Display the results.  
    MsgBox(sb.ToString())  
  
    ' This code produces the following output:  
  
    ' Venus Fly Trap  
    ' Waterwheel Plant  
  
End Sub  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq></xref:System.Linq>   
 [Cenni preliminari sugli operatori di Query standard (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Clausola FROM](../../../../visual-basic/language-reference/queries/from-clause.md)   
 [Procedura: eseguire Query su un ArrayList con LINQ (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md)
