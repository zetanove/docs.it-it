---
title: "How to: Create a File in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "text files, creating"
  - "files, creating"
ms.assetid: 0253bb6d-5519-4a50-b882-b93ef5cca0d9
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Create a File in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In questo esempio viene creato un file di testo vuoto nel percorso specificato utilizzando il metodo <xref:System.IO.File.Create%2A> nella classe <xref:System.IO.File>.  
  
## Esempio  
 [!code-vb[VbFileIOMisc#1](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-create-a-file_1.vb)]  
  
## Compilazione del codice  
 Utilizzare la variabile `file` per scrivere nel file.  
  
## Programmazione efficiente  
 Se il file esiste già verrà sostituito.  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il formato del nome del percorso non è corretto.  Ad esempio, contiene caratteri non consentiti oppure è solo uno spazio vuoto \(<xref:System.ArgumentException>\).  
  
-   Il percorso è di sola lettura \(<xref:System.IO.IOException>\).  
  
-   Il nome del percorso è `Nothing` \(<xref:System.ArgumentNullException>\).  
  
-   Il nome percorso è troppo lungo \(<xref:System.IO.PathTooLongException>\).  
  
-   Il percorso non è valido \(<xref:System.IO.DirectoryNotFoundException>\).  
  
-   Il percorso contiene solo i due punti ":" \(<xref:System.NotSupportedException>\).  
  
## Sicurezza di .NET Framework  
 È possibile che venga generata una <xref:System.Security.SecurityException> in ambienti ad attendibilità parziale.  
  
 La chiamata al metodo <xref:System.IO.File.Create%2A> richiede <xref:System.Security.Permissions.FileIOPermission>.  
  
 Viene generata una <xref:System.UnauthorizedAccessException> se l'utente non dispone dell'autorizzazione per creare il file.  
  
## Vedere anche  
 <xref:System.IO>   
 <xref:System.IO.File.Create%2A>   
 [Using Libraries from Partially Trusted Code](../Topic/Using%20Libraries%20from%20Partially%20Trusted%20Code.md)   
 [Code Access Security Basics](../Topic/Code%20Access%20Security%20Basics.md)