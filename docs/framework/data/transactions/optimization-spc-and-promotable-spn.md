---
title: "Ottimizzazione mediante commit monofase e notifica monofase promuovibile  | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 57beaf1a-fb4d-441a-ab1d-bc0c14ce7899
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Ottimizzazione mediante commit monofase e notifica monofase promuovibile 
Questo argomento descrive i meccanismi di ottimizzazione delle prestazioni forniti dall'infrastruttura <xref:System.Transactions>.  
  
## PSPE \(Promotable Single Phase Enlistment\)  
 L'infrastruttura <xref:System.Transactions> amministra le transazioni contenute in un solo dominio applicazione che comporta al massimo una sola risorsa durevole o più risorse volatili.Poiché esegue chiamate che riguardano esclusivamente un determinato dominio applicazione, l'infrastruttura <xref:System.Transactions> offre prestazioni migliori e una velocità effettiva più elevata.  
  
 Quando tuttavia la transazione viene passata a un altro oggetto contenuto in un altro dominio applicazione dello stesso computer, in un altro processo o in un altro computer, oppure quando occorre integrare un altro gestore di risorse durevoli, l'infrastruttura <xref:System.Transactions> esegue automaticamente l'escalation della transazione in modo che venga gestita dal gestore MSDTC.Una transazione gestita dal gestore MSDTC presenta un livello di prestazioni inferiore rispetto a una transazione gestita dall'infrastruttura <xref:System.Transactions>.  
  
 Per ottimizzare le prestazioni, l'infrastruttura <xref:System.Transactions> fornisce il meccanismo di integrazione PSPE \(Promotable Single Phase Enlistment\). Tale meccanismo consente a una risorsa durevole remota appartenente a un altro dominio applicazione, processo o computer di partecipare a una transazione dello spazio dei nomi <xref:System.Transactions> senza comportarne l'escalation a una transazione MSDTC.Questo gestore di risorse \(in seguito indicato con la sigla GR\) può ospitare e "possedere" una transazione di cui in seguito può eseguire l'escalation a una transazione distribuita \(o MSDTC\), se necessario.Ciò riduce le probabilità di utilizzo del gestore MSDTC.  
  
 Questo GR specifico in genere dispone di transazioni interne non distribuite e deve essere in grado di supportare una funzionalità che consenta di convertirle in transazioni distribuite in fase di esecuzione.Un esempio di gestore di questo tipo è SQL Server 2005.In questo caso, l'infrastruttura <xref:System.Transactions> assume un ruolo di gestione passivo e si limita a verificare se occorre eseguire l'escalation di una determinata transazione.Per supportare l'interazione tra l'infrastruttura <xref:System.Transactions> e il gestore di risorse, quest'ultimo deve implementare l'interfaccia <xref:System.Transactions.IPromotableSinglePhaseNotification>.  
  
 Il metodo <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> viene utilizzato per integrare una determinata risorsa durevole di cui in seguito è possibile eseguire l'escalation.Questo metodo garantisce che l'escalation dell'integrazione possa essere eseguita ogni volta che sia necessario.Se l'integrazione riesce, il GR crea una transazione interna propria e la associa alla transazione dello spazio dei nomi <xref:System.Transactions>.Se l'integrazione PSPE non riesce, il GR deve invece ricorrere al metodo <xref:System.Transactions.Transaction.EnlistDurable%2A> per eseguire l'integrazione.Gli errori di integrazione PSPE possono verificarsi quando la transazione è già una transazione distribuita oppure quando un altro GR ha già eseguito l'integrazione PSPE.  
  
 Dopo l'integrazione, le richieste ai client di commit o di interruzione della transazione dello spazio dei nomi <xref:System.Transactions> vengono convertite in richieste al GR, rispettivamente tramite la chiamata al metodo <xref:System.Transactions.IPromotableSinglePhaseNotification.SinglePhaseCommit%2A> o al metodo <xref:System.Transactions.IPromotableSinglePhaseNotification.Rollback%2A>.  
  
 Se la transazione dello spazio dei nomi <xref:System.Transactions> non richiede l'escalation in nessun caso, quando viene eseguito il commit della transazione il GR riceve una notifica che richiede di procedere all'utilizzo del metodo <xref:System.Transactions.IPromotableSinglePhaseNotification.SinglePhaseCommit%2A>al fine di eseguire il commit della transazione interna creata inizialmente.  
  
 Se la transazione dello spazio dei nomi <xref:System.Transactions> richiede un'escalation \(ad esempio, per supportare più GR\), lo spazio dei nomi <xref:System.Transactions> informa il gestore di risorse in merito chiamando il metodo <xref:System.Transactions.ITransactionPromoter.Promote%2A> sull'interfaccia <xref:System.Transactions.ITransactionPromoter> da cui deriva l'interfaccia <xref:System.Transactions.IPromotableSinglePhaseNotification>.Il gestore di risorse esegue quindi la conversione interna della transazione da una transazione locale \(che non richiede la registrazione\) a un oggetto di transazione in grado di partecipare a una transazione DTC e quindi la associa alle operazioni già svolte.Quando viene richiesto il commit della transazione, la gestione transazioni invia comunque la notifica di richiesta di utilizzo del metodo <xref:System.Transactions.IPromotableSinglePhaseNotification.SinglePhaseCommit%2A> al gestore di risorse, che quindi esegue il commit della transazione distribuita creata nel corso dell'escalation.  
  
