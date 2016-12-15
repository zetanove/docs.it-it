---
title: "La codifica non pu&#242; essere impostata su Nothing | Microsoft Docs"
ms.custom: ""
ms.date: "11/16/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 59f7c731-8291-4a85-bf51-c225e48cdc84
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# La codifica non pu&#242; essere impostata su Nothing
Un tentativo di leggere o scrivere in un file non è riuscito perché il parametro `encoding` è stato impostato su `Nothing` ma richiede un valore valido.  
  
 <xref:System.Text.Encoding> consente di determinare quale codifica usare durante la scrittura in un file. Il valore predefinito è UTF\-8.  
  
### Per correggere l'errore  
  
-   Specificare un valore valido per il parametro `encoding`.  
  
## Vedere anche  
 [File Encodings](../../visual-basic/developing-apps/programming/drives-directories-files/file-encodings.md)   
 [Reading from Files](../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)   
 [Writing to Files](../../visual-basic/developing-apps/programming/drives-directories-files/writing-to-files.md)   
 [Metodo My.Computer.FileSystem.ReadAllText](http://msdn.microsoft.com/it-it/3a7ac8be-fb1d-4087-bc65-167d6754d57f)   
 [Metodo My.Computer.FileSystem.WriteAllText](http://msdn.microsoft.com/it-it/f507460c-87d9-4504-b74f-3ff825c7d5c4)