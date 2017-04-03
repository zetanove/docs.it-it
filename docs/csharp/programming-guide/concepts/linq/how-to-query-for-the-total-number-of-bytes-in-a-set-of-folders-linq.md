---
title: 'Procedura: Eseguire una query per trovare il numero totale di byte in un set di cartelle (LINQ) (C#) | Microsoft Docs'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: a01bd1d4-133c-4ca2-aa4e-e93e81d6076c
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: dd78f36792ab65f31075a7a83660261f096953ae
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-query-for-the-total-number-of-bytes-in-a-set-of-folders-linq-c"></a>Procedura: Eseguire una query per trovare il numero totale di byte in un set di cartelle (LINQ) (C#)
Questo esempio illustra come recuperare il numero totale di byte usati da tutti i file in una cartella specificata e in tutte le relative sottocartelle.  
  
## <a name="example"></a>Esempio  
 Il metodo <xref:System.Linq.Enumerable.Sum%2A> aggiunge i valori di tutti gli elementi selezionati nella clausola `select`. È possibile modificare facilmente questa query per recuperare il file più grande o più piccolo nella struttura ad albero di directory specificata chiamando il metodo <xref:System.Linq.Enumerable.Min%2A> o <xref:System.Linq.Enumerable.Max%2A> anziché <xref:System.Linq.Enumerable.Sum%2A>.  
  
```csharp  
class QuerySize  
{  
    public static void Main()  
    {  
        string startFolder = @"c:\program files\Microsoft Visual Studio 9.0\VC#";  
  
        // Take a snapshot of the file system.  
        // This method assumes that the application has discovery permissions  
        // for all folders under the specified path.  
        IEnumerable<string> fileList = System.IO.Directory.GetFiles(startFolder, "*.*", System.IO.SearchOption.AllDirectories);  
  
        var fileQuery = from file in fileList  
                        select GetFileLength(file);  
  
        // Cache the results to avoid multiple trips to the file system.  
        long[] fileLengths = fileQuery.ToArray();  
  
        // Return the size of the largest file  
        long largestFile = fileLengths.Max();  
  
        // Return the total number of bytes in all the files under the specified folder.  
        long totalBytes = fileLengths.Sum();  
  
        Console.WriteLine("There are {0} bytes in {1} files under {2}",  
            totalBytes, fileList.Count(), startFolder);  
        Console.WriteLine("The largest files is {0} bytes.", largestFile);  
  
        // Keep the console window open in debug mode.  
        Console.WriteLine("Press any key to exit.");  
        Console.ReadKey();  
    }  
  
    // This method is used to swallow the possible exception  
    // that can be raised when accessing the System.IO.FileInfo.Length property.  
    static long GetFileLength(string filename)  
    {  
        long retval;  
        try  
        {  
            System.IO.FileInfo fi = new System.IO.FileInfo(filename);  
            retval = fi.Length;  
        }  
        catch (System.IO.FileNotFoundException)  
        {  
            // If a file is no longer present,  
            // just add zero bytes to the total.  
            retval = 0;  
        }  
        return retval;  
    }  
}  
```  
  
 Se è necessario contare solo il numero di byte in un albero di directory specificato, è possibile eseguire questa operazione in modo più efficiente senza creare una query LINQ che comporta un sovraccarico dovuto alla creazione della raccolta di elenchi come origine dati. I vantaggi dell'uso di LINQ aumentano per le query più complesse oppure quando è necessario eseguire più query nella stessa origine dati.  
  
 La query effettua una chiamata a un metodo separato per ottenere la lunghezza del file. Questa operazione viene eseguita per gestire una possibile eccezione generata nel caso in cui il file sia stato eliminato in un altro thread dopo la creazione dell'oggetto <xref:System.IO.FileInfo> nella chiamata a `GetFiles`. Sebbene l'oggetto <xref:System.IO.FileInfo> sia già stato creato, l'eccezione può verificarsi poiché un oggetto <xref:System.IO.FileInfo> tenta di aggiornare la proprietà <xref:System.IO.FileInfo.Length%2A> con la lunghezza più recente al primo accesso alla proprietà. Inserendo questa operazione in un blocco try/catch all'esterno della query, si evita di eseguire operazioni nelle query che possono causare effetti collaterali. In generale, è necessario prestare particolare attenzione durante la gestione delle eccezioni per assicurarsi che un'applicazione non venga lasciata in uno stato sconosciuto.  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Creare un progetto che usa.NET Framework 3.5 o versione successiva con un riferimento a System.Core.dll e alle direttive `using` per gli spazi dei nomi System.Linq e System.IO.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to Objects (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-objects.md)   
 [Directory di file e LINQ (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-file-directories.md)
