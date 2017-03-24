---
title: 'Procedura: eseguire una Query per trovare frasi che contengono un Set specificato di parole (LINQ) (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: a5ae8ced-61fe-4c10-bb8a-95630e50f603
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
ms.openlocfilehash: 31561d586c9c05f502002efdfc455acb55159fed
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-query-for-sentences-that-contain-a-specified-set-of-words-linq-visual-basic"></a>Procedura: eseguire una query per trovare frasi che contengono un set definito di parole (LINQ) (Visual Basic)
In questo esempio viene illustrato come trovare frasi in un file di testo che contengono corrispondenze per ognuno di un set specificato di parole. Anche se la matrice dei termini di ricerca è hardcoded in questo esempio, si potrebbe anche essere compilato in modo dinamico in fase di esecuzione. In questo esempio, la query restituisce le frasi che contengono le parole "Sempre", "dati" e "integrata".  
  
## <a name="example"></a>Esempio  
  
```vb  
Class FindSentences  
  
    Shared Sub Main()  
        Dim text As String = "Historically, the world of data and the world of objects " &   
        "have not been well integrated. Programmers work in C# or Visual Basic " &   
        "and also in SQL or XQuery. On the one side are concepts such as classes, " &   
        "objects, fields, inheritance, and .NET Framework APIs. On the other side " &   
        "are tables, columns, rows, nodes, and separate languages for dealing with " &   
        "them. Data types often require translation between the two worlds; there are " &   
        "different standard functions. Because the object world has no notion of query, a " &   
        "query can only be represented as a string without compile-time type checking or " &   
        "IntelliSense support in the IDE. Transferring data from SQL tables or XML trees to " &   
        "objects in memory is often tedious and error-prone."  
  
        ' Split the text block into an array of sentences.  
        Dim sentences As String() = text.Split(New Char() {".", "?", "!"})  
  
        ' Define the search terms. This list could also be dynamically populated at runtime  
        Dim wordsToMatch As String() = {"Historically", "data", "integrated"}  
  
        ' Find sentences that contain all the terms in the wordsToMatch array  
        ' Note that the number of terms to match is not specified at compile time  
        Dim sentenceQuery = From sentence In sentences   
                            Let w = sentence.Split(New Char() {" ", ",", ".", ";", ":"},   
                                                   StringSplitOptions.RemoveEmptyEntries)   
                            Where w.Distinct().Intersect(wordsToMatch).Count = wordsToMatch.Count()   
                            Select sentence  
  
        ' Execute the query  
        For Each str As String In sentenceQuery  
            Console.WriteLine(str)  
        Next  
  
        ' Keep console window open in debug mode.  
        Console.WriteLine("Press any key to exit.")  
        Console.ReadKey()  
    End Sub  
  
End Class  
' Output:  
' Historically, the world of data and the world of objects have not been well integrated  
```  
  
 La query funziona suddividendo prima il testo in frasi e quindi suddividendo le frasi in una matrice di stringhe che contengono ogni parola. Per ognuna di queste matrici, il <xref:System.Linq.Enumerable.Distinct%2A>metodo rimuove tutte le parole duplicate e quindi la query esegue un <xref:System.Linq.Enumerable.Intersect%2A>operazione sulla matrice di parole e `wordsToMatch` array.</xref:System.Linq.Enumerable.Intersect%2A> </xref:System.Linq.Enumerable.Distinct%2A> Se il conteggio dell'intersezione è lo stesso conteggio del `wordsToMatch` matrice, tutte le parole sono state trovate le parole e viene restituita la frase originale.  
  
 Nella chiamata a <xref:System.String.Split%2A>, i segni di punteggiatura vengono usati come separatore per rimuoverli dalla stringa.</xref:System.String.Split%2A> Se questa operazione non, ad esempio, si potrebbe disporre di una stringa "Sempre", che non corrisponde a "Sempre" nel `wordsToMatch` matrice. È necessario utilizzare altri separatori, a seconda dei tipi di punteggiatura trovati nel testo di origine.  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Creare un progetto destinato a .NET Framework versione 3.5 o versione successiva con un riferimento a System.Core.dll e una `Imports` istruzione per lo spazio dei nomi System. Linq.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ e stringhe (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)