> [!NOTE]
>  Le tracce **TransactionCommitted** \(create quando si richiede il commit della transazione di cui è stata eseguita l'escalation\) contengono l'ID attività della transazione DTC.  
  
 Per ulteriori informazioni sull'escalation della gestione delle transazioni, vedere [Escalation della gestione delle transazioni ](../../../../docs/framework/data/transactions/transaction-management-escalation.md).  
  
## Scenario di escalation della gestione delle transazioni  
 Nello scenario seguente viene mostrata l'escalation di una transazione a transazione distribuita utilizzando lo spazio dei nomi <xref:System.Data> come 'proxy' del gestore di risorse.Questo scenario presuppone che sia già presente una connessione dello spazio dei nomi <xref:System.Data> al database, CN1, coinvolta nella transazione e che l'applicazione desideri coinvolgere un'altra connessione dello spazio dei nomi <xref:System.Data>, CN2.La transazione, in quanto completamente distribuita e con commit a due fasi, deve essere promossa a transazione DTC.  
  
 In questo scenario:  
  
1.  CN1 chiama il metodo <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> per integrarsi nella transazione.Quindi, la transazione è ancora locale e non prevede nessun'altra integrazione promuovibile. La chiamata al metodo <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> ha pertanto esito positivo.  
  
2.  Quando la seconda connessione CN2 chiama il metodo <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A>, la chiamata ha esito negativo poiché la transazione prevede un'altra integrazione promuovibile.Di conseguenza, CN2 deve ottenere una transazione DTC per poterla passare a SQL.A tale scopo, CN2 utilizza uno dei metodi forniti dalla classe <xref:System.Transactions.TransactionInterop> per creare un formato della transazione che possa essere passato SQL.  
  
3.  Lo spazio dei nomi <xref:System.Transactions> chiama il metodo <xref:System.Transactions.ITransactionPromoter.Promote%2A> sull'interfaccia <xref:System.Transactions.ITransactionPromoter> implementata da CN1.  
  
4.  A questo punto, CN1 esegue l'escalation della transazione utilizzando uno dei meccanismi specifici di SQL 2005 e dello spazio dei nomi <xref:System.Data>.  
  
5.  Il valore restituito dal metodo di <xref:System.Transactions.ITransactionPromoter.Promote%2A> è una matrice di byte che contiene un token di propagazione per la transazione.<xref:System.Transactions> utilizza questo token di propagaition per creare una transazione di DTC che può includere nella transazione locale.  
  
6.  A questo punto, CN2 può utilizzare i dati ricevuti dalla chiamata a uno dei metodi forniti dalla classe <xref:System.Transactions.TransactionInterop> per passare la transazione a SQL.  
  
7.  Entrambe le connessioni risultano quindi integrate in una transazione DTC distribuita.  
  
## Ottimizzazione mediante commit monofase  
 Il protocollo di commit monofase è più efficiente in fase di esecuzione, poiché tutti gli aggiornamenti vengono eseguiti senza alcuna coordinazione esplicita.Per sfruttare questa ottimizzazione è necessario implementare un gestore di risorse utilizzando l'interfaccia <xref:System.Transactions.ISinglePhaseNotification> per la risorsa e quindi integrare le risorse in una transazione utilizzando il metodo <xref:System.Transactions.Transaction.EnlistDurable%2A> o il metodo <xref:System.Transactions.Transaction.EnlistVolatile%2A>.In particolare, per garantire l'esecuzione di un commit monofase, il parametro *EnlistmentOptions* deve essere uguale a <xref:System.Transactions.EnlistmentOptions>.  
  
 Poiché l'interfaccia <xref:System.Transactions.ISinglePhaseNotification> deriva dall'interfaccia <xref:System.Transactions.IEnlistmentNotification>, se il GR non supporta il commit monofase può comunque ricevere le notifiche di commit a due fasi.Se la gestione transazioni invia una notifica di chiamata al metodo <xref:System.Transactions.ISinglePhaseNotification.SinglePhaseCommit%2A> al GR, quest'ultimo deve tentare di eseguire il commit della transazione e quindi deve indicare alla gestione transazioni l'esito del tentativo, ovvero se eseguire il commit o il rollback della transazione mediante una chiamata al metodo <xref:System.Transactions.SinglePhaseEnlistment.Committed%2A>, al metodo <xref:System.Transactions.SinglePhaseEnlistment.Aborted%2A> o al metodo <xref:System.Transactions.SinglePhaseEnlistment.InDoubt%2A> sul parametro <xref:System.Transactions.SinglePhaseEnlistment>.In questa fase, la risposta di una chiamata al metodo <xref:System.Transactions.Enlistment.Done%2A> sull'integrazione implica l'utilizzo della semantica ReadOnly.Pertanto, evitare di ricorrere al metodo <xref:System.Transactions.Enlistment.Done%2A> in aggiunta agli altri metodi.  
  
 Se è presente un'integrazione volatile e nessuna integrazione durevole, le integrazioni volatili ricevono una notifica di commit monofase. Se sono presenti più integrazioni volatili e solo un'integrazione durevole, le integrazioni volatili ricevono un commit a due fasi.Al completamento l'elenco durevole riceve un commit monofase.  
  
## Vedere anche  
 [Integrazione di risorse come partecipanti a una transazione ](../../../../docs/framework/data/transactions/enlisting-resources-as-participants-in-a-transaction.md)   
 [Commit di una transazione monofase e multifase ](../../../../docs/framework/data/transactions/committing-a-transaction-in-single-phase-and-multi-phase.md)