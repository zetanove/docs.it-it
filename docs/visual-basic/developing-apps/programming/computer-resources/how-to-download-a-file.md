---
title: "How to: Download a File in Visual Basic | Microsoft Docs"
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
  - "downloading Internet resources, files"
  - "downloading files"
  - "remote computers, downloading from"
  - "files, downloading"
  - "files, transferring"
ms.assetid: ac479f81-c0e2-4b99-af73-217f446b73da
caps.latest.revision: 22
caps.handback.revision: 22
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Download a File in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

È possibile utilizzare il metodo <xref:Microsoft.VisualBasic.Devices.Network.DownloadFile%2A> per scaricare un file remoto e archiviarlo in un percorso specifico.  Se il parametro `ShowUI` è impostato su `True`, verrà visualizzata una finestra di dialogo in cui viene illustrato lo stato di avanzamento del processo di download e che consente di annullare l'operazione.  Per impostazione predefinita, i file esistenti con lo stesso nome non vengono sovrascritti. Se si desidera sovrascrivere i file esistenti, impostare il parametro `overwrite` su `True`.  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il nome dell'unità non è valido \(<xref:System.ArgumentException>\).  
  
-   Non è stata fornita l'autenticazione necessaria \(<xref:System.UnauthorizedAccessException> o <xref:System.Security.SecurityException>\).  
  
-   Il server non risponde entro il `connectionTimeout` specificato \(<xref:System.TimeoutException>\).  
  
-   Il sito web ha rifiutato la richiesta \(<xref:System.Net.WebException>\).  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
> [!IMPORTANT]
>  Non basarsi sul nome del file per prendere decisioni in merito al relativo contenuto.  Ad esempio, è possibile che il file Form1.vb non sia un file di origine Visual Basic.  Prima di usare i dati nell'applicazione verificare tutti gli input.  È possibile che il contenuto del file non corrisponda a quanto previsto e che quindi i metodi per la lettura dal file non abbiano esito positivo.  
  
### Per scaricare un file  
  
-   Utilizzare il metodo `DownloadFile` per scaricare il file, specificando il percorso del file di destinazione come una stringa o URI e specificando il percorso dove archiviare il file.  Nell'esempio riportato di seguito viene eseguito il download del file `WineList.txt` da `http://www.cohowinery.com/downloads` e viene salvato in `C:\Documents and Settings\All Users\Documents`:  
  
     [!code-vb[VbResourceTasks#9](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-download-a-file_1.vb)]  
  
### Per scaricare un file, specificando un intervallo di timeout  
  
-   Utilizzare il metodo `DownloadFile` per eseguire il download del file, specificando il percorso del file di destinazione come una stringa o URI, il percorso dove archiviare il file e l'intervallo di timeout in millisecondi. Il valore predefinito di è 1000.  Nell'esempio riportato di seguito viene eseguito il download del file `WineList.txt` da `http://www.cohowinery.com/downloads` e viene salvato in `C:\Documents and Settings\All Users\Documents`, specificando un intervallo di timeout di 500 millisecondi:  
  
     [!code-vb[VbResourceTasks#10](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-download-a-file_2.vb)]  
  
### Per scaricare un file, fornendo un nome utente e una password  
  
-   Utilizzare il metodo `DownLoadFile` per eseguire il download del file, specificando il percorso del file di destinazione come una stringa o URI e il percorso dove archiviare il file, il nome utente e la password.  Nell'esempio riportato di seguito viene eseguito il download del file `WineList.txt` da `http://www.cohowinery.com/downloads` e viene salvato in `C:\Documents and Settings\All Users\Documents`, con il nome utente `anonymous` e una password vuota.  
  
     [!code-vb[VbResourceTasks#11](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-download-a-file_3.vb)]  
  
    > [!IMPORTANT]
    >  Il protocollo FTP utilizzato dal metodo `DownLoadFile` invia informazioni, comprese le password, in testo semplice e non deve pertanto essere utilizzato per la trasmissione di informazioni riservate.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Devices.Network>   
 <xref:Microsoft.VisualBasic.Devices.Network.DownloadFile%2A>   
 [How to: Upload a File](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-upload-a-file.md)   
 [Procedura: analizzare percorsi di file](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)