---
title: 'Procedura: Caricare un file in Visual Basic | Microsoft Docs'
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
- networks, uploading files
- files, uploading
- uploading files
- UploadFile method
- My.Computer.Network.UploadFile method
ms.assetid: a8b37924-c523-4fd3-b5ca-cb0074df29cd
caps.latest.revision: 22
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
ms.openlocfilehash: 1663cc6ad0a6e5f2a940c050c75d403cffd1f53f
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-upload-a-file-in-visual-basic"></a>Procedura: caricare un file in Visual Basic
Il metodo <xref:Microsoft.VisualBasic.Devices.Network.UploadFile%2A> consente di caricare un file e archiviarlo in un percorso remoto. Se il parametro `ShowUI` è impostato su `True`, viene visualizzata una finestra di dialogo in cui è illustrato lo stato di avanzamento del processo di download. Qui l'utente può annullare l'operazione.  
  
### <a name="to-upload-a-file"></a>Per caricare un file  
  
-   Usare il metodo `UploadFile` per caricare un file, specificando il percorso del file di origine e il percorso della directory di destinazione come stringa o URI (Uniform Resource Identifier). Nell'esempio riportato di seguito il file `Order.txt` viene caricato in `http://www.cohowinery.com/uploads.aspx`.  
  
     [!code-vb[VbResourceTasks#6](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-upload-a-file_1.vb)]  
  
### <a name="to-upload-a-file-and-show-the-progress-of-the-operation"></a>Per caricare un file e visualizzare lo stato di avanzamento dell'operazione  
  
-   Usare il metodo `UploadFile` per caricare un file, specificando il percorso del file di origine e il percorso della directory di destinazione come stringa o URI. Nell'esempio riportato di seguito il file `Order.txt` viene caricato in `http://www.cohowinery.com/uploads.aspx` senza specificare un nome utente o una password, viene visualizzato lo stato di avanzamento del processo di caricamento ed è previsto un intervallo di timeout di 500 millisecondi.  
  
     [!code-vb[VbResourceTasks#7](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-upload-a-file_2.vb)]  
  
### <a name="to-upload-a-file-supplying-a-user-name-and-password"></a>Per caricare un file, specificando un nome utente e una password  
  
-   Usare il metodo `UploadFile` per caricare un file, specificando il percorso del file di origine e il percorso della directory di destinazione come stringa o URI e indicando il nome utente e la password. Nell'esempio riportato di seguito il file `Order.txt` viene caricato in `http://www.cohowinery.com/uploads.aspx` specificando il nome utente `anonymous` e una password vuota.  
  
     [!code-vb[VbResourceTasks#8](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-upload-a-file_3.vb)]  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Le condizioni seguenti possono generare un'eccezione:  
  
-   Il percorso file locale non è valido (<xref:System.ArgumentException>).  
  
-   Autenticazione non riuscita (<xref:System.Security.SecurityException>).  
  
-   Timeout della connessione (<xref:System.TimeoutException>).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Devices.Network?displayProperty=fullName>   
 <xref:Microsoft.VisualBasic.Devices.Network.UploadFile%2A>   
 [Procedura: Scaricare file](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-download-a-file.md)   
 [Procedura: analizzare percorsi di file](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)
