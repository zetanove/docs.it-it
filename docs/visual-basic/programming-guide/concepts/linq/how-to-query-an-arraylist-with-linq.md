---
title: 'Procedura: eseguire Query su un ArrayList con LINQ (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 176358a9-d765-4b57-9557-7feb4428138d
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
ms.openlocfilehash: f48b06c23b1e28fccb953638954a8d9afefe574e
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-query-an-arraylist-with-linq-visual-basic"></a>Procedura: eseguire Query su un ArrayList con LINQ (Visual Basic)
Quando si utilizza LINQ per non query generica <xref:System.Collections.IEnumerable>raccolte, ad esempio <xref:System.Collections.ArrayList>, è necessario dichiarare in modo esplicito il tipo della variabile di intervallo in base al tipo specifico di oggetti nella raccolta.</xref:System.Collections.ArrayList> </xref:System.Collections.IEnumerable> Ad esempio, se si dispone di un <xref:System.Collections.ArrayList>di `Student` oggetti, il [dalla clausola](../../../../visual-basic/language-reference/queries/from-clause.md) dovrebbe essere simile al seguente:</xref:System.Collections.ArrayList>  
  
```  
  
Dim query = From student As Student In arrList   
...  
  
```  
  
 Specificando il tipo della variabile di intervallo, si esegue il cast di ogni elemento di <xref:System.Collections.ArrayList>per un `Student`.</xref:System.Collections.ArrayList>  
  
 L'utilizzo di una variabile di intervallo tipizzata in modo esplicito in un'espressione di query è equivalente alla chiamata di <xref:System.Linq.Enumerable.Cast%2A>(metodo).</xref:System.Linq.Enumerable.Cast%2A> <xref:System.Linq.Enumerable.Cast%2A>genera un'eccezione se non è possibile eseguire il cast specificato.</xref:System.Linq.Enumerable.Cast%2A> <xref:System.Linq.Enumerable.Cast%2A>e <xref:System.Linq.Enumerable.OfType%2A>sono i due metodi di operatore di Query Standard che operano su non generica <xref:System.Collections.IEnumerable>tipi.</xref:System.Collections.IEnumerable> </xref:System.Linq.Enumerable.OfType%2A></xref:System.Linq.Enumerable.Cast%2A> In Visual Basic, è necessario chiamare esplicitamente il <xref:System.Linq.Enumerable.Cast%2A>metodo sull'origine dati per garantire un tipo di variabile di intervallo specifico.</xref:System.Linq.Enumerable.Cast%2A> Per ulteriori informazioni, vedere[relazioni tra i tipi nelle operazioni di Query (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/type-relationships-in-query-operations.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrata una semplice query su un <xref:System.Collections.ArrayList>.</xref:System.Collections.ArrayList> Si noti che in questo esempio utilizza gli inizializzatori di oggetto quando il codice chiama il <xref:System.Collections.ArrayList.Add%2A>(metodo), ma questo non è un requisito.</xref:System.Collections.ArrayList.Add%2A>  
  
```vb  
Imports System.Collections  
Imports System.Linq  
  
Module Module1  
  
    Public Class Student  
        Public Property FirstName As String  
        Public Property LastName As String  
        Public Property Scores As Integer()  
    End Class  
  
    Sub Main()  
  
        Dim student1 As New Student With {.FirstName = "Svetlana",   
                                     .LastName = "Omelchenko",   
                                     .Scores = New Integer() {98, 92, 81, 60}}  
        Dim student2 As New Student With {.FirstName = "Claire",   
                                    .LastName = "O'Donnell",   
                                    .Scores = New Integer() {75, 84, 91, 39}}  
        Dim student3 As New Student With {.FirstName = "Cesar",   
                                    .LastName = "Garcia",   
                                    .Scores = New Integer() {97, 89, 85, 82}}  
        Dim student4 As New Student With {.FirstName = "Sven",   
                                    .LastName = "Mortensen",   
                                    .Scores = New Integer() {88, 94, 65, 91}}  
  
        Dim arrList As New ArrayList()  
        arrList.Add(student1)  
        arrList.Add(student2)  
        arrList.Add(student3)  
        arrList.Add(student4)  
  
        ' Use an explicit type for non-generic collections  
        Dim query = From student As Student In arrList   
                    Where student.Scores(0) > 95   
                    Select student  
  
        For Each student As Student In query  
            Console.WriteLine(student.LastName & ": " & student.Scores(0))  
        Next  
        ' Keep the console window open in debug mode.  
        Console.WriteLine("Press any key to exit.")  
        Console.ReadKey()  
    End Sub  
  
End Module  
' Output:  
'   Omelchenko: 98  
'   Garcia: 97  
```  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to Objects (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)
