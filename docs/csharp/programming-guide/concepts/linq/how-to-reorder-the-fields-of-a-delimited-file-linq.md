---
title: 'Procedura: Riordinare i campi di un file delimitato (LINQ) (C#) | Microsoft Docs'
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
ms.assetid: 4e62d82c-61b7-4f18-b9a1-86723746d7d2
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
ms.openlocfilehash: a7417143a1dbe2e07e7983fb12d6f3e55e70f461
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-reorder-the-fields-of-a-delimited-file-linq-c"></a>Procedura: Riordinare i campi di un file delimitato (LINQ) (C#)
Un file con valori delimitati da virgole (CSV) è un file di testo che spesso viene usato per archiviare dati di un foglio di calcolo o altri dati tabulari rappresentati da righe e colonne. Grazie al metodo <xref:System.String.Split%2A> per separare i campi, è molto semplice eseguire una query e modificare i file CSV tramite LINQ. In effetti la stessa tecnica può essere usata per riordinare le parti di qualsiasi riga di testo strutturata, non solo i file CSV.  
  
 Nell'esempio seguente vengono usate tre colonne per rappresentare "cognome", "nome" e "ID" di alcuni studenti. I campi sono in ordine alfabetico in base ai cognomi degli studenti. La query genera una nuova sequenza in cui la colonna ID viene visualizzata per prima, seguita da una seconda colonna che combina il nome e il cognome dello studente. Le righe vengono riordinate in base al campo ID. I risultati vengono salvati in un nuovo file e i dati originali non vengono modificati.  
  
### <a name="to-create-the-data-file"></a>Per creare il file di dati  
  
1.  Copiare le righe seguenti in un file di testo normale denominato spreadsheet1.csv. Salvare il file nella cartella del progetto.  
  
    ```  
    Adams,Terry,120  
    Fakhouri,Fadi,116  
    Feng,Hanying,117  
    Garcia,Cesar,114  
    Garcia,Debra,115  
    Garcia,Hugo,118  
    Mortensen,Sven,113  
    O'Donnell,Claire,112  
    Omelchenko,Svetlana,111  
    Tucker,Lance,119  
    Tucker,Michael,122  
    Zabokritski,Eugene,121  
    ```  
  
## <a name="example"></a>Esempio  
  
```csharp  
class CSVFiles  
{  
    static void Main(string[] args)  
    {  
        // Create the IEnumerable data source  
        string[] lines = System.IO.File.ReadAllLines(@"../../../spreadsheet1.csv");  
  
        // Create the query. Put field 2 first, then  
        // reverse and combine fields 0 and 1 from the old field  
        IEnumerable<string> query =  
            from line in lines  
            let x = line.Split(',')  
            orderby x[2]  
            select x[2] + ", " + (x[1] + " " + x[0]);  
  
        // Execute the query and write out the new file. Note that WriteAllLines  
        // takes a string[], so ToArray is called on the query.  
        System.IO.File.WriteAllLines(@"../../../spreadsheet2.csv", query.ToArray());  
  
        Console.WriteLine("Spreadsheet2.csv written to disk. Press any key to exit");  
        Console.ReadKey();  
    }  
}  
/* Output to spreadsheet2.csv:  
111, Svetlana Omelchenko  
112, Claire O'Donnell  
113, Sven Mortensen  
114, Cesar Garcia  
115, Debra Garcia  
116, Fadi Fakhouri  
117, Hanying Feng  
118, Hugo Garcia  
119, Lance Tucker  
120, Terry Adams  
121, Eugene Zabokritski  
122, Michael Tucker  
 */  
```  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Creare un progetto che usi .NET Framework versione 3.5 o successiva con un riferimento a System.Core.dll e alle direttive `using` per gli spazi dei nomi System.Linq e System.IO.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ e stringhe (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-strings.md)   
 [Directory di file e LINQ (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-file-directories.md)   
 [Procedura: generare XML da file CSV](http://msdn.microsoft.com/library/dd7bab8c-96fa-4343-94d0-9739dd6a74fd)
