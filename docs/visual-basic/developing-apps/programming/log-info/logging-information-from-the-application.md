---
title: "Logging Information from the Application (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
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
  - "Log object"
  - "My.Log object"
  - "applications [Visual Basic], logging information from"
  - "logging"
  - "My.Application.Log object"
  - "examples [Visual Basic], logging application information"
ms.assetid: 8bf4f047-22d6-48d6-aec5-93b98ad5b8e8
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Logging Information from the Application (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Negli argomenti di questa sezione viene descritto come registrare le informazioni dall'applicazione utilizzando l'oggetto `My.Application.Log` o `My.Log` e come ampliare le capacità di registrazione dell'applicazione.  
  
 L'oggetto `Log` fornisce i metodi per scrivere le informazioni sui listener di log dell'applicazione, mentre la proprietà avanzata `TraceSource` dell'oggetto `Log` fornisce informazioni di configurazione dettagliate.  L'oggetto `Log` è configurato dal file di configurazione dell'applicazione.  
  
 L'oggetto `My.Log` è disponibile solo per le applicazioni ASP.NET.  Per le applicazioni client, utilizzare `My.Application.Log`.  Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.Logging.Log>.  
  
## Attività  
  
|Per|Vedere|  
|---------|------------|  
|Scrivere le informazioni sugli eventi nei log dell'applicazione.|[Procedura: scrivere messaggi di log](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)|  
|Scrivere le informazioni sulle eccezioni nei log dell'applicazione.|[How to: Log Exceptions](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)|  
|Scrivere le informazioni di traccia nei log dell'applicazione all'avvio e alla chiusura dell'applicazione.|[Procedura: registrare messaggi all'avvio o all'arresto dell'applicazione](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-messages-when-the-application-starts-or-shuts-down.md)|  
|Configurare `My.Application.Log` per scrivere le informazioni in un file di testo.|[How to: Write Event Information to a Text File](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-event-information-to-a-text-file.md)|  
|Configurare `My.Application.Log` per scrivere le informazioni in un log eventi.|[Procedura: scrivere nel log eventi di un'applicazione](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-to-an-application-event-log.md)|  
|Modificare la posizione dove `My.Application.Log` scrive le informazioni.|[Procedura dettagliata: modifica della posizione di inserimento delle informazioni con My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)|  
|Determinare la posizione dove `My.Application.Log` scrive le informazioni.|[Procedura dettagliata: individuazione della posizione di inserimento delle informazioni con My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)|  
|Creare un listener di log personalizzato per `My.Application.Log`.|[Walkthrough: Creating Custom Log Listeners](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-creating-custom-log-listeners.md)|  
|Filtrare l'output dei log `My.Application.Log`.|[Walkthrough: Filtering My.Application.Log Output](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-filtering-my-application-log-output.md)|  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 [Utilizzo dei log applicazione](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)   
 [Troubleshooting: Log Listeners](../../../../visual-basic/developing-apps/programming/log-info/troubleshooting-log-listeners.md)