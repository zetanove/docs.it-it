---
title: 'Procedura: riordinare i campi di un File delimitato (LINQ) (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: c451c7db-663b-4daf-b8ba-a2093095d672
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
ms.openlocfilehash: 9abb0510ed3944cd80d6658238ef79d64dc0ca27
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-reorder-the-fields-of-a-delimited-file-linq-visual-basic"></a>Procedura: riordinare i campi di un File delimitato (LINQ) (Visual Basic)
Un file con valori delimitati da virgole (CSV) è un file di testo che viene spesso utilizzato per archiviare i dati del foglio di calcolo o altri dati in formato tabulare che sono rappresentati da righe e colonne. Tramite il <xref:System.String.Split%2A>metodo per separare i campi, è molto semplice eseguire query e modificare i file CSV utilizzando LINQ.</xref:System.String.Split%2A> In effetti, utilizzare la stessa tecnica per riordinare le parti di qualsiasi riga di testo; strutturata non è limitata ai file CSV.  
  
 Nell'esempio seguente si presuppone che le tre colonne rappresentano cognome degli studenti"," "nome" e "ID". I campi sono in ordine alfabetico in base ai cognomi degli studenti. La query genera una nuova sequenza in cui la colonna ID viene visualizzata per prima, seguita da una seconda colonna che combina nome e cognome dello studente. Le righe vengono riordinate in base al campo ID. I risultati vengono salvati in un nuovo file e i dati originali non viene modificati.  
  
### <a name="to-create-the-data-file"></a>Per creare il file di dati  
  
1.  Copiare le righe seguenti in un file di testo normale denominato Spreadsheet1. Salvare il file nella cartella del progetto.  
  
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
  
```vb  
Class CSVFiles  
  
    Shared Sub Main()  
  
        ' Create the IEnumerable data source.  
        Dim lines As String() = System.IO.File.ReadAllLines("../../../spreadsheet1.csv")  
  
        ' Execute the query. Put field 2 first, then  
        ' reverse and combine fields 0 and 1 from the old field  
        Dim lineQuery = From line In lines   
                        Let x = line.Split(New Char() {","})   
                        Order By x(2)   
                        Select x(2) & ", " & (x(1) & " " & x(0))  
  
        ' Execute the query and write out the new file. Note that WriteAllLines  
        ' takes a string array, so ToArray is called on the query.  
        System.IO.File.WriteAllLines("../../../spreadsheet2.csv", lineQuery.ToArray())  
  
        ' Keep console window open in debug mode.  
        Console.WriteLine("Spreadsheet2.csv written to disk. Press any key to exit")  
        Console.ReadKey()  
    End Sub  
End Class  
' Output to spreadsheet2.csv:  
' 111, Svetlana Omelchenko  
' 112, Claire O'Donnell  
' 113, Sven Mortensen  
' 114, Cesar Garcia  
' 115, Debra Garcia  
' 116, Fadi Fakhouri  
' 117, Hanying Feng  
' 118, Hugo Garcia  
' 119, Lance Tucker  
' 120, Terry Adams  
' 121, Eugene Zabokritski  
' 122, Michael Tucker  
```  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ e stringhe (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)   
 [Directory di File (Visual Basic) e LINQ](../../../../visual-basic/programming-guide/concepts/linq/linq-and-file-directories.md)   
 [Procedura: generare XML da file CSV](http://msdn.microsoft.com/library/dd7bab8c-96fa-4343-94d0-9739dd6a74fd)
