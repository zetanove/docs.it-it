---
title: 'Procedura: Creare una directory in Visual Basic | Microsoft Docs'
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
- directories [Visual Basic], creating
- folders [Visual Basic], creating
ms.assetid: 0351a2ca-24d8-43b5-bb39-9b99e6401cff
caps.latest.revision: 19
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
ms.openlocfilehash: 81afe64204fda468f452f86171b15080f9c3d948
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-create-a-directory-in-visual-basic"></a>Procedura: creare una directory in Visual Basic
Usare il metodo `CreateDirectory` dell'oggetto `My.Computer.FileSystem` per la creazione di directory.  
  
 Se la directory esiste già, non verranno generate eccezioni.  
  
### <a name="to-create-a-directory"></a>Per creare una directory  
  
-   Usare il metodo `CreateDirectory` specificando il percorso completo della posizione in cui deve essere creata la directory. Nell'esempio riportato di seguito la directory `NewDirectory` viene creata in `C:\Documents and Settings\All Users\Documents`.  
  
     [!code-vb[VbVbcnMyFileSystem#2](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-create-a-directory_1.vb)]  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il nome della directory non è valido. Contiene ad esempio caratteri non validi o è costituito solo da uno spazio (<xref:System.ArgumentException>).  
  
-   La directory padre della directory da creare è di sola lettura (<xref:System.IO.IOException>).  
  
-   Il nome della directory è `Nothing` (<xref:System.ArgumentNullException>).  
  
-   Il nome della directory è troppo lungo (<xref:System.IO.PathTooLongException>).  
  
-   Il nome della directory è un carattere due punti ":" (<xref:System.NotSupportedException>).  
  
-   L'utente non è autorizzato a creare la directory (<xref:System.UnauthorizedAccessException>).  
  
-   L'utente non ha le autorizzazioni richieste in una situazione di attendibilità parziale (<xref:System.Security.SecurityException>).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.CreateDirectory%2A>   
 [Creazione, eliminazione e spostamento di file e directory](../../../../visual-basic/developing-apps/programming/drives-directories-files/creating-deleting-and-moving-files-and-directories.md)
