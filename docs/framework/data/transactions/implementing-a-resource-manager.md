---
title: "Implementazione di un gestore di risorse  | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d5c153f6-4419-49e3-a5f1-a50ae4c81bf3
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Implementazione di un gestore di risorse 
Ogni risorsa utilizzata in una transazione viene gestita da un gestore di risorse, le cui azioni vengono coordinate da una gestione transazioni.I gestori di risorse collaborano con la gestione transazioni allo scopo di garantire atomicità e isolamento all'applicazione.Alcuni esempi di gestori di risorse sono le code di messaggi durevoli, le tabelle hash in memoria e Microsoft SQL Server.  
  
 Un gestore di risorse gestisce dati durevoli o volatili.La durabilità \(o la volatilità\) di un gestore di risorse ne indica la capacità \(o la non capacità\) di ripristino in caso di errore.I gestori di risorse che supportano il ripristino in caso di errore salvano i dati in modo permanente in un archivio durevole durante la fase 1, ovvero la fase di preparazione. In questo modo, se il gestore di risorse diventa non disponibile, può reintegrarsi nella transazione non appena viene ripristinato e quindi eseguire le azioni appropriate in base alle notifiche ricevute dalla gestione transazioni.In generale, i gestori di risorse volatili gestiscono risorse volatili, come nel caso di una struttura di dati in memoria \(ad esempio, una tabella hash transazionale in memoria\), laddove i gestori di risorse durevoli gestiscono risorse che presentano un archivio di backup permanente, come nel caso di un database con archivio di backup su disco.  
  
 Per poter partecipare a una determinata transazione, una risorsa deve integrarsi in essa.La classe <xref:System.Transactions.Transaction> definisce un set di metodi i cui nomi iniziano con **Enlist** che forniscono questa funzionalità.I diversi metodi **Enlist** corrispondono ai vari tipi di integrazione disponibili in un gestore di risorse.In particolare, i metodi <xref:System.Transactions.Transaction.EnlistVolatile%2A> vengono utilizzati per le risorse volatili, mentre i metodi <xref:System.Transactions.Transaction.EnlistDurable%2A> vengono utilizzati per le risorse durevoli.Per semplicità, dopo aver deciso se utilizzare il metodo <xref:System.Transactions.Transaction.EnlistDurable%2A> o il metodo <xref:System.Transactions.Transaction.EnlistVolatile%2A> a seconda del supporto di durabilità della risorsa utilizzata, è necessario integrare la risorsa nel protocollo 2PC \(2\-Phase Commit, commit a due fasi\) implementando nel gestore di risorse l'interfaccia <xref:System.Transactions.IEnlistmentNotification>.Per ulteriori informazioni sul protocollo 2PC, vedere [Commit di una transazione monofase e multifase ](../../../../docs/framework/data/transactions/committing-a-transaction-in-single-phase-and-multi-phase.md).  
  
 L'integrazione in una determinata transazione garantisce al gestore di risorse di ricevere callback dalla gestione transazioni quando la transazione viene interrotta o quando ne viene eseguito il commit.Per ogni integrazione esiste un'istanza specifica della classe <xref:System.Transactions.IEnlistmentNotification>.In genere esiste un'unica integrazione per ogni transazione. È tuttavia possibile che un gestore di risorse scelga di integrarsi più volte nella stessa transazione.  
  
 Dopo l'integrazione, il gestore di risorse risponde alle richieste della transazione.Un gestore di risorse durevole memorizza una quantità di informazioni sufficiente ad annullare o a ripetere le operazioni della transazione sulle risorse che gestisce.Esistono vari metodi per implementare questa funzionalità. Due tecniche comuni sono la memorizzazione di più versioni dei dati o la gestione di un registro delle modifiche.  
  
 Quando l'applicazione esegue il commit della transazione, la gestione transazioni avvia il protocollo di commit a due fasi.Nella prima fase, la gestione transazioni verifica se ogni gestore di risorse integrato ha eseguito la procedura di preparazione di commit della transazione,ovvero se è pronto a interrompere la transazione oppure a eseguirne il commit.  
  
 Durante questa prima fase di preparazione, il gestore di risorse durevole registra i dati vecchi e nuovi in un archivio permanente. Ciò garantisce la possibilità di recuperare i dati anche in caso di errore di sistema.Se il gestore di risorse è in grado di completare la procedura di preparazione, comunica alla gestione transazioni il proprio voto a favore del commit o dell'interruzione della transazione.Se uno dei gestori di risorse segnala un errore durante la fase di preparazione, la gestione transazioni invia un comando di rollback a ogni gestore di risorse e informa l'applicazione in merito all'esito negativo del commit.  
  
 Dopo la preparazione, un gestore di risorse deve attendere per ottenere un commit o un callback di interruzione dalla gestione transazioni nella fase 2.Il completamento della preparazione e il protocollo di commit generalmente richiedono una frazione di secondo.Tuttavia, se si verificano errori di sistema o di comunicazione, la notifica di commit o di interruzione può richiedere minuti o persino ore.Durante questo periodo, il gestore di risorse è incerto sul risultato della transazionee non è in grado di stabilire se procedere al commit o all'interruzione della transazione.Per proteggere i dati modificati e impedirne la modifica da parte di altre transazioni, il gestore di risorse blocca la transazione finché non riceve una notifica definitiva.  
  
 Quando si verifica un errore in un gestore di risorse, tutte le transazioni a cui quest'ultimo è integrato vengono interrotte, ad eccezione di quelle per cui la procedura di preparazione o di commit è stata eseguita prima dell'errore.Quando viene riavviato, un gestore di risorse durevole ricostruisce lo stato di commit delle risorse gestite. A tale scopo, recupera le informazioni di preparazione scritte nella fase 1 e quindi procede di conseguenza al commit o all'interruzione delle transazioni precedentemente interrotte.  
  
 In breve, il protocollo di commit a due fasi e i gestori di risorse collaborano per garantire l'atomicità e la durevolezza delle transazioni.  
  
 La classe <xref:System.Transactions.Transaction> fornisce inoltre il metodo <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> per eseguire l'integrazione PSPE \(Promotable Single Phase Enlistment\).Grazie a questo meccanismo, un gestore di risorse durevoli può ospitare e "possedere" una transazione di cui in seguito può eseguire l'escalation in modo che venga gestita dal gestore MSDTC, se necessario.Per ulteriori informazioni in merito, vedere [Ottimizzazione mediante commit monofase e notifica monofase promuovibile ](../../../../docs/framework/data/transactions/optimization-spc-and-promotable-spn.md).  
  
