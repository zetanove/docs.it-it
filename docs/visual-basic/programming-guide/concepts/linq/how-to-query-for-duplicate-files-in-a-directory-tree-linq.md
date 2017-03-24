---
title: 'Procedura: eseguire una Query per i file duplicati in una struttura di Directory (LINQ) (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 387d7c97-95dd-4a50-9761-7e9cf8ae9e6a
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
ms.openlocfilehash: 9773f1fc5a17957cb77a0f14e12a2f61e67d73c3
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-query-for-duplicate-files-in-a-directory-tree-linq-visual-basic"></a>Procedura: eseguire una Query per i file duplicati in una struttura di Directory (LINQ) (Visual Basic)
Talvolta i file con lo stesso nome possono trovarsi in più di una cartella. Ad esempio, nella cartella di installazione di Visual Studio, diverse cartelle dispongano di un file Readme. htm. In questo esempio viene illustrato come eseguire una query per tali nomi file duplicati in una cartella radice specificata. Nel secondo esempio viene illustrato come eseguire una query per i file le cui dimensioni e ora di creazione uguali.  
  
## <a name="example"></a>Esempio  
  
```vb  
Module QueryDuplicateFileNames  
  
    Public Sub Main()  
  
        Dim path As String = "C:\Program Files\Microsoft Visual Studio 9.0\Common7"  
        QueryDuplicates1(path)  
        ' Uncomment to run this query instead  
        ' QueryDuplicates2(path)  
  
    End Sub  
    Sub QueryDuplicates1(ByVal root As String)  
        Dim dir As New System.IO.DirectoryInfo(root)  
        Dim duplicates = From aFile In dir.GetFiles("*.*", System.IO.SearchOption.AllDirectories) _  
                                 Order By aFile.Name _  
                                 Group aFile By aFile.Name Into newGroup = Group _  
                                 Where newGroup.Count() >= 2 _  
                                 Select newGroup  
  
        ' Page the display so that the results can be read.  
        Dim trimLength = root.Length  
        PageOutput(duplicates, trimLength)  
  
    End Sub  
    Sub QueryDuplicates2(ByVal root As String)  
  
        ' This time a composite key is used. This sub finds all files  
        ' that have been copied into multiple subfolders.  
        Dim dir As New System.IO.DirectoryInfo(root)  
  
        Dim duplicates = From aFile In Dir.GetFiles("*.*", System.IO.SearchOption.AllDirectories) _  
                                 Order By aFile.Name _  
                                 Group aFile By aFile.Name, aFile.CreationTime, aFile.Length Into newGroup = Group _  
                                 Where newGroup.Count() >= 2 _  
                                 Select newGroup  
  
        ' Page the display so that the results can be read.  
        Dim trimLength = root.Length  
        PageOutput(duplicates, trimLength)  
  
    End Sub  
    ' Pages console diplay for large query results. No more than one group per page.  
    ' This sub specifically works with group queries of FileInfo objects  
    ' but can be modified for any type.  
    Sub PageOutput(ByVal groupQuery, ByVal charsToSkip)  
  
        ' "3" = 1 line for extension key + 1 for "Press any key" + 1 for input cursor.  
        Dim numLines As Integer = Console.WindowHeight - 3  
        ' Flag to indicate whether there are more results to diplay  
        Dim goAgain As Boolean = True  
  
        For Each fg As IEnumerable(Of System.IO.FileInfo) In groupQuery  
            ' Start a new extension at the top of a page.  
            Dim currentLine As Integer = 0  
  
            Do While (currentLine < fg.Count())  
                Console.Clear()  
  
                ' Get the next page of results  
                ' No more than one filename per page  
                Dim resultPage = From file In fg _  
                                Skip currentLine Take numLines  
  
                ' Execute the query. Trim the paths in the output.  
                For Each line In resultPage  
                    Console.WriteLine(vbTab & line.FullName.Substring(charsToSkip))  
                Next  
  
                ' Advance the current position  
                currentLine = numLines + currentLine  
  
                ' Give the user a chance to break out of the loop  
                Console.WriteLine("Press any key for next page or the 'End' key to exit.")  
                Dim key As ConsoleKey = Console.ReadKey().Key  
                If key = ConsoleKey.End Then  
                    goAgain = False  
                    Exit For  
                End If  
            Loop  
        Next  
    End Sub  
End Module  
```  
  
 La prima query utilizza una chiave semplice per determinare una corrispondenza. Consente di trovare i file che hanno lo stesso nome ma il cui contenuto potrebbe essere diverso. La seconda query utilizza una chiave composta per la corrispondenza con tre proprietà del <xref:System.IO.FileInfo>oggetto.</xref:System.IO.FileInfo> Questa query è molto più probabile trovare i file con lo stesso nome e un contenuto simile o identico.  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Creare un progetto destinato a .NET Framework versione 3.5 o versione successiva con un riferimento a System.Core.dll e una `Imports` istruzione per lo spazio dei nomi System. Linq.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to Objects (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)   
 [Directory di File (Visual Basic) e LINQ](../../../../visual-basic/programming-guide/concepts/linq/linq-and-file-directories.md)
