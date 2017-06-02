---
title: "Conferma | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8637aeaf-ac9e-49b8-93f4-da15dee45277
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Conferma
In questo esempio vengono illustrati quattro scenari comuni riguardanti l'utilizzo di <xref:System.Activities.Statements.CompensableActivity> e la conferma.L'esempio esegue quattro flussi di lavoro per illustrare la conferma.Questo esempio è disponibile nelle versioni dichiarativa e imperativa.  
  
## Confermare una CompensableActivity  
 Il primo flusso di lavoro illustra come confermare un'attività CompensableActivity ed è costituito da una sequenza di due istanze di <xref:System.Activities.Statements.CompensableActivity>.Dopo il completamento della seconda <xref:System.Activities.Statements.CompensableActivity>, un'attività Confirm conferma la prima attività.Quando il flusso di lavoro viene completato correttamente, tutte le istanze di <xref:System.Activities.Statements.CompensableActivity> che non sono state confermate o compensate vengono confermate automaticamente utilizzando l'ordine predefinito.Senza la conferma, la seconda <xref:System.Activities.Statements.CompensableActivity> sarebbe stata confermata per prima.  
  
## Compensazione esplicita  
 Il secondo scenario illustra l'effetto sulla conferma predefinita quando una <xref:System.Activities.Statements.CompensableActivity> viene compensata in modo esplicito.Il flusso di lavoro è costituito da una sequenza di due attività <xref:System.Activities.Statements.CompensableActivity>. Dopo il completamento della seconda, la prima viene compensata in modo esplicito.Di conseguenza, quando il flusso di lavoro viene completato, solo la seconda <xref:System.Activities.Statements.CompensableActivity> viene confermata.  
  
## Controllo dell'ordine di conferma per le attività CompensableActivity annidate  
 Il terzo scenario illustra come controllare l'ordine di conferma per <xref:System.Activities.Statements.CompensableActivity> annidate.Lo scenario è costituito da una <xref:System.Activities.Statements.CompensableActivity> come radice del flusso di lavoro.Il corpo della <xref:System.Activities.Statements.CompensableActivity> radice è una sequenza di tre <xref:System.Activities.Statements.CompensableActivity>.<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> per la <xref:System.Activities.Statements.CompensableActivity> radice è una sequenza che specifica di confermare la prima, quindi la seconda <xref:System.Activities.Statements.CompensableActivity> annidata.Quando il flusso di lavoro viene completato, conferma la <xref:System.Activities.Statements.CompensableActivity> radice che quindi conferma la prima, la seconda e la terza <xref:System.Activities.Statements.CompensableActivity> annidate, in tale ordine.Di conseguenza, l'ordine di conferma predefinito viene essenzialmente invertito.Poiché la terza <xref:System.Activities.Statements.CompensableActivity> non è stata confermata in modo esplicito come parte della <xref:System.Activities.Statements.CompensableActivity> radice da parte di <xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A>, viene confermata secondo l'ordine predefinito.Poiché, tuttavia, è la sola <xref:System.Activities.Statements.CompensableActivity> non confermata, ciò significa solo che viene confermata.  
  
## Ambito di variabili  
 Il quarto scenario illustra come la durata di variabili definite per una <xref:System.Activities.Statements.CompensableActivity> o una delle relative attività padre sia ancora nell'ambito quando vengono eseguiti i gestori <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>, <xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> o <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>, anche se l'attività o il flusso di lavoro è stato completato.Il flusso di lavoro è costituito da una sequenza di due <xref:System.Activities.Statements.CompensableActivity>.Nel corpo della prima, la variabile `mySum` viene impostata sulla somma di 5 e 10 e il risultato viene stampato.Nel corpo della seconda <xref:System.Activities.Statements.CompensableActivity> la somma viene impostata sulla somma della somma esistente più 7 e il risultato viene stampato.Viene definito un gestore conferma personalizzato per la prima <xref:System.Activities.Statements.CompensableActivity>, che stampa la somma, sottrae 7 e stampa nuovamente la somma.Controllando le somme stampate risulta chiaro che la variabile è nell'ambito non solo per i corpi di entrambe le <xref:System.Activities.Statements.CompensableActivity>, ma anche per <xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A>.  
  
#### Per eseguire l'esempio  
  
1.  Caricare la soluzione in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Eseguire l'applicazione ConfirmationSample.exe.  
  
3.  Osservare il seguente output:  
  
 **Explicit confirmation:Start of workflowCompensableActivity1: BodyCompensableActivity2: BodyCompensableActivity1: Confirmation HandlerEnd of workflowCompensableActivity2: Confirmation HandlerExplicit compensation:Start of workflowCompensableActivity1: BodyCompensableActivity2: BodyCompensableActivity1: Compensation HandlerEnd of workflowCompensableActivity2: Confirmation HandlerCustom confirmation handler:Start of workflowCompensableActivity1: BodyCompensableActivity2: BodyCompensableActivity3: BodyEnd of workflowCompensableActivity1: Confirmation HandlerCompensableActivity2: Confirmation HandlerCompensableActivity3: Confirmation HandlerVariable access in a confirmation handler:Start of workflowCompensableActivity1: BodyCompensableActivity1: The sum is: 15CompensableActivity2: BodyCompensableActivity2: Adding 7 to the sumCompensableActivity2: The sum is now: 22End of workflowCompensableActivity2: Confirmation HandlerCompensableActivity1: Confirmation HandlerCompensableActivity2: The sum is: 22CompensableActivity2: After subtracting 12 the sum is now: 10Press ENTER to exit.**  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Compensation\Confirmation`  
  
## Vedere anche