## In questa sezione  
 I passaggi che in genere vengono eseguiti dai gestori di risorse sono descritti negli argomenti seguenti.  
  
 [Integrazione di risorse come partecipanti a una transazione ](../../../../docs/framework/data/transactions/enlisting-resources-as-participants-in-a-transaction.md)  
  
 Descrive come una risorsa durevole o volatile può integrarsi in una transazione.  
  
 [Commit di una transazione monofase e multifase ](../../../../docs/framework/data/transactions/committing-a-transaction-in-single-phase-and-multi-phase.md)  
  
 Descrive come un gestore di risorse risponde a una notifica di commit ed esegue la procedura di preparazione.  
  
 [Esecuzione del ripristino ](../../../../docs/framework/data/transactions/performing-recovery.md)  
  
 Descrive la procedura di ripristino eseguita da un gestore di risorse in caso di errore.  
  
 [Livelli di attendibilità di sicurezza nell'accesso alle risorse ](../../../../docs/framework/data/transactions/security-trust-levels-in-accessing-resources.md)  
  
 Descrive come i tre livelli di attendibilità di System.Transactions limitano l'accesso ai tipi di risorse esposte dallo spazio dei nomi <xref:System.Transactions>.  
  
 [Ottimizzazione mediante commit monofase e notifica monofase promuovibile ](../../../../docs/framework/data/transactions/optimization-spc-and-promotable-spn.md)  
  
 Descrive alcune metodologie di ottimizzazione delle implementazioni dei gestori di risorse.