---
title: "Implementazione di una transazione esplicita mediante CommittableTransaction  | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 29efe5e5-897b-46c2-a35f-e599a273acc8
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Implementazione di una transazione esplicita mediante CommittableTransaction 
A differenza della classe <xref:System.Transactions.TransactionScope>, che consente di utilizzare le transazioni in modo implicito, la classe <xref:System.Transactions.CommittableTransaction> consente di utilizzare le transazioni in modo esplicito.Questa classe è utile nelle applicazioni che utilizzano la stessa transazione per più chiamate di funzione o di thread.A differenza della classe <xref:System.Transactions.TransactionScope>, il writer di applicazione deve chiamare in modo specifico i metodi <xref:System.Transactions.Transaction.Rollback%2A> e <xref:System.Transactions.CommittableTransaction.Commit%2A>, rispettivamente per interrompere la transazione o per eseguirne il commit.  
  
## Panoramica sulla classe CommittableTransaction  
 La classe <xref:System.Transactions.CommittableTransaction> deriva dalla classe <xref:System.Transactions.Transaction> e pertanto ne presenta tutte le funzionalità.Il metodo <xref:System.Transactions.Transaction.Rollback%2A> della classe <xref:System.Transactions.Transaction> è particolarmente utile e può inoltre essere utilizzato per eseguire il rollback di un oggetto <xref:System.Transactions.CommittableTransaction>.  
  
 La classe <xref:System.Transactions.Transaction> è simile alla classe <xref:System.Transactions.CommittableTransaction>. Tuttavia, a differenza di quest'ultima, la prima non prevede alcun metodo `Commit`.Ciò consente di passare l'oggetto di transazione \(o i cloni di tale oggetto\) agli altri metodi \(eventualmente presenti su altri thread\) e al contempo controllare il momento in cui viene eseguito il commit della transazione.Benché il codice chiamato sia in grado di integrarsi nella transazione e di votare sull'esito di quest'ultima, soltanto il creatore dell'oggetto <xref:System.Transactions.CommittableTransaction> può eseguire il commit della transazione.  
  
 Quando si utilizza la classe <xref:System.Transactions.CommittableTransaction> è opportuno tenere presente i punti seguenti.  
  
-   La creazione di una transazione <xref:System.Transactions.CommittableTransaction> non comporta l'impostazione della transazione di ambiente.Questa transazione deve essere impostata e reimpostata in modo specifico, in modo da garantire che i gestori di risorse possano funzionare nel contesto temporale e transazionale appropriato.Per definire la transazione di ambiente corrente è necessario impostare la proprietà statica <xref:System.Transactions.Transaction.Current%2A> dell'oggetto globale <xref:System.Transactions.Transaction>.  
  
-   Gli oggetti <xref:System.Transactions.CommittableTransaction> non possono essere riutilizzati.In particolare, un oggetto <xref:System.Transactions.CommittableTransaction> per cui è stato eseguito il commit o il rollback non può essere utilizzato nuovamente in una transazione.In altre parole, non può essere impostato come contesto della transazione di ambiente corrente.  
  
