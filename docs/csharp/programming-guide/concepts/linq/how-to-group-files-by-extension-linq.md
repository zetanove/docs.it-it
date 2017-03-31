---
title: 'Procedura: Raggruppare file per estensione (LINQ) (C#) | Microsoft Docs'
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
ms.assetid: 21a98320-a5a1-4981-82d8-6a637e7d9018
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
ms.openlocfilehash: 67b3672ff7fa6c4d188c18f246f5e564ec3b0b29
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-group-files-by-extension-linq-c"></a>Procedura: Raggruppare file per estensione (LINQ) (C#)
Questo esempio illustra come usare LINQ per eseguire operazioni avanzate di raggruppamento e ordinamento su elenchi di file o cartelle. Viene anche illustrato come scorrere i risultati nella finestra della console usando i metodi <xref:System.Linq.Enumerable.Skip%2A> e <xref:System.Linq.Enumerable.Take%2A>.  
  
## <a name="example"></a>Esempio  
 La query seguente illustra come raggruppare il contenuto di un albero di directory specificato per l'estensione dei nomi dei file.  
  
```csharp  
class GroupByExtension  
{  
    // This query will sort all the files under the specified folder  
    //  and subfolder into groups keyed by the file extension.  
    private static void Main()  
    {  
        // Take a snapshot of the file system.  
        string startFolder = @"c:\program files\Microsoft Visual Studio 9.0\Common7";  
  
        // Used in WriteLine to trim output lines.  
        int trimLength = startFolder.Length;  
  
        // Take a snapshot of the file system.  
        System.IO.DirectoryInfo dir = new System.IO.DirectoryInfo(startFolder);  
  
        // This method assumes that the application has discovery permissions  
        // for all folders under the specified path.  
        IEnumerable<System.IO.FileInfo> fileList = dir.GetFiles("*.*", System.IO.SearchOption.AllDirectories);  
  
        // Create the query.  
        var queryGroupByExt =  
            from file in fileList  
            group file by file.Extension.ToLower() into fileGroup  
            orderby fileGroup.Key  
            select fileGroup;  
  
        // Display one group at a time. If the number of   
        // entries is greater than the number of lines  
        // in the console window, then page the output.  
        PageOutput(trimLength, queryGroupByExt);  
    }  
  
    // This method specifically handles group queries of FileInfo objects with string keys.  
    // It can be modified to work for any long listings of data. Note that explicit typing  
    // must be used in method signatures. The groupbyExtList parameter is a query that produces  
    // groups of FileInfo objects with string keys.  
    private static void PageOutput(int rootLength,  
                                    IEnumerable<System.Linq.IGrouping<string, System.IO.FileInfo>> groupByExtList)  
    {  
        // Flag to break out of paging loop.  
        bool goAgain = true;  
  
        // "3" = 1 line for extension + 1 for "Press any key" + 1 for input cursor.  
        int numLines = Console.WindowHeight - 3;  
  
        // Iterate through the outer collection of groups.  
        foreach (var filegroup in groupByExtList)  
        {  
            // Start a new extension at the top of a page.  
            int currentLine = 0;  
  
            // Output only as many lines of the current group as will fit in the window.  
            do  
            {  
                Console.Clear();  
                Console.WriteLine(filegroup.Key == String.Empty ? "[none]" : filegroup.Key);  
  
                // Get 'numLines' number of items starting at number 'currentLine'.  
                var resultPage = filegroup.Skip(currentLine).Take(numLines);  
  
                //Execute the resultPage query  
                foreach (var f in resultPage)  
                {  
                    Console.WriteLine("\t{0}", f.FullName.Substring(rootLength));  
                }  
  
                // Increment the line counter.  
                currentLine += numLines;  
  
                // Give the user a chance to escape.  
                Console.WriteLine("Press any key to continue or the 'End' key to break...");  
                ConsoleKey key = Console.ReadKey().Key;  
                if (key == ConsoleKey.End)  
                {  
                    goAgain = false;  
                    break;  
                }  
            } while (currentLine < filegroup.Count());  
  
            if (goAgain == false)  
                break;  
        }  
    }  
}  
```  
  
 L'output di questo programma può essere lungo, a seconda dei dettagli del file system locale e dell'impostazione di `startFolder`. Per abilitare la visualizzazione di tutti i risultati, in questo esempio viene illustrato come scorrere i risultati. È possibile applicare le stesse tecniche ad applicazioni Windows e Web. Si noti che, poiché il codice dispone gli elementi in un gruppo, è necessario un ciclo `foreach` annidato. È disponibile anche una logica aggiuntiva per calcolare la posizione corrente nell'elenco e per consentire all'utente di interrompere lo scorrimento e uscire dal programma. In questo caso particolare la query di scorrimento viene eseguita sui risultati memorizzati nella cache della query originale. In altri contesti, come ad esempio LINQ to SQL, la memorizzazione nella cache non è necessaria.  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Creare un progetto che usi .NET Framework 3.5 o versione successiva con un riferimento a System.Core.dll e alle direttive `using` per gli spazi dei nomi System.Linq e System.IO.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to Objects (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-objects.md)   
 [Directory di file e LINQ (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-file-directories.md)
