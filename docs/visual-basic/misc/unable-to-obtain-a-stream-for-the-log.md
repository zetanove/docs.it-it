---
title: "Impossibile ottenere un flusso per il log | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrApplicationLog_ExhaustedPossibleStreamNames"
ms.assetid: 33994f52-8efb-4790-a459-033e5c1db632
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Impossibile ottenere un flusso per il log
Impossibile ottenere un flusso per il log. I possibili nome file basati su \<nome\> sono già in uso.  
  
 La classe <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> non può creare un nuovo file di log, perché tutti i nomi potenziali dei file di log basati su \<nome\> sono già in uso.  
  
 L'esistenza di un numero eccessivo di file di log può indicare un problema architetturale dell'applicazione. Per altre informazioni, vedere la documentazione per la classe <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener>.  
  
### Per correggere l'errore  
  
1.  Impostare la proprietà <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.LogFileCreationSchedule%2A> su <xref:Microsoft.VisualBasic.Logging.LogFileCreationScheduleOption> o <xref:Microsoft.VisualBasic.Logging.LogFileCreationScheduleOption> per includere nel nome del file di log un indicatore di data.  
  
2.  Archiviare i log esistenti e rimuoverli dal computer per consentire all'oggetto <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> di creare nuovi log.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener>   
 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.LogFileCreationSchedule%2A>   
 [Oggetto My.Application.Log](../../visual-basic/language-reference/objects/my-application-log-object.md)   
 [My.Log Object](../../visual-basic/language-reference/objects/my-log-object.md)