## Creazione di una transazione CommittableTransaction  
 Nell'esempio seguente viene creata una nuova istanza della classe <xref:System.Transactions.CommittableTransaction> e quindi ne viene eseguito il commit.  
  
 [!code-csharp[Tx_CommittableTx#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/tx_committabletx/cs/committabletxwithsql.cs#1)]
 [!code-vb[Tx_CommittableTx#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/tx_committabletx/vb/committabletxwithsql.vb#1)]  
  
 La creazione di una transazione <xref:System.Transactions.CommittableTransaction> non comporta l'impostazione automatica del contesto della transazione di ambiente.Ne consegue che a tale transazione non può appartenere alcuna operazione di gestore di risorse.La proprietà statica <xref:System.Transactions.Transaction.Current%2A> dell'oggetto globale <xref:System.Transactions.Transaction> viene utilizzata per impostare o recuperare la transazione di ambiente e l'applicazione deve impostarla manualmente per garantire che i gestori di risorse possano partecipare alla transazione.È inoltre consigliabile salvare la transazione di ambiente precedente e ripristinarla al termine dell'utilizzo dell'oggetto <xref:System.Transactions.CommittableTransaction>.  
  
 Per eseguire il commit di una transazione è necessario chiamare esplicitamente il metodo <xref:System.Transactions.CommittableTransaction.Commit%2A>.Per eseguire il rollback di una transazione è invece necessario chiamare il metodo <xref:System.Transactions.Transaction.Rollback%2A>.È importante notare che tutte le risorse coinvolte in una transazione <xref:System.Transactions.CommittableTransaction> restano bloccate finché non viene eseguito il commit o il rollback di tale transazione.  
  
 Un oggetto <xref:System.Transactions.CommittableTransaction> può essere utilizzato per più thread e chiamate di funzione.In caso di errore, tuttavia, spetta allo sviluppatore dell'applicazione gestire le eccezioni e chiamare in modo specifico il metodo <xref:System.Transactions.Transaction.Rollback%28System.Exception%29>.  
  
## Commit asincrono  
 La classe <xref:System.Transactions.CommittableTransaction> fornisce inoltre un meccanismo per eseguire il commit asincrono di una transazione.Il commit di una transazione può richiedere molto tempo, in quanto può coinvolgere varie operazioni di accesso al database nonché un'eventuale latenza di rete.Nelle applicazioni ad elevata velocità effettiva è essenziale evitare i deadlock. A tale scopo, è possibile utilizzare il commit asincrono per concludere le operazioni transazionali il prima possibile ed eseguire l'operazione di commit come attività in background.I metodi <xref:System.Transactions.CommittableTransaction.BeginCommit%2A> e <xref:System.Transactions.CommittableTransaction.EndCommit%2A> della classe <xref:System.Transactions.CommittableTransaction> consentono di raggiungere tale obiettivo.  
  
 È possibile chiamare il metodo <xref:System.Transactions.CommittableTransaction.BeginCommit%2A> per avviare la procedura di commit in un thread del pool di thread.È inoltre possibile chiamare il metodo <xref:System.Transactions.CommittableTransaction.EndCommit%2A> per determinare se il commit della transazione è stato effettivamente eseguito.Se per qualche motivo il commit della transazione ha avuto esito negativo, il metodo <xref:System.Transactions.CommittableTransaction.EndCommit%2A> genera un'eccezione di transazione.Se al momento della chiamata al metodo <xref:System.Transactions.CommittableTransaction.EndCommit%2A> il commit della transazione non è ancora stato eseguito, il chiamante resta bloccato finché la transazione non viene interrotta o non ne viene eseguito il commit.  
  
 Il modo più semplice per eseguire un commit asincrono è ricorrere a un metodo callback che viene chiamato al completamento della procedura di commit.Tuttavia, è necessario chiamare il metodo <xref:System.Transactions.CommittableTransaction.EndCommit%2A> sull'oggetto <xref:System.Transactions.CommittableTransaction> inizialmente utilizzato per effettuare la chiamata.Per ottenere tale oggetto è possibile eseguire il downcast del parametro *IAsyncResult* del metodo callback, in quanto la classe <xref:System.Transactions.CommittableTransaction> implementa la classe <xref:System.IAsyncResult>.  
  
 L'esempio seguente illustra come eseguire un commit asincrono.  
  
```csharp  
public void DoTransactionalWork()  
{  
     Transaction oldAmbient = Transaction.Current;  
     CommittableTransaction committableTransaction = new CommittableTransaction();  
     Transaction.Current = committableTransaction;  
  
     try  
     {  
          /* Perform transactional work here */  
          // No errors - commit transaction asynchronously  
          committableTransaction.BeginCommit(OnCommitted,null);  
     }  
     finally  
     {  
          //Restore the ambient transaction   
          Transaction.Current = oldAmbient;  
     }  
}  
void OnCommitted(IAsyncResult asyncResult)  
{  
     CommittableTransaction committableTransaction;  
     committableTransaction = asyncResult as CommittableTransaction;     
     Debug.Assert(committableTransaction != null);  
     try  
     {  
          using(committableTransaction)  
          {  
               committableTransaction.EndCommit(asyncResult);  
          }  
     }  
     catch(TransactionException e)  
     {  
          //Handle the failure to commit  
     }  
}  
```  
  
## Vedere anche  
 [Implementazione di una transazione implicita mediante l'ambito di transazione ](../../../../docs/framework/data/transactions/implementing-an-implicit-transaction-using-transaction-scope.md)   
 [Elaborazione della transazione ](../../../../docs/framework/data/transactions/index.md)