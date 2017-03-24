---
title: 'Procedura: combinare query LINQ con espressioni regolari (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 3da1bd10-b0d8-4d5b-a637-966891c13592
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
ms.openlocfilehash: 283b5e844c91da22aadd7bcf88ea327ccc080be7
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-combine-linq-queries-with-regular-expressions-visual-basic"></a>Procedura: combinare query LINQ con espressioni regolari (Visual Basic)
In questo esempio viene illustrato come utilizzare la <xref:System.Text.RegularExpressions.Regex>classe per creare un'espressione regolare per la corrispondenza più complessa nelle stringhe di testo.</xref:System.Text.RegularExpressions.Regex> La query LINQ consente di filtrare esattamente i file che si desidera eseguire la ricerca con espressioni regolari e di elaborare i risultati.  
  
## <a name="example"></a>Esempio  
  
```vb  
Class LinqRegExVB  
  
    Shared Sub Main()  
  
        ' Root folder to query, along with all subfolders.  
        ' Modify this path as necessary so that it accesses your Visual Studio folder.  
        Dim startFolder As String = "C:\program files\Microsoft Visual Studio 9.0\"  
        ' One of the following paths may be more appropriate on your computer.  
        'string startFolder = @"c:\program files (x86)\Microsoft Visual Studio 9.0\";  
        'string startFolder = @"c:\program files\Microsoft Visual Studio 10.0\";  
        'string startFolder = @"c:\program files (x86)\Microsoft Visual Studio 10.0\";  
  
        ' Take a snapshot of the file system.  
        Dim fileList As IEnumerable(Of System.IO.FileInfo) = GetFiles(startFolder)  
  
        ' Create a regular expression to find all things "Visual".  
        Dim searchTerm As System.Text.RegularExpressions.Regex =   
            New System.Text.RegularExpressions.Regex("Visual (Basic|C#|C\+\+|J#|SourceSafe|Studio)")  
  
        ' Search the contents of each .htm file.  
        ' Remove the where clause to find even more matches!  
        ' This query produces a list of files where a match  
        ' was found, and a list of the matches in that file.  
        ' Note: Explicit typing of "Match" in select clause.  
        ' This is required because MatchCollection is not a   
        ' generic IEnumerable collection.  
        Dim queryMatchingFiles = From afile In fileList  
                                Where afile.Extension = ".htm"  
                                Let fileText = System.IO.File.ReadAllText(afile.FullName)  
                                Let matches = searchTerm.Matches(fileText)  
                                Where (matches.Count > 0)  
                                Select Name = afile.FullName,  
                                       Matches = From match As System.Text.RegularExpressions.Match In matches  
                                                 Select match.Value  
  
        ' Execute the query.  
        Console.WriteLine("The term " & searchTerm.ToString() & " was found in:")  
  
        For Each fileMatches In queryMatchingFiles  
            ' Trim the path a bit, then write   
            ' the file name in which a match was found.  
            Dim s = fileMatches.Name.Substring(startFolder.Length - 1)  
            Console.WriteLine(s)  
  
            ' For this file, write out all the matching strings  
            For Each match In fileMatches.Matches  
                Console.WriteLine("  " + match)  
            Next  
        Next  
  
        ' Keep the console window open in debug mode  
        Console.WriteLine("Press any key to exit")  
        Console.ReadKey()  
    End Sub  
  
    ' Function to retrieve a list of files. Note that this is a copy  
    ' of the file information.  
    Shared Function GetFiles(ByVal root As String) As IEnumerable(Of System.IO.FileInfo)  
        Return From file In My.Computer.FileSystem.GetFiles(  
                   root, FileIO.SearchOption.SearchAllSubDirectories, "*.*")   
               Select New System.IO.FileInfo(file)  
    End Function  
  
End Class  
```  
  
 Si noti che è anche possibile eseguire una query di <xref:System.Text.RegularExpressions.MatchCollection>oggetto restituito da un `RegEx` search.</xref:System.Text.RegularExpressions.MatchCollection> In questo esempio viene generato solo il valore di ogni corrispondenza nei risultati. Tuttavia, è anche possibile utilizzare LINQ per eseguire tutti i tipi di filtro, ordinamento e raggruppamento su tale insieme. Poiché <xref:System.Text.RegularExpressions.MatchCollection>è di tipo non generico <xref:System.Collections.IEnumerable>raccolta, è necessario dichiarare in modo esplicito il tipo della variabile di intervallo nella query.</xref:System.Collections.IEnumerable> </xref:System.Text.RegularExpressions.MatchCollection>  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Creare un progetto destinato a .NET Framework versione 3.5 o versione successiva con un riferimento a System.Core.dll e una `Imports` istruzione per lo spazio dei nomi System. Linq.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ e stringhe (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)   
 [Directory di File (Visual Basic) e LINQ](../../../../visual-basic/programming-guide/concepts/linq/linq-and-file-directories.md)
