---
title: "How to: Get the Collection of Files in a Directory in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "folders, working with"
  - "files, accessing"
ms.assetid: 6c8ba7e8-dd37-4853-92bf-762b67c98160
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# How to: Get the Collection of Files in a Directory in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Gli overload del metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%2A?displayProperty=fullName> restituiscono una raccolta di stringhe di sola lettura che rappresenta i nomi dei file contenuti in una directory:  
  
-   Usare l'overload <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%28System.String%29> per eseguire una ricerca di file semplice in una directory specificata senza cercare nelle sottodirectory.  
  
-   Usare l'overload [GetFiles\(String, SearchOption, String\<xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%28System.String%2CMicrosoft.VisualBasic.FileIO.SearchOption%2CSystem.String%5B%5D%29> per specificare opzioni aggiuntive per la ricerca.  È possibile usare il parametro `wildCards` per specificare un criterio di ricerca.  Per includere le sottodirectory nella ricerca, impostare il parametro `searchType` su <xref:Microsoft.VisualBasic.FileIO.SearchOption?displayProperty=fullName>.  
  
 Se non vengono trovati file corrispondenti al criterio specificato, verrà restituita una raccolta vuota.  
  
### Per elencare i file in una directory  
  
-   Usare uno degli overload del metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%2A?displayProperty=fullName>, fornendo il nome e il percorso della directory in cui cercare nel parametro `directory`.  L'esempio seguente restituisce tutti i file nella directory e li aggiunge e a  `ListBox1`.  
  
     [!code-vb[VbVbcnMyFileSystem#32](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-get-the-collection-of-files-in-a-directory_1.vb)]  
  
## Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il percorso non è valido per uno dei seguenti motivi: è una stringa di lunghezza zero, contiene solo spazi vuoti, contiene caratteri non validi o è il percorso di una periferica \(inizia con starts with \\\\.  \\\) \(<xref:System.ArgumentException>\).  
  
-   Il percorso non è valido in quanto è `Nothing` \(<xref:System.ArgumentNullException>\).  
  
-   `directory` non esiste \(<xref:System.IO.DirectoryNotFoundException>\).  
  
-   `directory` punta a un file esistente \(<xref:System.IO.IOException>\).  
  
-   La lunghezza del percorso supera la lunghezza massima definita dal sistema \(<xref:System.IO.PathTooLongException>\).  
  
-   Il nome di un file o di una directory nel percorso contiene i due punti \(:\) o ha un formato non valido \(<xref:System.NotSupportedException>\).  
  
-   L'utente non dispone delle autorizzazioni necessarie per visualizzare il percorso \(<xref:System.Security.SecurityException>\).  
  
-   L'utente non dispone delle autorizzazioni necessarie \(<xref:System.UnauthorizedAccessException>\).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFiles%2A>   
 [How to: Find Files with a Specific Pattern](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-find-files-with-a-specific-pattern.md)   
 [How to: Find Subdirectories with a Specific Pattern](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-find-subdirectories-with-a-specific-pattern.md)