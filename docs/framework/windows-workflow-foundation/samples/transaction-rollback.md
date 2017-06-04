---
title: "Rollback di transazioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7f377147-7529-4689-a588-608cee87fdf8
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Rollback di transazioni
In questo esempio viene illustrato come creare un oggetto <xref:System.Activities.NativeActivity> personalizzato che accede all'oggetto <xref:System.Activities.RuntimeTransactionHandle> di ambiente per ottenere la transazione di ambiente ed eseguirne il rollback in modo esplicito.  
  
## Dettagli dell'esempio  
 Nel flusso di lavoro una transazione viene completata automaticamente quando l'oggetto <xref:System.Activities.Statements.TransactionScope> o <xref:System.ServiceModel.Activities.TransactedReceiveScope> più esterno viene completato.Una transazione esegue in modo implicito il rollback quando un'eccezione non gestita viene propagata attraverso il limite di ambito.In alcuni casi può tuttavia risultare opportuno eseguire il rollback di una transazione in modo esplicito senza dover generare un'eccezione.In questo caso, è possibile utilizzare l'attività di rollback personalizzata come quella disponibile in questo esempio per interrompere in modo esplicito la transazione di ambiente e fornire un motivo facoltativo per l'eccezione.  
  
 `RollbackActivity` è un'attività <xref:System.Activities.NativeActivity> in quanto richiede l'accesso alle proprietà di esecuzione per ottenere l'oggetto <xref:System.Activities.RuntimeTransactionHandle> di ambiente.Nel metodo `Execute`, ottiene <xref:System.Activities.RuntimeTransactionHandle> e controlla se è `null` che indica che l'attività è stata utilizzata senza una transazione di runtime di ambiente.Ottiene quindi la transazione, controllando nuovamente se `null` è presente.È possibile che <xref:System.Activities.RuntimeTransactionHandle> sia di ambiente senza avere mai inizializzato una transazione di runtime.Infine la transazione viene interrotta chiamando <xref:System.Transactions.Transaction.Rollback%2A> e specificando un'eccezione fornita dall'utente o un'eccezione generica che dichiara che l'attività ha eseguito il rollback della transazione.  
  
 Il flusso di lavoro di esempio è costituito da un oggetto <xref:System.Activities.Statements.TransactionScope> il cui corpo stampa lo stato della transazione prima e dopo l'esecuzione di `RollbackActivity`.Notare che anche se il rollback della transazione è stato eseguito, <xref:System.Activities.Statements.TransactionScope> viene esegue fino al completamento e non interrompe il flusso di lavoro finché il corpo non viene completato.Il flusso di lavoro viene  interrotto perché la proprietà <xref:System.Activities.Statements.TransactionScope.AbortInstanceOnTransactionFailure%2A> viene impostata sul valore predefinito `true`.  
  
#### Per utilizzare questo esempio  
  
1.  Caricare la soluzione TransactionRollback.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Premere CTRL\+F5 per eseguire l'applicazione.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\Transactions\TransactionRollback`  
  
## Vedere anche  
 [Transazioni](../../../../docs/framework/windows-workflow-foundation//workflow-transactions.md)