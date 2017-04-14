---
title: "TransactionScope di base | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1e22b76a-76de-43b4-9be7-7a86ed3d5a44
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# TransactionScope di base
Questo esempio è costituito da quattro scenari che vengono eseguiti illustrando come annidare istanze di <xref:System.Activities.Statements.TransactionScope>.Nel primo scenario viene illustrato l'annidamento di un'attività di terze parti di cui l'autore non dispone di informazioni sulla modalità di costruzione.Nel secondo e nel terzo scenario viene illustrato come vengono rispettati timeout, mentre nello scenario finale viene illustrata l'impostazione di <xref:System.Activities.Statements.TransactionScope.AbortInstanceOnTransactionFailure%2A>.  
  
## Annidamento di TransactionScopeActivity  
 Il flusso di lavoro per il primo scenario è costituito da una sequenza di due attività <xref:System.Activities.Statements.WriteLine> e una <xref:System.Activities.Statements.TransactionScope>.Il corpo di <xref:System.Activities.Statements.TransactionScope> è una sequenza delle altre due attività <xref:System.Activities.Statements.WriteLine>, un'attività personalizzata che stampa l'identificatore locale della transazione e un'attività di terze parti.L'attività di terze parti `TransactionScopeTest` contiene un oggetto <xref:System.Activities.Statements.TransactionScope> anche se l'autore del flusso di lavoro non ha modo di esserne a conoscenza.In questo scenario viene illustrato che le attività <xref:System.Activities.Statements.TransactionScope> possono essere annidate.  
  
## Timeout  
 Il flusso di lavoro per il secondo scenario è quasi identico al primo.`TransactionScopeTest` è stato sostituito con <xref:System.Activities.Statements.TransactionScope>.Il corpo di <xref:System.Activities.Statements.TransactionScope> ha un ritardo di cinque secondi e il timeout per la transazione è impostato su due secondi.Il valore del timeout per l'attività <xref:System.Activities.Statements.TransactionScope> esterna è impostato su 10 secondi.Notare che viene rispettato il timeout inferiore presente nell'ambito e la transazione scade.  
  
 Il flusso di lavoro per il terzo scenario è quasi identico al secondo scenario.L'attività di ritardo è stata spostata dal corpo dell'attività <xref:System.Activities.Statements.TransactionScope> interna immediatamente dopo di essa nella sequenza, ovvero il corpo dell'attività <xref:System.Activities.Statements.TransactionScope> esterna.La transazione scade ancora perché il timeout di due secondi dell'attività <xref:System.Activities.Statements.TransactionScope> interna non è più applicabile.La transazione scade a 10 secondi quando viene superato il timeout dell'attività <xref:System.Activities.Statements.TransactionScope> esterna.  
  
## Interruzione in caso di errore della transazione  
 Questo flusso di lavoro è simile al terzo scenario, salvo il fatto che i timeout sono stati sostituiti dalla proprietà <xref:System.Activities.Statements.TransactionScope.AbortInstanceOnTransactionFailure%2A>.Notare che i flag di tutti gli elementi figlio interni, se impostati, devono corrispondere all'attività <xref:System.Activities.Statements.TransactionScope> esterna.In questo scenario non corrispondono e quindi viene generata un'eccezione all'apertura del flusso di lavoro.  
  
#### Per eseguire l’esempio  
  
1.  Aprire la soluzione BasicTransactionScopeSample.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B o scegliere **Compila soluzione** dal menu **Compila**.  
  
3.  Una volta completata la compilazione, premere F5 o scegliere **Avvia debug** dal menu **Debug**.In alternativa è possibile premere CTRL\+F5 o scegliere **Avvia senza eseguire debug** dal menu **Debug** per l'esecuzione senza debug.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Transactions\BasicTransactionScope`  
  
## Vedere anche