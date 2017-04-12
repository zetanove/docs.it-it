---
title: 'Procedura: eseguire una Query per il numero totale di byte in un Set di cartelle (LINQ) (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: bfe85ed2-44dc-4ef1-aac7-241622b80a69
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
ms.openlocfilehash: 668a8a4d89f7b81c3aef9b4e1a46ad749c4a8341
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-query-for-the-total-number-of-bytes-in-a-set-of-folders-linq-visual-basic"></a>Procedura: eseguire una Query per il numero totale di byte in un Set di cartelle (LINQ) (Visual Basic)
In questo esempio viene illustrato come recuperare il numero totale di byte utilizzati da tutti i file in una cartella specificata e tutte le relative sottocartelle.  
  
## <a name="example"></a>Esempio  
 Il <xref:System.Linq.Enumerable.Sum%2A>metodo aggiunge i valori di tutti gli elementi selezionati nel `select` clausola.</xref:System.Linq.Enumerable.Sum%2A> È possibile modificare facilmente questa query per recuperare il file più grande o più piccolo nella struttura della directory specificata chiamando il <xref:System.Linq.Enumerable.Min%2A> <xref:System.Linq.Enumerable.Max%2A>metodo anziché <xref:System.Linq.Enumerable.Sum%2A>.</xref:System.Linq.Enumerable.Sum%2A> </xref:System.Linq.Enumerable.Max%2A> o</xref:System.Linq.Enumerable.Min%2A>  
  
```vb  
Module QueryTotalBytes  
    Sub Main()  
  
        ' Change the drive\path if necessary.  
        Dim root As String = "C:\Program Files\Microsoft Visual Studio 9.0\VB"  
  
        'Take a snapshot of the folder contents.  
        ' This method assumes that the application has discovery permissions  
        ' for all folders under the specified path.  
        Dim fileList = My.Computer.FileSystem.GetFiles _  
                  (root, FileIO.SearchOption.SearchAllSubDirectories, "*.*")  
  
        Dim fileQuery = From file In fileList _  
                        Select GetFileLength(file)  
  
        ' Force execution and cache the results to avoid multiple trips to the file system.  
        Dim fileLengths = fileQuery.ToArray()  
  
        ' Find the largest file  
        Dim maxSize = Aggregate aFile In fileLengths Into Max()  
  
        ' Find the total number of bytes  
        Dim totalBytes = Aggregate aFile In fileLengths Into Sum()  
  
        Console.WriteLine("The largest file is " & maxSize & " bytes")  
        Console.WriteLine("There are " & totalBytes & " total bytes in " & _  
                          fileList.Count & " files under " & root)  
  
        ' Keep the console window open in debug mode  
        Console.WriteLine("Press any key to exit.")  
        Console.ReadKey()  
    End Sub  
  
    ' This method is used to catch the possible exception  
    ' that can be raised when accessing the FileInfo.Length property.  
    Function GetFileLength(ByVal filename As String) As Long  
        Dim retval As Long  
        Try  
            Dim fi As New System.IO.FileInfo(filename)  
            retval = fi.Length  
        Catch ex As System.IO.FileNotFoundException  
            ' If a file is no longer present,  
            ' just return zero bytes.   
            retval = 0  
        End Try  
  
        Return retval  
    End Function  
End Module  
```  
  
 Se è sufficiente contare il numero di byte in una struttura ad albero di directory specificata, è possibile farlo in modo più efficiente senza creare una query LINQ, che genera l'overhead della creazione della raccolta di elenco come origine dati. L'utilità dell'approccio LINQ aumenta se la query diventa più complessa, o quando è necessario eseguire più query sulla stessa origine dati.  
  
 La query effettua una chiamata a un metodo separato per ottenere la lunghezza del file. In tal modo di utilizzare la possibile eccezione generata se il file è stato eliminato in un altro thread dopo la <xref:System.IO.FileInfo>è stato creato l'oggetto nella chiamata a `GetFiles`.</xref:System.IO.FileInfo> Anche se il <xref:System.IO.FileInfo>oggetto è già stato creato, l'eccezione può verificarsi perché un <xref:System.IO.FileInfo>oggetto tenta di aggiornare il relativo <xref:System.IO.FileInfo.Length%2A>proprietà con la lunghezza più recente la prima volta che si accede alla proprietà.</xref:System.IO.FileInfo.Length%2A> </xref:System.IO.FileInfo> </xref:System.IO.FileInfo> Inserendo questa operazione in un blocco try-catch all'esterno della query, il codice segue la regola di evitare operazioni di query che possono causare effetti collaterali. In generale, è necessario prestare particolare attenzione quando si usano le eccezioni per assicurarsi che un'applicazione non viene lasciata in uno stato sconosciuto.  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Creare un progetto destinato a .NET Framework versione 3.5 o versione successiva con un riferimento a System.Core.dll e una `Imports` istruzione per lo spazio dei nomi System. Linq.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to Objects (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)   
 [Directory di File (Visual Basic) e LINQ](../../../../visual-basic/programming-guide/concepts/linq/linq-and-file-directories.md)
