---
title: "Procedura: leggere un file di testo una riga alla volta (Visual C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "lettura di file di testo, riga per riga"
  - "ReadLine (metodo) [C#]"
  - "file di testo [C#]"
ms.assetid: d62e22c5-a13c-48db-af9b-f10c801b0cb1
caps.latest.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 11
---
# Procedura: leggere un file di testo una riga alla volta (Visual C#)
Nell'esempio riportato di seguito il contenuto di un file di testo viene letto una riga alla volta, in una stringa, utilizzando il metodo `ReadLine` della classe `StreamReader`.  Ogni riga di testo viene archiviata nella stringa `line` e visualizzata.  
  
## Esempio  
  
```  
int counter = 0;  
string line;  
  
// Read the file and display it line by line.  
System.IO.StreamReader file =   
    new System.IO.StreamReader(@"c:\test.txt");  
while((line = file.ReadLine()) != null)  
{  
    System.Console.WriteLine (line);  
    counter++;  
}  
  
file.Close();  
System.Console.WriteLine("There were {0} lines.", counter);  
// Suspend the screen.  
System.Console.ReadLine();  
```  
  
## Compilazione del codice  
 Copiare il codice e incollarlo nel metodo `Main` di un'applicazione console.  
  
 Sostituire `"c:\test.txt"` con il nome del file effettivo.  
  
## Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il file non esiste.  
  
## Sicurezza di .NET Framework  
 Non basarsi sul nome del file per prendere decisioni in merito al relativo contenuto.  Il file `myFile.cs` potrebbe ad esempio non essere un file di origine C\#.  
  
## Vedere anche  
 <xref:System.IO?displayProperty=fullName>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [File system e Registro di sistema](../../../csharp/programming-guide/file-system/file-system-and-the-registry.md)