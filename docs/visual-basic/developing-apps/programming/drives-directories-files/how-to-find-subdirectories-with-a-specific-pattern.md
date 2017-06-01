---
title: 'Procedura: Trovare sottodirectory con un criterio specifico in Visual Basic | Microsoft Docs'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- pattern matching
- folders, finding
ms.assetid: c9265fd1-7483-4150-8b7f-ff642caa939d
caps.latest.revision: 16
author: dotnet-bot
ms.author: dotnetcontent
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 3fc7683c6629e2d94f3acb670810c6632efec094
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-find-subdirectories-with-a-specific-pattern-in-visual-basic"></a>Procedura: cercare sottodirectory con un modello specifico in Visual Basic
Il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetDirectories%2A> restituisce una raccolta di stringhe di sola lettura che rappresentano i nomi di percorso per le sottodirectory di una directory. È possibile usare il parametro `wildCards` per specificare un criterio specifico. Se si vogliono includere i contenuti delle sottodirectory nella ricerca, impostare il parametro `searchType` su `SearchOption.SearchAllSubDirectories`.  
  
 Se non vengono trovate directory corrispondenti al criterio specificato, verrà restituita una raccolta vuota.  
  
### <a name="to-find-subdirectories-with-a-specific-pattern"></a>Per trovare sottodirectory con un criterio specifico  
  
-   Usare il metodo `GetDirectories`, specificando il nome e percorso della directory che si vuole cercare. L'esempio seguente restituisce tutte le directory nella struttura di directory che contengono la parola "Logs" nel nome e li aggiunge a `ListBox1`.  
  
     [!code-vb[VbVbcnFileAccess#1](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-find-subdirectories-with-a-specific-pattern_1.vb)]  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il percorso non è valido per uno dei motivi seguenti: è una stringa di lunghezza zero, contiene solo spazi vuoti, contiene caratteri non validi o è il percorso di un dispositivo (inizia con \\\\.\\) (<xref:System.ArgumentException>).  
  
-   Il percorso non è valido in quanto è `Nothing` (<xref:System.ArgumentNullException>).  
  
-   Uno o più caratteri jolly specificati è `Nothing`, una stringa vuota o contiene solo spazi (<xref:System.ArgumentNullException>).  
  
-   `directory` non esiste (<xref:System.IO.DirectoryNotFoundException>).  
  
-   `directory` punta a un file esistente (<xref:System.IO.IOException>).  
  
-   La lunghezza del percorso supera la lunghezza massima definita dal sistema (<xref:System.IO.PathTooLongException>).  
  
-   Il nome di un file o di una cartella nel percorso contiene i due punti (:) o ha un formato non valido (<xref:System.NotSupportedException>).  
  
-   L'utente non dispone delle autorizzazioni necessarie per visualizzare il percorso (<xref:System.Security.SecurityException>).  
  
-   L'utente non dispone delle autorizzazioni necessarie (<xref:System.UnauthorizedAccessException>).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetDirectories%2A>   
 [Procedura: trovare file con un modello specifico](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-find-files-with-a-specific-pattern.md)
