---
title: "Eseguire un flusso di lavoro in un oggetto TransactionScope imperativo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bd0e8686-c1d0-4400-a541-da94ed03afc7
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Eseguire un flusso di lavoro in un oggetto TransactionScope imperativo
In questo esempio viene illustrato come eseguire un flusso di lavoro tramite <xref:System.Activities.WorkflowInvoker> in un oggetto <xref:System.Transactions.Transaction> da codice C\# imperativo.  
  
## Dettagli dell'esempio  
 Nel codice C\# imperativo, l'oggetto <xref:System.Transactions.TransactionScope> viene utilizzato per incapsulare un set di operazioni che viene eseguito nella stessa transazione.L'oggetto <xref:System.Transactions.TransactionScope> funziona creando una transazione di ambiente e inizializzando la proprietà <xref:System.Transactions.Transaction.Current%2A> alla quale è possibile accedere da qualsiasi operazione eseguita in tale thread.  
  
 Per ottenere il comportamento equivalente nel flusso di lavoro, il runtime deve effettuare un'operazione aggiuntiva di inizializzazione della proprietà <xref:System.Transactions.Transaction.Current%2A> prima dell'esecuzione di ogni attività, in quanto un flusso di lavoro non gestisce l'affinità di thread tra attività.Con questo supporto runtime, il comportamento risultante è che, durante l'esecuzione di un flusso di lavoro con <xref:System.Activities.WorkflowInvoker> all'interno di un oggetto <xref:System.Transactions.TransactionScope>, tutte le attività vengono eseguite nel contesto della transazione di ambiente creata dall'oggetto <xref:System.Transactions.TransactionScope>.  
  
 Un flusso di lavoro può disporre di una sola transazione di ambiente per ogni istanza del flusso di lavoro; transazioni annidate non sono disponibili.Anche se il flusso di lavoro contiene un'attività <xref:System.Activities.Statements.TransactionScope>, ciò non crea una nuova transazione interna.Al contrario, viene riutilizzata la transazione di ambiente creata all'esterno del flusso di lavoro.  
  
 Nell'esempio viene iniziato un nuovo oggetto <xref:System.Transactions.Transaction.TransactionScope>, viene stampato l'ID transazione e viene avviato un flusso di lavoro tramite <xref:System.Activities.WorkflowInvoker>.Il flusso di lavoro stampa nuovamente l'ID transazione, mostrando che si tratta della stessa transazione, quindi esegue un oggetto <xref:System.Activities.Statements.TransactionScope> e viene completato.La chiamata al metodo <xref:System.Activities.WorkflowInvoker.Invoke%2A> su <xref:System.Activities.WorkflowInvoker> è sincrona, pertanto il thread originale viene bloccato fino a quando il flusso di lavoro non viene completato.Una volta completato il flusso di lavoro, la transazione viene completata e le risorse eliminate.  
  
#### Per utilizzare questo esempio  
  
1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione ImperativeTransactionSample.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\Transactions\ImperativeTransaction`  
  
## Vedere anche