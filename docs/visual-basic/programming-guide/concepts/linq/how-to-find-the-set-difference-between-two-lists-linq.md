---
title: 'Procedura: trovare la differenza dei Set tra due elenchi (LINQ) (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: b5b25474-10a8-4df6-aab5-75621bb6b68e
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
ms.openlocfilehash: e2e67a03d5826d7d93e04b6c20a09cbbcabc8629
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-find-the-set-difference-between-two-lists-linq-visual-basic"></a>Procedura: trovare la differenza dei Set tra due elenchi (LINQ) (Visual Basic)
In questo esempio viene illustrato come utilizzare LINQ per confrontare due elenchi di stringhe e restituire le righe presenti in names1. txt, ma non in names2.  
  
### <a name="to-create-the-data-files"></a>Per creare i file di dati  
  
1.  Copiare names1. txt e names2. txt nella cartella della soluzione come illustrato nella [procedura: combinare e confrontare stringhe raccolte (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-combine-and-compare-string-collections-linq.md).  
  
## <a name="example"></a>Esempio  
  
```vb  
Class CompareLists  
  
    Shared Sub Main()  
  
        ' Create the IEnumerable data sources.  
        Dim names1 As String() = System.IO.File.ReadAllLines("../../../names1.txt")  
        Dim names2 As String() = System.IO.File.ReadAllLines("../../../names2.txt")  
  
        ' Create the query. Note that method syntax must be used here.  
        Dim differenceQuery = names1.Except(names2)  
        Console.WriteLine("The following lines are in names1.txt but not names2.txt")  
  
        ' Execute the query.  
        For Each name As String In differenceQuery  
            Console.WriteLine(name)  
        Next  
  
        ' Keep console window open in debug mode.  
        Console.WriteLine("Press any key to exit.")  
        Console.ReadKey()  
    End Sub  
End Class  
' Output:  
' The following lines are in names1.txt but not names2.txt  
' Potra, Cristina  
' Noriega, Fabricio  
' Aw, Kam Foo  
' Toyoshima, Tim  
' Guy, Wey Yuan  
' Garcia, Debra  
```  
  
 Alcuni tipi di query operazioni in Visual Basic, ad esempio <xref:System.Linq.Enumerable.Except%2A>, <xref:System.Linq.Enumerable.Distinct%2A>, <xref:System.Linq.Enumerable.Union%2A>, e <xref:System.Linq.Enumerable.Concat%2A>, può essere espresso solo nella sintassi delle query basate su metodo.</xref:System.Linq.Enumerable.Concat%2A> </xref:System.Linq.Enumerable.Union%2A> </xref:System.Linq.Enumerable.Distinct%2A> </xref:System.Linq.Enumerable.Except%2A>  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Creare un progetto destinato a .NET Framework versione 3.5 o versione successiva con un riferimento a System.Core.dll e una `Imports` istruzione per lo spazio dei nomi System. Linq.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ e stringhe (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)
