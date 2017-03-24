---
title: "Procedura: popolare raccolte di oggetti da più origini (LINQ) (Visual Basic) | Documenti di Microsoft"
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
ms.assetid: 63062a22-e6a9-42c0-b357-c7c965f58f33
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
ms.openlocfilehash: 25f504d862ef2176dc90a31fbccf18777b9d3d0a
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-populate-object-collections-from-multiple-sources-linq-visual-basic"></a>Procedura: popolare raccolte di oggetti da più origini (LINQ) (Visual Basic)
In questo esempio viene illustrato come unire dati da origini diverse in una sequenza di nuovi tipi.  
  
> [!NOTE]
>  Non tentare di aggiungere dati in memoria o i dati nel file system con i dati che è ancora in un database. Tali join tra domini può generare risultati non definiti a causa di diversi modi in cui le operazioni di join possono essere definite per le query di database e altri tipi di origini. Inoltre, è possibile che tale operazione potrebbe generare un'eccezione di memoria esaurita se la quantità di dati nel database è sufficientemente grande. Per unire i dati da un database per i dati in memoria, chiamare innanzitutto `ToList` o `ToArray` nel database di eseguire una query e quindi eseguire il join nella raccolta restituita.  
  
### <a name="to-create-the-data-file"></a>Per creare il file di dati  
  
-   Copiare i file Names. csv e scores nella cartella del progetto, come descritto in [procedura: unire contenuto da diversi file (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-join-content-from-dissimilar-files-linq.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come utilizzare un tipo denominato `Student` per archiviare i dati uniti da due insiemi di stringhe che simulano i dati del foglio di calcolo in formato CSV in memoria. Il primo insieme di stringhe rappresenta i nomi degli studenti e gli ID e la seconda raccolta rappresenta l'ID dello studente (nella prima colonna) e i punteggi di quattro esami. L'ID viene utilizzato come chiave esterna.  
  
```vb  
Class Student  
    Public FirstName As String  
    Public LastName As String  
    Public ID As Integer  
    Public ExamScores As List(Of Integer)  
End Class  
  
Class PopulateCollection  
  
    Shared Sub Main()  
  
        ' Merge content from spreadsheets into a list of Student objects.  
  
        ' These data files are defined in How to: Join Content from   
        ' Dissimilar Files (LINQ).  
  
        ' Each line of names.csv consists of a last name, a first name, and an  
        ' ID number, separated by commas. For example, Omelchenko,Svetlana,111  
        Dim names As String() = System.IO.File.ReadAllLines("../../../names.csv")  
  
        ' Each line of scores.csv consists of an ID number and four test   
        ' scores, separated by commas. For example, 111, 97, 92, 81, 60  
        Dim scores As String() = System.IO.File.ReadAllLines("../../../scores.csv")  
  
        ' The following query merges the content of two dissimilar spreadsheets   
        ' based on common ID values.  
        ' Multiple From clauses are used instead of a Join clause  
        ' in order to store the results of scoreLine.Split.  
        ' Note the dynamic creation of a list of integers for the  
        ' ExamScores member. We skip the first item in the split string   
        ' because it is the student ID, not an exam score.  
        Dim queryNamesScores = From nameLine In names  
                          Let splitName = nameLine.Split(New Char() {","})  
                          From scoreLine In scores  
                          Let splitScoreLine = scoreLine.Split(New Char() {","})  
                          Where splitName(2) = splitScoreLine(0)  
                          Select New Student() With {  
                               .FirstName = splitName(0), .LastName = splitName(1), .ID = splitName(2),  
                               .ExamScores = (From scoreAsText In splitScoreLine Skip 1  
                                             Select Convert.ToInt32(scoreAsText)).ToList()}  
  
        ' Optional. Store the query results for faster access in future  
        ' queries. This could be useful with very large data files.  
        Dim students As List(Of Student) = queryNamesScores.ToList()  
  
        ' Display each student's name and exam score average.  
        For Each s In students  
            Console.WriteLine("The average score of " & s.FirstName & " " &  
                              s.LastName & " is " & s.ExamScores.Average())  
        Next  
  
        ' Keep console window open in debug mode.  
        Console.WriteLine("Press any key to exit.")  
        Console.ReadKey()  
    End Sub  
End Class  
  
' Output:   
' The average score of Omelchenko Svetlana is 82.5  
' The average score of O'Donnell Claire is 72.25  
' The average score of Mortensen Sven is 84.5  
' The average score of Garcia Cesar is 88.25  
' The average score of Garcia Debra is 67  
' The average score of Fakhouri Fadi is 92.25  
' The average score of Feng Hanying is 88  
' The average score of Garcia Hugo is 85.75  
' The average score of Tucker Lance is 81.75  
' The average score of Adams Terry is 85.25  
' The average score of Zabokritski Eugene is 83  
' The average score of Tucker Michael is 92  
```  
  
 Nel [clausola Select](../../../../visual-basic/language-reference/queries/select-clause.md) clausola, un inizializzatore di oggetto viene utilizzato per creare un'istanza di ogni nuovo `Student` oggetto con i dati dalle due origini.  
  
 Se non è necessario archiviare i risultati di una query, tipi anonimi possono essere più conveniente di tipi denominati. Tipi denominati sono necessari se si passano i risultati della query all'esterno del metodo in cui viene eseguita la query. Nell'esempio seguente esegue la stessa attività dell'esempio precedente, ma utilizza tipi anonimi anziché tipi denominati:  
  
```vb  
' Merge the data by using an anonymous type.   
' Note the dynamic creation of a list of integers for the  
' ExamScores member. We skip 1 because the first string  
' in the array is the student ID, not an exam score.  
Dim queryNamesScores2 =  
    From nameLine In names  
    Let splitName = nameLine.Split(New Char() {","})  
    From scoreLine In scores  
    Let splitScoreLine = scoreLine.Split(New Char() {","})  
    Where splitName(2) = splitScoreLine(0)  
    Select New With  
           {.Last = splitName(0),  
            .First = splitName(1),  
            .ExamScores = (From scoreAsText In splitScoreLine Skip 1  
                           Select Convert.ToInt32(scoreAsText)).ToList()}  
  
' Display each student's name and exam score average.  
For Each s In queryNamesScores2  
    Console.WriteLine("The average score of " & s.First & " " &  
                      s.Last & " is " & s.ExamScores.Average())  
Next  
```  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Creare un progetto destinato a .NET Framework versione 3.5 o versione successiva con un riferimento a System.Core.dll e una `Imports` istruzione per lo spazio dei nomi System. Linq.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ e stringhe (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)
