---
title: 'Procedura: scaricare file in Visual Basic | Documentazione Microsoft'
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
- downloading Internet resources, files
- downloading files
- remote computers, downloading from
- files, downloading
- files, transferring
ms.assetid: ac479f81-c0e2-4b99-af73-217f446b73da
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
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: bd37b52d12876dad6ec4b2a1bb34f4987f933c08
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-download-a-file-in-visual-basic"></a>Procedura: scaricare file in Visual Basic
Il metodo <xref:Microsoft.VisualBasic.Devices.Network.DownloadFile%2A> può essere usato per scaricare un file remoto e archiviarlo in un percorso specifico. Se il parametro `ShowUI` è impostato su `True`, viene visualizzata una finestra che mostra lo stato di avanzamento del download e consente agli utenti di annullare l'operazione. Per impostazione predefinita non vengono sovrascritti i file esistenti con lo stesso nome. Se si desidera sovrascrivere i file esistenti, impostare il parametro `overwrite` su `True`.  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il nome dell'unità non è valido (<xref:System.ArgumentException>).  
  
-   L'autenticazione necessaria non è stata fornita (<xref:System.UnauthorizedAccessException> o <xref:System.Security.SecurityException>).  
  
-   Il server non risponde entro il `connectionTimeout` (<xref:System.TimeoutException>) specificato.  
  
-   La richiesta è stata rifiutata dal sito Web (<xref:System.Net.WebException>).  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
> [!IMPORTANT]
>  Non basarsi sul nome del file per prendere decisioni in merito al relativo contenuto. È possibile ad esempio che il file Form1.vb non sia un file di origine di Visual Basic. Prima di usare i dati nell'applicazione verificare tutti gli input. È possibile che il contenuto del file non corrisponda a quanto previsto e che quindi i metodi per la lettura dal file non abbiano esito positivo.  
  
### <a name="to-download-a-file"></a>Per scaricare un file  
  
-   Usare il metodo `DownloadFile` per scaricare il file, specificando il percorso del file di destinazione come stringa o URI e specificando la posizione in cui archiviare il file. Questo esempio scarica il file `WineList.txt` da `http://www.cohowinery.com/downloads` e lo salva in `C:\Documents and Settings\All Users\Documents`:  
  
     [!code-vb[VbResourceTasks#9](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-download-a-file_1.vb)]  
  
### <a name="to-download-a-file-specifying-a-time-out-interval"></a>Per scaricare un file, specificando un intervallo di timeout  
  
-   Usare il metodo `DownloadFile` per scaricare il file, specificando il percorso del file di destinazione come stringa o URI che specifica la posizione in cui archiviare il file e specificando l'intervallo di timeout in millisecondi (il valore predefinito è 1000). Questo esempio scarica il file `WineList.txt` da `http://www.cohowinery.com/downloads` e lo salva in `C:\Documents and Settings\All Users\Documents`, specificando un intervallo di timeout di 500 millisecondi:  
  
     [!code-vb[VbResourceTasks#10](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-download-a-file_2.vb)]  
  
### <a name="to-download-a-file-supplying-a-user-name-and-password"></a>Per scaricare un file, fornendo un nome utente e una password  
  
-   Usare il metodo `DownLoadFile` per scaricare il file, specificando il percorso del file di destinazione come stringa o URI e specificando la posizione in cui archiviare il file, il nome utente e la password. Questo esempio scarica il file `WineList.txt` da `http://www.cohowinery.com/downloads` e lo salva in `C:\Documents and Settings\All Users\Documents`, con il nome utente `anonymous` e una password vuota.  
  
     [!code-vb[VbResourceTasks#11](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-download-a-file_3.vb)]  
  
    > [!IMPORTANT]
    >  Il protocollo FTP utilizzato dal metodo `DownLoadFile` invia informazioni, comprese le password, in testo normale e non deve essere usato per trasmettere informazioni riservate.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Devices.Network>   
 <xref:Microsoft.VisualBasic.Devices.Network.DownloadFile%2A>   
 [Procedura: caricare un file](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-upload-a-file.md)   
 [Procedura: analizzare percorsi di file](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)

