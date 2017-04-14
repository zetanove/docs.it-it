---
title: "Scrittura di un&#39;applicazione transazionale  | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a4d891f2-6fc8-4395-93c6-6819492406e0
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Scrittura di un&#39;applicazione transazionale 
I programmatori di applicazioni transazionali possono utilizzare i due modelli di programmazione forniti dallo spazio dei nomi <xref:System.Transactions> per creare una transazione.È possibile utilizzare il modello di programmazione esplicita tramite la classe <xref:System.Transactions.Transaction> oppure il modello di programmazione implicita, in cui le transazioni vengono gestite automaticamente dall'infrastruttura mediante la classe <xref:System.Transactions.TransactionScope>.Per le attività di sviluppo è consigliabile utilizzare il modello transazionale implicito.Nell'argomento [Implementazione di una transazione implicita mediante l'ambito di transazione ](../../../../docs/framework/data/transactions/implementing-an-implicit-transaction-using-transaction-scope.md) sono disponibili ulteriori informazioni sull'utilizzo degli ambiti di transazione.  
  
 Entrambi i modelli supportano il commit delle transazioni quando il programma raggiunge uno stato coerente.Se il commit riesce, il sistema esegue il commit permanente della transazione.Se il commit non riesce, la transazione viene interrotta.Se risulta impossibile completare correttamente una transazione, il programma dell'applicazione tenta di interromperla e quindi di annullarne gli effetti.  
  
## Argomenti della sezione  
  
### Creazione di una transazione  
 Lo spazio dei nomi <xref:System.Transactions> offre due modelli per creare una transazione.Questi modelli vengono descritti negli argomenti seguenti.  
  
 [Implementazione di una transazione implicita mediante l'ambito di transazione ](../../../../docs/framework/data/transactions/implementing-an-implicit-transaction-using-transaction-scope.md)  
  
 Descrive il modo in cui lo spazio dei nomi <xref:System.Transactions> supporta la creazione di transazioni implicite mediante la classe <xref:System.Transactions.TransactionScope>.  
  
 [Implementazione di una transazione esplicita mediante CommittableTransaction ](../../../../docs/framework/data/transactions/implementing-an-explicit-transaction-using-committabletransaction.md)  
  
 Descrive il modo in cui lo spazio dei nomi <xref:System.Transactions> supporta la creazione di transazioni esplicite mediante la classe <xref:System.Transactions.CommittableTransaction>.  
  
### Gestione dell'escalation delle transazioni  
 Quando una transazione deve accedere a una risorsa contenuta in un altro dominio applicazione oppure quando si desidera integrare le risorse in un altro gestore di risorse durevoli, il sistema esegue automaticamente l'escalation di tale transazione in modo che venga gestita dal gestore MSDTC.L'escalation delle transazioni viene descritta nell'argomento [Escalation della gestione delle transazioni ](../../../../docs/framework/data/transactions/transaction-management-escalation.md).  
  
### Concorrenza  
 Nell'argomento [Gestione della concorrenza con DependentTransaction ](../../../../docs/framework/data/transactions/managing-concurrency-with-dependenttransaction.md) viene descritto come è possibile ottenere la concorrenza fra attività asincrone tramite la classe <xref:System.Transactions.DependentTransaction> class.  
  
### Interoperabilità COM\+  
 L'argomento [Interoperabilità con transazioni COM\+ ed Enterprise Services ](../../../../docs/framework/data/transactions/interoperability-with-enterprise-services-and-com-transactions.md) illustra come è possibile definire un'interazione fra le transazioni distribuite e le transazioni COM\+.  
  
### Diagnostica  
 L'argomento [Tracce di diagnostica ](../../../../docs/framework/data/transactions/diagnostic-traces.md) descrive come è possibile utilizzare i codici di traccia generati dall'infrastruttura <xref:System.Transactions> per risolvere i problemi che si verificano nelle applicazioni utilizzate.  
  
### Utilizzo delle funzionalità all'interno di ASP.NET  
 L'argomento [Uso di System.Transactions in ASP.NET](../../../../docs/framework/data/transactions/using-system-transactions-in-aspnet.md) descrive il modo in cui è possibile utilizzare correttamente lo spazio dei nomi <xref:System.Transactions> all'interno di un'applicazione ASP.NET.