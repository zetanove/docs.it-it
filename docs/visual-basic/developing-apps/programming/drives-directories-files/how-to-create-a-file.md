---
title: 'Procedura: Creare un file in Visual Basic | Microsoft Docs'
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
- text files, creating
- files, creating
ms.assetid: 0253bb6d-5519-4a50-b882-b93ef5cca0d9
caps.latest.revision: 15
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
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: f9e2b11b6eed10bac04d22b202e7e16cfa70225d
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-create-a-file-in-visual-basic"></a>Procedura: creare un file in Visual Basic
In questo esempio viene creato un file di testo vuoto nel percorso specificato usando il metodo <xref:System.IO.File.Create%2A> nella classe <xref:System.IO.File>.  
  
## <a name="example"></a>Esempio  
 [!code-vb[VbFileIOMisc#1](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-create-a-file_1.vb)]  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Usare la variabile `file` per scrivere il file.  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Se il file esiste già, viene sostituito.  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il nome del percorso non è valido. Contiene ad esempio caratteri non validi o è costituito solo da uno spazio (<xref:System.ArgumentException>).  
  
-   Il percorso è di sola lettura (<xref:System.IO.IOException>).  
  
-   Il nome del percorso è `Nothing` (<xref:System.ArgumentNullException>).  
  
-   Il nome del percorso è troppo lungo (<xref:System.IO.PathTooLongException>).  
  
-   Il percorso non è valido (<xref:System.IO.DirectoryNotFoundException>).  
  
-   Il percorso contiene solo due punti ":" (<xref:System.NotSupportedException>).  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 È possibile che venga generata un'eccezione <xref:System.Security.SecurityException> in ambienti ad attendibilità parziale.  
  
 La chiamata al metodo <xref:System.IO.File.Create%2A> richiede <xref:System.Security.Permissions.FileIOPermission>.  
  
 Viene generata un'eccezione <xref:System.UnauthorizedAccessException> se l'utente non dispone dell'autorizzazione per creare il file.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.IO>   
 <xref:System.IO.File.Create%2A>   
 [Uso di librerie da codice parzialmente attendibile](../../../../framework/misc/using-libraries-from-partially-trusted-code.md)   
 [Nozioni fondamentali sulla sicurezza per l’accesso al codice](https://msdn.microsoft.com/library/33tceax8)
