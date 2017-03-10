---
title: "Procedura: ottenere informazioni relative a file, cartelle e unit&#224; (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "file [C#], recupero di informazioni"
ms.assetid: 22fc2da6-5494-405b-995e-c0b99142a93e
caps.latest.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# Procedura: ottenere informazioni relative a file, cartelle e unit&#224; (Guida per programmatori C#)
In .NET Framework, è possibile accedere alle informazioni sul file system tramite le classi seguenti:  
  
-   <xref:System.IO.FileInfo?displayProperty=fullName>  
  
-   <xref:System.IO.DirectoryInfo?displayProperty=fullName>  
  
-   <xref:System.IO.DriveInfo?displayProperty=fullName>  
  
-   <xref:System.IO.Directory?displayProperty=fullName>  
  
-   <xref:System.IO.File?displayProperty=fullName>  
  
 Le classi <xref:System.IO.FileInfo> e <xref:System.IO.DirectoryInfo> rappresentano un file o una directory e contengono proprietà che espongono molti degli attributi di file supportati dal file system NTFS.  Contengono anche metodi per l'apertura, la chiusura, lo spostamento e l'eliminazione di file e cartelle.  È possibile creare istanze di queste classi passando al costruttore una stringa che rappresenta il nome del file, della cartella o dell'unità:  
  
```c#  
System.IO.DriveInfo di = new System.IO.DriveInfo(@"C:\");  
```  
  
 È inoltre possibile ottenere i nomi di file, cartelle o unità tramite chiamate a <xref:System.IO.DirectoryInfo.GetDirectories%2A?displayProperty=fullName>, <xref:System.IO.DirectoryInfo.GetFiles%2A?displayProperty=fullName>e <xref:System.IO.DriveInfo.RootDirectory%2A?displayProperty=fullName>.  
  
 Le classi <xref:System.IO.Directory?displayProperty=fullName> e <xref:System.IO.File?displayProperty=fullName> forniscono metodi statici per il recupero di informazioni su directory e file.  
  
## Esempio  
 Nell'esempio seguente vengono mostrati vari modi di accedere alle informazioni su file e cartelle.  
  
 [!code-cs[csFilesandFolders#6](../../../csharp/programming-guide/file-system/codesnippet/csharp/csFilesFolders/FileIteration.cs#6)]  
  
## Programmazione efficiente  
 Quando si elaborano stringhe di percorso specificate dall'utente, è necessario gestire anche le eccezioni per le condizioni seguenti:  
  
-   Il formato del nome del file non è corretto.  Ad esempio, contiene caratteri non validi o solo uno spazio vuoto.  
  
-   Il nome del file è null.  
  
-   La lunghezza del nome del file è maggiore di quella consentita dal sistema  
  
-   Il nome del file contiene due punti \(:\).  
  
 Se l'applicazione non dispone delle autorizzazioni sufficienti per la lettura del file specificato, il metodo `Exists` restituirà `false`, indipendentemente dall'esistenza del percorso, e non verrà generata un'eccezione.  
  
## Vedere anche  
 <xref:System.IO?displayProperty=fullName>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [File system e Registro di sistema](../../../csharp/programming-guide/file-system/file-system-and-the-registry.md)