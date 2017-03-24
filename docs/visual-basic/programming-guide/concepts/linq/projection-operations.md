---
title: Operazioni di proiezione (Visual Basic) | Documenti di Microsoft
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
ms.assetid: b8d38e6d-21cf-4619-8dbb-94476f4badc7
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
ms.openlocfilehash: 8876e65e752e0b18404ec32aecdcad7805533840
ms.lasthandoff: 03/13/2017

---
# <a name="projection-operations-visual-basic"></a>Operazioni di proiezione (Visual Basic)
Proiezione si riferisce all'operazione di trasformazione di un oggetto in un nuovo form che spesso costituita solo le proprietà che verranno utilizzate successivamente. Utilizzando la proiezione, è possibile costruire un nuovo tipo compilato in base a ogni oggetto. È possibile proiettare una proprietà ed eseguire una funzione matematica su di esso. È inoltre possibile proiettare l'oggetto originale senza modificarlo.  
  
 Nella sezione seguente sono elencati i metodi dell'operatore query standard che eseguono la proiezione.  
  
## <a name="methods"></a>Metodi  
  
|Nome metodo|Descrizione|Sintassi delle espressioni di Query Visual Basic|Altre informazioni|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|Seleziona|Valori di progetti basati su una funzione di trasformazione.|`Select`|<xref:System.Linq.Enumerable.Select%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Select%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Select%2A?displayProperty=fullName></xref:System.Linq.Queryable.Select%2A?displayProperty=fullName>|  
|SelectMany|Proietta le sequenze di valori che si basano su una funzione di trasformazione e quindi li converte in un'unica sequenza.|Utilizzare più `From` clausole|<xref:System.Linq.Enumerable.SelectMany%2A?displayProperty=fullName></xref:System.Linq.Enumerable.SelectMany%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.SelectMany%2A?displayProperty=fullName></xref:System.Linq.Queryable.SelectMany%2A?displayProperty=fullName>|  
  
## <a name="query-expression-syntax-examples"></a>Esempi di sintassi delle espressioni di query  
  
### <a name="select"></a>Seleziona  
 Nell'esempio seguente viene utilizzata la `Select` clausola per la prima lettera di ogni stringa in un elenco di stringhe del progetto.  
  
```vb  
Dim words = New List(Of String) From {"an", "apple", "a", "day"}  
  
Dim query = From word In words   
            Select word.Substring(0, 1)  
  
Dim sb As New System.Text.StringBuilder()  
For Each letter As String In query  
    sb.AppendLine(letter)  
Next  
  
' Display the output.  
MsgBox(sb.ToString())  
  
' This code produces the following output:  
  
' a  
' a  
' a  
' d  
```  
  
### <a name="selectmany"></a>SelectMany  
 Nell'esempio seguente usa più `From` clausole per ogni parola di ogni stringa in un elenco di stringhe del progetto.  
  
```vb  
Dim phrases = New List(Of String) From {"an apple a day", "the quick brown fox"}  
  
Dim query = From phrase In phrases   
            From word In phrase.Split(" "c)   
            Select word  
  
Dim sb As New System.Text.StringBuilder()  
For Each str As String In query  
    sb.AppendLine(str)  
Next  
  
' Display the output.  
MsgBox(sb.ToString())  
  
' This code produces the following output:  
  
' an  
' apple  
' a  
' day  
' the  
' quick  
' brown  
' fox  
```  
  
