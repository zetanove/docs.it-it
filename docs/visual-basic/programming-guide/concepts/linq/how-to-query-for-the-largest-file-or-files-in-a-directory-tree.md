---
title: "Procedura: eseguire una Query per il più grande o più file in una struttura di Directory (LINQ) (Visual Basic) | Documenti di Microsoft"
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
ms.assetid: 8c1c9f0c-95dd-4222-9be2-9ec026a13e81
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
ms.openlocfilehash: 055cbdd5a5903417ab382d390e1215f0319c0b5a
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-query-for-the-largest-file-or-files-in-a-directory-tree-linq-visual-basic"></a>Procedura: eseguire una query per trovare il file o i file più grandi in un albero di directory (LINQ) (Visual Basic)
Questo esempio mostra cinque query relative alle dimensioni del file in byte:  
  
-   Come recuperare la dimensione in byte del file più grande.  
  
-   Come recuperare la dimensione in byte del file più piccolo.  
  
-   Come recuperare il <xref:System.IO.FileInfo>file più grande o più piccolo dell'oggetto da uno o più cartelle in una cartella radice specificata.</xref:System.IO.FileInfo>  
  
-   Come recuperare una sequenza, ad esempio i file di dimensioni maggiori di 10.  
  
-   Come ordinare i file in gruppi in base alle dimensioni in byte, ignorando i file che sono minori dimensioni specificate.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente contiene cinque query distinte che illustrano come eseguire una query e i file di gruppo, in base alle dimensioni in byte. È possibile modificare con facilità questi esempi per basare la query su un'altra proprietà del <xref:System.IO.FileInfo>oggetto.</xref:System.IO.FileInfo>  
  
```vb  
Module QueryBySize  
    Sub Main()  
  
        ' Change the drive\path if necessary  
        Dim root As String = "C:\Program Files\Microsoft Visual Studio 9.0"  
  
        'Take a snapshot of the folder contents  
        Dim dir As New System.IO.DirectoryInfo(root)  
        Dim fileList = dir.GetFiles("*.*", System.IO.SearchOption.AllDirectories)  
  
        ' Return the size of the largest file  
        Dim maxSize = Aggregate aFile In fileList Into Max(GetFileLength(aFile))  
  
        'Dim maxSize = fileLengths.Max  
        Console.WriteLine("The length of the largest file under {0} is {1}", _  
                          root, maxSize)  
  
        ' Return the FileInfo object of the largest file  
        ' by sorting and selecting from the beginning of the list  
        Dim filesByLengDesc = From file In fileList _  
                              Let filelength = GetFileLength(file) _  
                              Where filelength > 0 _  
                              Order By filelength Descending _  
                              Select file  
  
        Dim longestFile = filesByLengDesc.First  
  
        Console.WriteLine("The largest file under {0} is {1} with a length of {2} bytes", _  
                          root, longestFile.FullName, longestFile.Length)  
  
        Dim smallestFile = filesByLengDesc.Last  
  
        Console.WriteLine("The smallest file under {0} is {1} with a length of {2} bytes", _  
                                root, smallestFile.FullName, smallestFile.Length)  
  
        ' Return the FileInfos for the 10 largest files  
        ' Based on a previous query, but nothing is executed  
        ' until the For Each statement below.  
        Dim tenLargest = From file In filesByLengDesc Take 10  
  
        Console.WriteLine("The 10 largest files under {0} are:", root)  
  
        For Each fi As System.IO.FileInfo In tenLargest  
            Console.WriteLine("{0}: {1} bytes", fi.FullName, fi.Length)  
        Next  
  
        ' Group files according to their size,  
        ' leaving out the ones under 200K  
        Dim sizeGroups = From file As System.IO.FileInfo In fileList _  
                         Where file.Length > 0 _  
                         Let groupLength = file.Length / 100000 _  
                         Group file By groupLength Into fileGroup = Group _  
                         Where groupLength >= 2 _  
                         Order By groupLength Descending  
  
        For Each group In sizeGroups  
            Console.WriteLine(group.groupLength + "00000")  
  
            For Each item As System.IO.FileInfo In group.fileGroup  
                Console.WriteLine("   {0}: {1}", item.Name, item.Length)  
            Next  
        Next  
  
        ' Keep the console window open in debug mode  
        Console.WriteLine("Press any key to exit.")  
        Console.ReadKey()  
  
    End Sub  
  
    ' This method is used to catch the possible exception  
    ' that can be raised when accessing the FileInfo.Length property.  
    ' In this particular case, it is safe to ignore the exception.  
    Function GetFileLength(ByVal fi As System.IO.FileInfo) As Long  
        Dim retval As Long  
        Try  
            retval = fi.Length  
        Catch ex As FileNotFoundException  
            ' If a file is no longer present,  
            ' just return zero bytes.   
            retval = 0  
        End Try  
  
        Return retval  
    End Function  
End Module  
```  
  
 Per restituire uno o più completare <xref:System.IO.FileInfo>oggetti, la query deve prima esaminare ciascuno di essi nei dati di origine e poi ordinarli in base al valore della proprietà Length.</xref:System.IO.FileInfo> Può quindi restituire il singolo oggetto o la sequenza con le lunghezze maggiori. Utilizzare <xref:System.Linq.Enumerable.First%2A>per restituire il primo elemento in un elenco.</xref:System.Linq.Enumerable.First%2A> Utilizzare <xref:System.Linq.Enumerable.Take%2A>per restituire il primo numero n di elementi.</xref:System.Linq.Enumerable.Take%2A> Specificare un ordinamento decrescente per inserire gli elementi più piccoli all'inizio dell'elenco.  
  
 La query effettua a un metodo separato per ottenere le dimensioni del file in byte per gestire una possibile eccezione generata nel caso in cui è stato eliminato un file in un altro thread nel periodo di tempo dopo il <xref:System.IO.FileInfo>è stato creato l'oggetto nella chiamata a `GetFiles`.</xref:System.IO.FileInfo> Anche il <xref:System.IO.FileInfo>oggetto è già stato creato, l'eccezione può verificarsi perché un <xref:System.IO.FileInfo>oggetto tenta di aggiornare il relativo <xref:System.IO.FileInfo.Length%2A>proprietà utilizzando la dimensione più corrente in byte la prima volta che si accede alla proprietà.</xref:System.IO.FileInfo.Length%2A> </xref:System.IO.FileInfo> </xref:System.IO.FileInfo> Inserendo questa operazione in un blocco try-catch all'esterno della query, si seguita la regola di evitare operazioni di query che possono causare effetti collaterali. In generale, è necessario prestare particolare attenzione durante l'utilizzo di eccezioni, per assicurarsi che un'applicazione non viene lasciata in uno stato sconosciuto.  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Creare un progetto destinato a .NET Framework versione 3.5 o versione successiva con un riferimento a System.Core.dll e una `Imports` istruzione per lo spazio dei nomi System. Linq.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to Objects (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)   
 [Directory di File (Visual Basic) e LINQ](../../../../visual-basic/programming-guide/concepts/linq/linq-and-file-directories.md)
