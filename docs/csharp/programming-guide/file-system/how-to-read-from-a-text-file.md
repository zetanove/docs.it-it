---
title: "Procedura: leggere da un file di testo (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "StreamReader.ReadToEnd"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "lettura di dati, testo (file)"
  - "lettura di file di testo"
  - "testo (file), lettura"
  - "testo (file), scrittura"
ms.assetid: 92246c5b-e819-4eea-9370-1a9460e12de3
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# Procedura: leggere da un file di testo (Guida per programmatori C#)
In questo esempio viene letto il contenuto di un file di testo tramite i metodi statici <xref:System.IO.File.ReadAllText%2A> e <xref:System.IO.File.ReadAllLines%2A> dalla classe <xref:System.IO.File?displayProperty=fullName>.  
  
 Per un esempio in cui viene utilizzato un oggetto <xref:System.IO.StreamReader>, vedere [Procedura: leggere un file di testo una riga alla volta](../../../csharp/programming-guide/file-system/how-to-read-a-text-file-one-line-at-a-time.md).  
  
> [!NOTE]
>  I file utilizzati in questo esempio vengono creati nell'argomento [Procedura: scrivere in un file di testo](../../../csharp/programming-guide/file-system/how-to-write-to-a-text-file.md).  
  
## Esempio  
 [!code-cs[csFilesandFolders#4](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-read-from-a-text-file_1.cs)]  
  
## Compilazione del codice  
 Copiare il codice e incollarlo in un'applicazione console C\#.  
  
 Se non si utilizzano i file di testo da [Procedura: scrivere in un file di testo](../../../csharp/programming-guide/file-system/how-to-write-to-a-text-file.md), sostituire l'argomento in `ReadAllText` e a `ReadAllLines` con il percorso appropriato e il nome file nel computer.  
  
## Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il file non esiste o non esiste nella posizione specificata.  Verificare che il percorso e l'ortografia del nome file.  
  
## Sicurezza di .NET Framework  
 Non basarsi sul nome di un file per determinare il contenuto del file.  Ad esempio, il file `myFile.cs` non può essere un file di origine C\#.  
  
## Vedere anche  
 <xref:System.IO?displayProperty=fullName>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [File system e Registro di sistema](../../../csharp/programming-guide/file-system/file-system-and-the-registry.md)