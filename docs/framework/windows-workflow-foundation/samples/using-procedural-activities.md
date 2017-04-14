---
title: "Utilizzo di attivit&#224; procedurali | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1c67f739-3878-48ad-806c-b2ce0d6733a0
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Utilizzo di attivit&#224; procedurali
Nell'esempio vengono utilizzate le attività <xref:System.Activities.Statements.Sequence>, <xref:System.Activities.Statements.Assign>, <xref:System.Activities.Statements.If>, <xref:System.Activities.Statements.While>, <xref:System.Activities.Statements.Switch%601>, <xref:System.Activities.Statements.TryCatch>e <xref:System.Activities.Statements.WriteLine> per implementare un gioco per indovinare un numero.Il gioco seleziona un numero casuale e il giocatore deve indovinare il numero.Quando il giocatore invia un numero errato, il flusso di lavoro fornisce un suggerimento che indica di provare a con un numero più alto o più basso.Se il giocatore indovina il numero in meno di 7 tentativi, viene visualizzato all'utente un messaggio di congratulazioni speciali.  
  
## Attività personalizzate in questo esempio  
  
### ReadLine  
 Legge una riga di testo dalla console.Questa attività deriva dalla classe <xref:System.Activities.NativeActivity> e crea un segnalibro ripreso dall'applicazione console quando viene letta una riga.  
  
### PromptInt  
 Richiede all'utente di digitare un numero, quindi lo legge da una finestra della console.L'attività deriva da <xref:System.Activities.Activity%601> e utilizza le attività <xref:System.Activities.Statements.WriteLine> e `ReadLine`.  
  
##### Per utilizzare questo esempio  
  
1.  Tramite [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione GuessingGame.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere CTRL\+F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Built-InActivities\Procedurals`  
  
## Vedere anche