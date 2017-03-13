---
title: "Procedura: creare un file o una cartella (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "creazione di file [C#]"
  - "creazione di cartelle [C#]"
  - "file [C#]"
  - "cartelle [C#]"
ms.assetid: 4582ee2d-d72d-4687-bcb9-08d336c62c25
caps.latest.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 22
---
# Procedura: creare un file o una cartella (Guida per programmatori C#)
A livello di codice è possibile creare una cartella sul computer, creare una sottocartella, creare un file nella sottocartella e scrivere dati nel file.  
  
## Esempio  
 [!code-cs[csFilesandFolders#10](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-create-a-file-or-folder_1.cs)]  
  
 Se la cartella esiste già, <xref:System.IO.Directory.CreateDirectory%2A> non produce effetti e non vengono generate eccezioni.  Tuttavia, <xref:System.IO.File.Create%2A?displayProperty=fullName> sostituisce un file esistente con un nuovo file.  Nell'esempio viene utilizzata un'istruzione`else` \- `if`per impedire la sostituzione di un file esistente.  
  
 Apportando le seguenti modifiche nell'esempio, è possibile specificare risultati diversi a seconda se un file con un determinato nome esiste già.  Se tale file non esiste, il codice ne crea uno.  Se tale file esiste, il codice aggiunge i dati a tale file.  
  
-   Specificare un nome file non casuale.  
  
    ```c#  
    // Comment out the following line.  
    //string fileName = System.IO.Path.GetRandomFileName();  
  
    // Replace that line with the following assignment.  
    string fileName = "MyNewFile.txt";  
  
    ```  
  
-   Sostituire l'istruzione `if`\-`else` con l'istruzione `using` riportata nel codice seguente.  
  
    ```c#  
    using (System.IO.FileStream fs = new System.IO.FileStream(pathString, FileMode.Append))   
    {  
        for (byte i = 0; i < 100; i++)  
        {  
            fs.WriteByte(i);  
        }  
    }  
  
    ```  
  
 Eseguire l'esempio più volte per verificare che i dati vengano aggiunti ogni volta al file.  
  
 Per ulteriori valori `FileMode` che è possibile provare, vedere <xref:System.IO.FileMode>.  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il formato del nome della cartella non è corretto.  È possibile ad esempio che contenga caratteri non validi o solo uno spazio vuoto \(classe <xref:System.ArgumentException>\).  Utilizzare la classe <xref:System.IO.Path> per creare nomi di percorso validi.  
  
-   La cartella padre della cartella da creare è di sola lettura \(classe <xref:System.IO.IOException>\).  
  
-   Il nome della cartella è `null` \(classe <xref:System.ArgumentNullException>\).  
  
-   Il nome della cartella è troppo lungo \(classe <xref:System.IO.PathTooLongException>\).  
  
-   Il nome della cartella è composto solo dai due punti, ":" \(classe <xref:System.IO.PathTooLongException>\).  
  
## Sicurezza di .NET Framework  
 È possibile che venga generata un'istanza della classe <xref:System.Security.SecurityException> in situazioni di attendibilità parziale.  
  
 Se l'utente non dispone dell'autorizzazione per creare la cartella, nell'esempio verrà generata un'istanza della classe <xref:System.UnauthorizedAccessException>.  
  
## Vedere anche  
 <xref:System.IO?displayProperty=fullName>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [File system e Registro di sistema](../../../csharp/programming-guide/file-system/file-system-and-the-registry.md)