---
title: "Gestione della concorrenza con DependentTransaction  | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b85a97d8-8e02-4555-95df-34c8af095148
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Gestione della concorrenza con DependentTransaction 
Il metodo <xref:System.Transactions.Transaction.DependentClone%2A> consente di clonare un oggetto <xref:System.Transactions.Transaction>.L'unico scopo di questo metodo è impedire il commit della transazione mentre altri blocchi di codice \(ad esempio un thread di lavoro\) stanno agendo su di essa.Quando le operazioni eseguite all'interno della transazione clonata sono state completate e il sistema è pronto ad eseguirne il commit, la transazione clonata può utilizzare il metodo <xref:System.Transactions.DependentTransaction.Complete%2A> per informare il creatore della transazione originale in merito.In questo modo è possibile preservare la coerenza e la correttezza dei dati.  
  
 La classe <xref:System.Transactions.DependentTransaction> può inoltre essere utilizzata per gestire la concorrenza tra attività asincrone.In questo scenario, la transazione padre può continuare a eseguire qualsiasi codice mentre la transazione duplicata dipendente agisce sulle proprie attività.In altre parole, l'esecuzione della transazione padre può procedere liberamente anche durante l'esecuzione della transazione dipendente.  
  
## Creazione di un clone dipendente  
 Per creare una transazione dipendente, chiamare il metodo <xref:System.Transactions.Transaction.DependentClone%2A> e passare l'enumerazione <xref:System.Transactions.DependentCloneOption> come parametro.Questo parametro definisce il comportamento della transazione nel caso in cui il metodo `Commit` venga chiamato nella transazione padre prima che il clone dipendente chiami il metodo <xref:System.Transactions.DependentTransaction.Complete%2A> per indicare che è pronto per il commit.Di seguito sono elencati i valori validi di questo parametro e le relative descrizioni.  
  
-   Il valore <xref:System.Transactions.DependentCloneOption> consente di creare una transazione dipendente che blocca il processo di commit della transazione padre finché non scade il timeout di quest'ultima o finché il metodo <xref:System.Transactions.DependentTransaction.Complete%2A> non viene chiamato in tutte le transazioni dipendenti a indicarne il completamento.Ciò è utile quando il client desidera che la transazione padre esegua il commit solo dopo il completamento delle transazioni dipendenti.Se la transazione padre termina la propria esecuzione prima delle transazioni dipendenti e chiama il metodo <xref:System.Transactions.CommittableTransaction.Commit%2A> sulla transazione, il processo di commit viene bloccato in un stato che consente l'esecuzione di operazioni aggiuntive relative alla transazione e la creazione di nuove integrazioni finché tutte le transazioni dipendenti non chiamano il metodo <xref:System.Transactions.DependentTransaction.Complete%2A>.Il processo di commit della transazione inizia non appena tutte le transazioni dipendenti terminano la propria esecuzione e chiamano il metodo <xref:System.Transactions.DependentTransaction.Complete%2A>.  
  
-   Il valore <xref:System.Transactions.DependentCloneOption>, invece, crea una transazione dipendente che viene interrotta automaticamente se il metodo <xref:System.Transactions.CommittableTransaction.Commit%2A> viene chiamato sulla transazione padre prima che il metodo <xref:System.Transactions.DependentTransaction.Complete%2A> venga chiamato sulla transazione dipendente.In questo caso, il sistema esegue il rollback di qualsiasi operazione svolta nella transazione dipendente nell'intervallo di durata di un'unica transazione e nessuna entità ha la possibilità di eseguire il commit parziale della transazione dipendente.  
  
 Quando l'applicazione termina le proprie operazioni relative alla transazione dipendente, è necessario chiamare il metodo <xref:System.Transactions.DependentTransaction.Complete%2A> una sola volta. In caso contrario, viene generata un'eccezione <xref:System.InvalidOperationException>.Dopo l'esecuzione di questa chiamata, evitare l'esecuzione di altre operazioni sulla transazione o verrà generata un'eccezione.  
  
 Nell'esempio di codice seguente viene mostrato come creare una transazione dipendente per gestire due attività simultanee clonando una transazione dipendente e passandola a un thread di lavoro.  
  
