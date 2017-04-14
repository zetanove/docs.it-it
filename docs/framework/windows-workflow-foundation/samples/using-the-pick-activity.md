---
title: "Utilizzo dell&#39;attivit&#224; Pick | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b89be812-a247-4025-b0e3-ffb20db027a6
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Utilizzo dell&#39;attivit&#224; Pick
In questo esempio viene illustrato come utilizzare l'attività <xref:System.Activities.Statements.Pick>.  
  
 L'attività <xref:System.Activities.Statements.Pick> fornisce il modello di controllo basato sugli eventiil cui comportamento è analogo a quello dell'istruzione C\# `switch`, che esegue solo uno dei rami nell'istruzione `switch`.A differenza dell'istruzione `switch` in cui l'esecuzione di un ramo viene effettuata in base a un valore, l'attività <xref:System.Activities.Statements.Pick> esegue un ramo in base alla modalità di completamento di un'attività.  
  
 In questo esempio un utente deve digitare il nome nella console entro un periodo di tempo specificato.L'attività <xref:System.Activities.Statements.Pick> nell'esempio dispone di due rami eseguiti in base al fatto che l'utente abbia o meno digitato il nome entro 5 secondi.Se l'utente digita il nome nei 5 secondi, viene eseguito il primo ramo che contiene un'attività `ReadLine` personalizzata; in caso contrario, viene eseguito l'altro ramo che contiene un'attività <xref:System.Activities.Statements.Delay>.Una volta digitato nella console, il nome dell'utente viene stampato nella console.Se un input non viene immesso entro 5 secondi, l'operazione è scaduta.  
  
## Dimostrazione  
 Attività <xref:System.Activities.Statements.Pick>.  
  
## Discussione  
 Nell'esempio è incluso un flusso di lavoro della finestra di progettazione e un flusso di lavoro codificato.  
  
 Flusso di lavoro della finestra di progettazione  
 Nella versione della finestra di progettazione dell'esempio viene illustrato come creare un flusso di lavoro nella finestra di progettazione.Sono inclusi i file seguenti:  
  
-   Program.cs: include la funzione `Main` che esegue il flusso di lavoro di esempio.  
  
-   ReadString.cs: attività personalizzata che legge alcuni input dalla console.  
  
-   Sequence1.xaml: flusso di lavoro creato tramite la finestra di progettazione utilizzata da Pick.  
  
 Flusso di lavoro codificato  
 Nella versione codificata dell'esempio viene illustrato come creare un flusso di lavoro nella finestra di progettazione.Sono inclusi i file seguenti:  
  
-   Program.cs: include la funzione `Main` che esegue il flusso di lavoro di esempio.  
  
-   ReadString.cs: attività personalizzata che legge alcuni input dalla console.  
  
#### Per utilizzare questo esempio  
  
1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione Pick.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Built-InActivities\Pick`  
  
## Vedere anche