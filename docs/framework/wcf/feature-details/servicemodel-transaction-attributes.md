---
title: "Attributi della transazione di ServiceModel | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "transazioni [WCF], Attributi ServiceModel"
ms.assetid: 1e0d2436-6ae5-439b-9765-a448d6f60000
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Attributi della transazione di ServiceModel
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] fornisce proprietà su tre attributi <xref:System.ServiceModel> standard che consentono di configurare il comportamento delle transazioni per un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
-   <xref:System.ServiceModel.TransactionFlowAttribute>  
  
-   <xref:System.ServiceModel.ServiceBehaviorAttribute>  
  
-   <xref:System.ServiceModel.OperationBehaviorAttribute>  
  
## TransactionFlowAttribute  
 L'attributo <xref:System.ServiceModel.TransactionFlowAttribute> specifica la disponibilità di un'operazione in un contratto di servizio ad accettare transazioni in ingresso da un client.L'attributo fornisce questo controllo con la proprietà seguente: le transazioni utilizzano l'enumerazione <xref:System.ServiceModel.TransactionFlowOption> per specificare se una transazione in ingresso è <xref:System.ServiceModel.TransactionFlowOption>, <xref:System.ServiceModel.TransactionFlowOption> o <xref:System.ServiceModel.TransactionFlowOption>.  
  
 Questo è l'unico attributo che correla le operazioni di assistenza alle interazioni esterne con un client.Gli attributi descritti nelle sezioni seguenti si riferiscono all'utilizzo di transazioni all'interno dell'esecuzione dell'operazione.  
  
## ServiceBehaviorAttribute  
 L'attributo <xref:System.ServiceModel.ServiceBehaviorAttribute> specifica il comportamento di esecuzione interno di un'implementazione del contratto di servizio.Le proprietà specifiche della transazione di questo attributo includono:  
  
-   <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionAutoCompleteOnSessionClose%2A> specifica se completare una transazione incompiuta alla chiusura della sessione.Il valore predefinito di questa proprietà è `false`.Se questa proprietà è `true` e la sessione in ingresso è stata chiusa correttamente e non per problemi di rete o errori client, tutte le transazioni incompiute vengono completate correttamente.In caso contrario, se questa proprietà è `false` o se la sessione non è stata chiusa normalmente, alla chiusura della sessione viene eseguito il rollback di tutte le transazioni incompiute.Se questa proprietà è `true`, il canale in ingresso deve essere basato sulla sessione.  
  
-   <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A> specifica se l'istanza del servizio sottostante viene rilasciata al completamento di una transazione.Il valore predefinito di questa proprietà è `true`.Il messaggio in ingresso successivo provoca la creazione di una nuova istanza sottostante, ignorando qualsiasi stato per transazione dell'istanza precedente.Il rilascio di un'istanza del servizio è un'azione interna eseguita dal servizio e non ha alcun impatto su nessuna connessione o sessione esistente che i client potrebbero aver stabilito.Questa funzionalità equivale a quella di attivazione JIT fornita da COM\+.Se la proprietà è `true`, <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> deve essere uguale a <xref:System.ServiceModel.ConcurrencyMode>.In caso contrario, il servizio genera un'eccezione di convalida di configurazione non valida durante l'avvio.  
  
-   <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A> specifica il livello di isolamento da utilizzare per le transazioni all'interno del servizio. Questa proprietà prende uno dei valori <xref:System.Transactions.IsolationLevel>.Se la proprietà del livello di isolamento locale è diversa da <xref:System.Transactions.IsolationLevel>, il livello di isolamento di una transazione in ingresso deve corrispondere all'impostazione di questa proprietà locale.In caso contrario, la transazione in ingresso viene rifiutata e al client viene restituito un errore.Se <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> è `true` e non viene propagata nessuna transazione, questa proprietà determina il valore <xref:System.Transactions.IsolationLevel> da utilizzare per la transazione creata localmente.Se <xref:System.Transactions.IsolationLevel> è impostato su <xref:System.Transactions.IsolationLevel>, viene utilizzato <xref:System.Transactions.IsolationLevel><xref:System.Transactions.IsolationLevel>.  
  