```csharp  
public class WorkerThread  
{  
    public void DoWork(DependentTransaction dependentTransaction)  
    {  
        Thread thread = new Thread(ThreadMethod);  
        thread.Start(dependentTransaction);   
    }  
  
    public void ThreadMethod(object transaction)   
    {   
        DependentTransaction dependentTransaction = transaction as DependentTransaction;  
        Debug.Assert(dependentTransaction != null);   
        try  
        {  
            using(TransactionScope ts = new TransactionScope(dependentTransaction))  
            {  
                /* Perform transactional work here */   
                ts.Complete();  
            }  
        }  
        finally  
        {  
            dependentTransaction.Complete();   
             dependentTransaction.Dispose();   
        }  
    }  
  
//Client code   
using(TransactionScope scope = new TransactionScope())  
{  
    Transaction currentTransaction = Transaction.Current;  
    DependentTransaction dependentTransaction;      
    dependentTransaction = currentTransaction.DependentClone(DependentCloneOption.BlockCommitUntilComplete);  
    WorkerThread workerThread = new WorkerThread();  
    workerThread.DoWork(dependentTransaction);  
    /* Do some transactional work here, then: */  
    scope.Complete();  
}  
  
```  
  
 Il codice client crea un ambito transazionale che imposta anch'esso la transazione di ambiente.Anziché passare la transazione di ambiente al thread di lavoroè necessario clonare la transazione corrente \(di ambiente\) chiamando il metodo <xref:System.Transactions.Transaction.DependentClone%2A> nella transazione corrente e quindi passare la transazione dipendente al thread di lavoro.  
  
 Il metodo `ThreadMethod` viene eseguito nel nuovo thread.Il client avvia un nuovo thread, passando la transazione dipendente come parametro `ThreadMethod`.  
  
 Poiché la transazione dipendente viene creata con il valore <xref:System.Transactions.DependentCloneOption>, il commit della transazione può avvenire solo dopo il completamento di tutte le operazioni transazionali nel secondo thread e dopo che il metodo <xref:System.Transactions.DependentTransaction.Complete%2A> sia stato chiamato sulla transazione dipendente.Ciò implica che se l'ambito client termina \(quando il client tenta di eliminare l'oggetto di transazione al termine dell'istruzione **using**\) prima che il nuovo thread chiami il metodo <xref:System.Transactions.DependentTransaction.Complete%2A> sulla transazione dipendente, il codice client si blocca finché il metodo <xref:System.Transactions.DependentTransaction.Complete%2A> non viene chiamato sulla transazione dipendente.A questo punto, la transazione può concludere la procedura di commit o di interruzione.  
  
## Problemi di concorrenza  
 Quando si utilizza la classe <xref:System.Transactions.DependentTransaction> occorre prendere in considerazione alcuni problemi di concorrenza aggiuntivi:  
  
-   Se il thread di lavoro esegue il rollback della transazione ma la transazione padre tenta di eseguirne il commit, viene generata un'eccezione <xref:System.Transactions.TransactionAbortedException>.  
  
-   È necessario creare un nuovo clone dipendente per ogni thread di lavoro della transazione.Evitare di passare lo stesso clone dipendente a più thread, in quando solo uno di essi è in grado di chiamare il metodo <xref:System.Transactions.DependentTransaction.Complete%2A> sul clone.  
  
-   Se il thread di lavoro genera un nuovo thread di lavoro, assicurarsi di creare un clone dipendente a partire dal clone dipendente e di passarlo al nuovo thread.  
  
## Vedere anche  
 <xref:System.Transactions.DependentTransaction>