## <a name="select-versus-selectmany"></a>Selezionare e SelectMany  
 La funzione di `Select()` e `SelectMany()` consiste nel produrre un valore di risultato (o valori) dai valori di origine. `Select()`produce un valore per ogni valore di origine. Il risultato complessivo è pertanto una raccolta con lo stesso numero di elementi della raccolta di origine. Al contrario, `SelectMany()` produce un unico risultato complessivo che contiene sottoraccolte concatenate di ogni valore di origine. La funzione di trasformazione che viene passata come argomento `SelectMany()` deve restituire una sequenza enumerabile di valori per ogni valore di origine. Queste sequenze enumerabili vengono quindi concatenate da `SelectMany()` per creare una sequenza di grandi dimensioni.  
  
 Nelle due figure seguenti mostrano la differenza tra le azioni di questi due metodi. In ogni caso, si supponga che la funzione del selettore (transform) consente di selezionare la matrice di fiori da ogni valore di origine.  
  
 Questa figura viene illustrato come `Select()` restituisce una raccolta con lo stesso numero di elementi della raccolta di origine.  
  
 ![Illustrazione concettuale dell'azione di Select ()](../../../../csharp/programming-guide/concepts/linq/media/selectaction.png "SelectAction")  
  
 Questa figura viene illustrato come `SelectMany()` concatena la sequenza intermedia di matrici in un unico valore finale che contiene ogni valore di ogni matrice intermedia.  
  
 ![Rappresentazione grafica dell'azione di SelectMany (). ] (../../../../csharp/programming-guide/concepts/linq/media/selectmany.png "SelectMany")  
  
### <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente viene confrontato il comportamento di `Select()` e `SelectMany()`. Il codice crea un "bouquet" di fiori prendendo i primi due elementi di ogni elenco di nomi di fiori nella raccolta di origine. In questo esempio, "singolo valore" che la funzione di trasformazione <xref:System.Linq.Enumerable.Select%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>è essa stessa una raccolta di valori.</xref:System.Linq.Enumerable.Select%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29> Questa operazione richiede aggiuntivo `For Each` ciclo per enumerare tutte le stringhe ogni sottosequenza.  
  
```vb  
Class Bouquet  
    Public Flowers As List(Of String)  
End Class  
  
Sub SelectVsSelectMany()  
    Dim bouquets = New List(Of Bouquet) From {   
        New Bouquet With {.Flowers = New List(Of String)(New String() {"sunflower", "daisy", "daffodil", "larkspur"})},   
        New Bouquet With {.Flowers = New List(Of String)(New String() {"tulip", "rose", "orchid"})},   
        New Bouquet With {.Flowers = New List(Of String)(New String() {"gladiolis", "lily", "snapdragon", "aster", "protea"})},   
        New Bouquet With {.Flowers = New List(Of String)(New String() {"larkspur", "lilac", "iris", "dahlia"})}}  
  
    Dim output As New System.Text.StringBuilder  
  
    ' Select()  
    Dim query1 = bouquets.Select(Function(b) b.Flowers)  
  
    output.AppendLine("Using Select():")  
    For Each flowerList In query1  
        For Each str As String In flowerList  
            output.AppendLine(str)  
        Next  
    Next  
  
    ' SelectMany()  
    Dim query2 = bouquets.SelectMany(Function(b) b.Flowers)  
  
    output.AppendLine(vbCrLf & "Using SelectMany():")  
    For Each str As String In query2  
        output.AppendLine(str)  
    Next  
  
    ' Display the output  
    MsgBox(output.ToString())  
  
    ' This code produces the following output:  
    '  
    ' Using Select():  
    ' sunflower  
    ' daisy  
    ' daffodil  
    ' larkspur  
    ' tulip  
    ' rose  
    ' orchid  
    ' gladiolis  
    ' lily  
    ' snapdragon  
    ' aster  
    ' protea  
    ' larkspur  
    ' lilac  
    ' iris  
    ' dahlia  
  
    ' Using SelectMany()  
    ' sunflower  
    ' daisy  
    ' daffodil  
    ' larkspur  
    ' tulip  
    ' rose  
    ' orchid  
    ' gladiolis  
    ' lily  
    ' snapdragon  
    ' aster  
    ' protea  
    ' larkspur  
    ' lilac  
    ' iris  
    ' dahlia  
  
End Sub  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq></xref:System.Linq>   
 [Cenni preliminari sugli operatori di Query standard (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Clausola SELECT](../../../../visual-basic/language-reference/queries/select-clause.md)   
 [Procedura: combinare dati utilizzando join](../../../../visual-basic/programming-guide/language-features/linq/how-to-combine-data-with-linq-by-using-joins.md)   
 [Procedura: popolare raccolte di oggetti da più origini (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-populate-object-collections-from-multiple-sources-linq.md)   
 [Procedura: restituire un risultato di Query LINQ come tipo specifico](../../../../visual-basic/programming-guide/language-features/linq/how-to-return-a-linq-query-result-as-a-specific-type.md)   
 [Procedura: suddividere un File in molti file utilizzando i gruppi (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-split-a-file-into-many-files-by-using-groups-linq.md)
