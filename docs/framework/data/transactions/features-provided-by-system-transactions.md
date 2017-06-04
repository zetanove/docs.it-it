---
title: "Funzionalit&#224; Fornite da System.Transactions  | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e458cef9-63b5-4401-b448-1536dcd9d9e5
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Funzionalit&#224; Fornite da System.Transactions 
Questa sezione descrive come utilizzare le funzionalità fornite dallo spazio dei nomi <xref:System.Transactions> per scrivere applicazioni transazionali e gestori di risorse personalizzati.In particolare, questa sezione descrive come creare una transazione \(locale o distribuita\) e come integrarvi una o più risorse.  
  
## Panoramica su System.Transactions  
 Grazie al supporto delle transazioni create in SQL Server, ADO.NET, MSMQ e Microsoft Distributed Transaction Coordinator \(MSDTC\), l'infrastruttura fornita dalle classi dello spazio dei nomi <xref:System.Transactions> rende la programmazione transazionale semplice ed efficiente.Lo spazio dei nomi <xref:System.Transactions> fornisce sia un modello di programmazione esplicito basato sulla classe <xref:System.Transactions.Transaction> sia un modello di programmazione implicito che utilizza la classe <xref:System.Transactions.TransactionScope>, in cui le transazioni vengono gestite automaticamente dall'infrastruttura.Per ulteriori informazioni su come creare un'applicazione transazionale utilizzando questi due modelli, vedere [Scrittura di un'applicazione transazionale ](../../../../docs/framework/data/transactions/writing-a-transactional-application.md).  
  
 Lo spazio dei nomi <xref:System.Transactions> fornisce inoltre i tipi per implementare un gestore di risorse,ovvero un'applicazione che gestisce i dati permanenti o volatili utilizzati in una transazione e che collabora con la gestione transazioni per garantire atomicità e isolamento all'applicazione che utilizza tale transazione.La gestione transazioni fornita dall'infrastruttura <xref:System.Transactions> supporta le transazioni che coinvolgono più risorse volatili o una sola risorsa durevole.Per ulteriori informazioni sull'implementazione di un gestore di risorse, vedere [Implementazione di un gestore di risorse ](../../../../docs/framework/data/transactions/implementing-a-resource-manager.md).  
  
 Inoltre, quando un gestore di risorse durevole aggiuntivo si integra in una transazione, la gestione transazioni collabora con una gestione transazioni basata su disco quale DTC allo scopo di eseguire in modo trasparente l'escalation delle transazioni da locali a distribuite.Di base l'infrastruttura <xref:System.Transactions> utilizza due meccanismi per ottimizzare le prestazioni:  
  
-   Escalation dinamica, che garantisce che l'infrastruttura <xref:System.Transactions> ricorra al gestore MSDTC solo quando una transazione coinvolge più risorse distribuite.Per ulteriori informazioni sull'escalation dinamica.Vedere l'argomento [Escalation della gestione delle transazioni ](../../../../docs/framework/data/transactions/transaction-management-escalation.md).  
  
-   PSPE, che consente a una risorsa, ad esempio un database, di assumere la proprietà della transazione se è l'unica entità a parteciparvi.In seguito, se necessario, l'infrastruttura <xref:System.Transactions> può comunque eseguire l'escalation della gestione della transazione a MSDTC.Ciò consente di ridurre ulteriormente le probabilità di utilizzo del gestore MSDTC.Il meccanismo PSPE è descritto nell'argomento [Ottimizzazione mediante commit monofase e notifica monofase promuovibile ](../../../../docs/framework/data/transactions/optimization-spc-and-promotable-spn.md).  
  
 Lo spazio dei nomi <xref:System.Transactions> definisce tre livelli di attendibilità per restringere l'accesso ai tipi di risorse che espone: AllowPartiallyTrustedCallers, DistributedTransactionPermission e FullTrust.Per ulteriori informazioni sui vari livelli di attendibilità, vedere [Livelli di attendibilità di sicurezza nell'accesso alle risorse ](../../../../docs/framework/data/transactions/security-trust-levels-in-accessing-resources.md).  
  
## Argomenti della sezione  
  
### Scrittura di un'applicazione transazionale  
 Lo spazio dei nomi <xref:System.Transactions> offre due modelli per creare le applicazioni di transazione.Nell'argomento [Implementazione di una transazione implicita mediante l'ambito di transazione ](../../../../docs/framework/data/transactions/implementing-an-implicit-transaction-using-transaction-scope.md) viene invece descritto come utilizzare la classe <xref:System.Transactions.TransactionScope> dello spazio dei nomi <xref:System.Transactions> per creare transazioni implicite.  
  
 L'argomento [Implementazione di una transazione esplicita mediante CommittableTransaction ](../../../../docs/framework/data/transactions/implementing-an-explicit-transaction-using-committabletransaction.md) descrive invece come utilizzare la classe <xref:System.Transactions.CommittableTransaction> dello spazio dei nomi <xref:System.Transactions> per creare transazioni esplicite.  
  
 Per ulteriori informazioni sulla scrittura di un'applicazione transazionale, vedere [Scrittura di un'applicazione transazionale ](../../../../docs/framework/data/transactions/writing-a-transactional-application.md).  
  
### Implementazione di un gestore di risorse  
 Per implementare un gestore di risorse in grado di partecipare a una transazione, vedere [Implementazione di un gestore di risorse ](../../../../docs/framework/data/transactions/implementing-a-resource-manager.md).Questa sezione descrive l'integrazione di una risorsa, il commit di una transazione, il ripristino in caso di errore e i metodi di ottimizzazione.