-   <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A> specifica il periodo di tempo entro il quale deve essere completata una nuova transazione creata nel servizio.Allo scadere di questo periodo di tempo, se la transazione non è stata completata, si interromperà.Il <xref:System.TimeSpan> viene utilizzato come timeout di <xref:System.Transactions.TransactionScope> per qualsiasi operazione il cui <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> sia impostato su `true` e per la quale sia stata creata una nuova transazione.Il timeout è la durata consentita massima dalla creazione della transazione al completamento della fase 1 nel protocollo di commit a due fasi.Il valore di timeout utilizzato è sempre il valore inferiore tra la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A> e l'impostazione della configurazione di `transactionTimeout`.  
  
## OperationBehaviorAttribute  
 L'attributo <xref:System.ServiceModel.OperationBehaviorAttribute> specifica i comportamenti dei metodi nell'implementazione del servizio.È possibile utilizzarlo per indicare il comportamento di esecuzione specifico dell'operazione.Le proprietà di questo attributo non influiscono sulla descrizione Web Service Description Language \(WSDL\) del contratto di servizio e sono esclusivamente elementi del modello di programmazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che attivano le funzionalità comuni che altrimenti dovrebbero essere implementate dagli sviluppatori.  
  
 Questo attributo ha le seguenti proprietà specifiche per la transazione:  
  
-   <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> specifica se un metodo deve essere eseguito entro l'ambito di una transazione attiva.Il valore predefinito è `false`.Se per un metodo non è impostato l'attributo <xref:System.ServiceModel.OperationBehaviorAttribute>, il metodo non verrà eseguito in una transazione.Se per un'operazione non è richiesto un ambito della transazione, nessuna transazione presente nell'intestazione del messaggio viene attivata e rimane come elemento di <xref:System.ServiceModel.OperationContext.IncomingMessageProperties%2A> di <xref:System.ServiceModel.OperationContext>.Se per un'operazione è richiesto un ambito della transazione, l'origine per la transazione viene derivata da uno degli elementi seguenti:  
  
    -   Se una transazione viene propagata dal client, il metodo viene eseguito nell'ambito di una transazione creato utilizzando quella transazione distribuita.  
  
    -   Con un trasporto in coda, viene utilizzata la transazione utilizzata per annullare l'accodamento del messaggio.Si noti che la transazione utilizzata non è una transazione propagata, in quanto non è stata fornita dal mittente originale del messaggio.  
  
    -   Un trasporto personalizzato può fornire una transazione tramite l'utilizzo di `TransportTransactionProperty`.  
  
    -   Se in nessuno dei casi precedenti viene fornita un'origine esterna per una transazione, subito prima di chiamare il metodo viene creata una nuova istanza <xref:System.Transactions.Transaction>.  
  
-   <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> specifica se la transazione in cui viene eseguito il metodo viene completata automaticamente nel caso in cui non venga generata alcuna eccezione non gestita.Se questa proprietà è `true`, l'infrastruttura chiamante contrassegna automaticamente la transazione come "completata" se il metodo dell'utente viene restituito senza generare un'eccezione.Se questa proprietà è `false`, la transazione viene allegata all'istanza e viene contrassegnata come "completata" solo se il client chiama un metodo successivo contrassegnato con questa proprietà uguale con `true` o se un metodo successivo chiama in modo esplicito <xref:System.ServiceModel.OperationContext.SetTransactionComplete%2A>.Se non si verifica nessuno dei casi precedenti, la transazione non verrà mai "completata" e non verrà eseguito il commit del lavoro, a meno che la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionAutoCompleteOnSessionClose%2A> non sia impostata su `true`.Se questa proprietà è impostata su `true`, è necessario utilizzare un canale con una sessione e <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> deve essere impostato su <xref:System.ServiceModel.InstanceContextMode>.