---
title: 'Procedura: Creare un file o una cartella (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- folders [C#]
- creating files [C#]
- files [C#]
- creating folders [C#]
ms.assetid: 4582ee2d-d72d-4687-bcb9-08d336c62c25
caps.latest.revision: 22
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: bba53c8d175d95aa3b89ba458517d439a8d2bb11
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-a-file-or-folder-c-programming-guide"></a>Procedura: creare un file o una cartella (Guida per programmatori C#)
A livello di codice è possibile creare una cartella, una sottocartella e un file nella sottocartella e quindi scrivere dati nel file.  
  
## <a name="example"></a>Esempio  
 [!code-cs[csFilesandFolders#10](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-create-a-file-or-folder_1.cs)]  
  
 Se la cartella esiste già, <xref:System.IO.Directory.CreateDirectory%2A> non produce effetti e non vengono generate eccezioni. <xref:System.IO.File.Create%2A?displayProperty=fullName>, tuttavia, sostituisce un file esistente con un nuovo file. Nell'esempio viene usata un'istruzione `if`-`else` per evitare la sostituzione di un file esistente.  
  
 Apportando le modifiche seguenti nell'esempio, è possibile specificare risultati diversi in base all'esistenza o meno di un file con un determinato nome. Se il file non esiste, il codice ne crea uno. Se il file esiste, il codice aggiunge i dati a questo.  
  
-   Specificare un nome file non casuale.  
  
    ```csharp  
    // Comment out the following line.  
    //string fileName = System.IO.Path.GetRandomFileName();  
  
    // Replace that line with the following assignment.  
    string fileName = "MyNewFile.txt";  
  
    ```  
  
-   Sostituire l'istruzione `if`-`else` con l'istruzione `using` riportata nel codice seguente.  
  
    ```csharp  
    using (System.IO.FileStream fs = new System.IO.FileStream(pathString, FileMode.Append))   
    {  
        for (byte i = 0; i < 100; i++)  
        {  
            fs.WriteByte(i);  
        }  
    }  
  
    ```  
  
 Eseguire l'esempio più volte per verificare che i dati vengano aggiunti al file ogni volta.  
  
 Per altri valori `FileMode` da provare, vedere <xref:System.IO.FileMode>.  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il formato del nome della cartella non è valido. È possibile ad esempio che contenga caratteri non validi o sia costituito solo da uno spazio (classe <xref:System.ArgumentException>). Per creare nomi di percorso validi, usare la classe <xref:System.IO.Path>.  
  
-   La cartella padre della cartella da creare è di sola lettura (classe <xref:System.IO.IOException>).  
  
-   Il nome della cartella è `null` (classe <xref:System.ArgumentNullException>).  
  
-   Il nome della cartella è troppo lungo (classe <xref:System.IO.PathTooLongException>).  
  
-   Il nome della cartella è composto solo dai due punti, ":" (classe <xref:System.IO.PathTooLongException>).  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 In condizioni di attendibilità parziale è possibile che venga generata un'istanza della classe <xref:System.Security.SecurityException>.  
  
 Se l'utente non dispone dell'autorizzazione per creare la cartella, l'esempio genera un'istanza della classe <xref:System.UnauthorizedAccessException>.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.IO?displayProperty=fullName>   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [File system e Registro di sistema (Guida per programmatori C#)](../../../csharp/programming-guide/file-system/index.md)
