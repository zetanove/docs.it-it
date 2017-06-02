---
title: "Verifica Get e Put condizionale | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3d22067f-57b8-4e0f-a571-a694512187ae
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Verifica Get e Put condizionale
In questo esempio viene descritto come utilizzare le nuove API di aggiornamento e recupero condizionali per il modello di programmazione WCF REST.Poiché aggiornamento e recupero condizionali risultano più appropriati per servizi REST e orientati alle risorse, il presente esempio amplia l'esempio [Servizio risorse di base](../../../../docs/framework/wcf/samples/basic-resource-service.md).Questo esempio si concentra sull'aggiunta di supporto per aggiornamento e recupero condizionali all'esempio [Servizio risorse di base](../../../../docs/framework/wcf/samples/basic-resource-service.md) utilizzando le nuove API introdotte in [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)].  
  
## Dimostrazione  
 Aggiornamento e recupero condizionali  
  
## Discussione  
 In questo esempio, il servizio WCF presenta una raccolta di clienti in modo REST e orientato alle risorse.Per una descrizione dettagliata dell'implementazione del servizio, vedere l'esempio [Servizio risorse di base](../../../../docs/framework/wcf/samples/basic-resource-service.md).  
  
 Questo esempio aggiunge funzionalità di aggiornamento e recupero condizionali all'esempio [Servizio risorse di base](../../../../docs/framework/wcf/samples/basic-resource-service.md).Aggiornamento e recupero condizionali utilizzano tag di entità HTTP e le intestazioni HTTP If\-None\-Match e If\-Match per convalidare il fatto che i client dispongano o meno dell'entità più aggiornata per una determinata risorsa.Tuttavia, l'attività di implementazione di codice per analizzare correttamente le intestazioni HTTP If\-None\-Match e If\-Match può essere monotona e soggetta ad errori.Pertanto, i metodi <xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalRetrieve%2A> e <xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalUpdate%2A> sono stati aggiunti a <xref:System.ServiceModel.Web.IncomingWebRequestContext>, a cui è possibile accedere utilizzando l'istanza corrente di <xref:System.ServiceModel.Web.WebOperationContext>.Inoltre, il metodo `SetETag` è stato aggiunto a <xref:System.ServiceModel.Web.OutgoingWebRequestContext>, semplificando la restituzione di tag di entità validi.  
  
 Il metodo <xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalRetrieve%2A> deve essere utilizzato con operazioni \[WebGet\].Il tag di entità corrente per la risorsa specificata viene considerato come parametro `entityTag`, che può essere di tipo `string`, `int`, `long` o `Guid`.Il metodo <xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalRetrieve%2A> verifica il tag di entità nell'intestazione HTTP If\-None\-Match della richiesta.Se il tag di entità è presente nell'intestazione HTTP If\-None\-Match, viene generata un'eccezione <xref:System.ServiceModel.Web.WebFaultException> con il codice di stato Non modificato \(304\); in caso contrario, il metodo termina.Il meccanismo di recupero condizionale consente al client di indicare al server che dispone di tale entità e di inviare l'entità corrente solo se il client ne è sprovvisto.È possibile visualizzare l'utilizzo di esempio del metodo <xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalRetrieve%2A> nelle operazioni `GetCustomer` e `GetCustomers` del servizio.È importante notare che le chiamate a <xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalRetrieve%2A> potrebbero non restituire alcun risultato.Gli sviluppatori devono implementare l'operazione in modo tale che sia possibile determinare l'esito positivo della richiesta prima che venga eseguita la chiamata a <xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalRetrieve%2A>. In mancanza della chiamata a <xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalRetrieve%2A>, il servizio invierebbe in questo modo una risposta con un codice di stato che indica un esito positivo.  
  
 Il metodo <xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalUpdate%2A> è analogo al metodo <xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalRetrieve%2A>.Il tag di entità corrente viene utilizzato anche per la risorsa specificata.Tuttavia, deve essere utilizzato con operazioni \[WebInvoke\] in cui il metodo viene impostato su "PUT" o "DELETE".Il metodo <xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalUpdate%2A> verifica il tag di entità nell'intestazione HTTP If\-Match della richiesta.Se il tag di entità non è presente nell'intestazione HTTP If\-Match, viene generata un'eccezione <xref:System.ServiceModel.Web.WebFaultException> con il codice di stato Precondizione non riuscita \(412\).Il meccanismo di aggiornamento condizionale consente al client di indicare al server che dispone di tale entità per la risorsa. Consente inoltre solo al client di modificare la risorsa, se l'entità di cui dispone è corrente.È possibile visualizzare l'utilizzo di esempio del metodo <xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalUpdate%2A> nelle operazioni `UpdateCustomer` e `DeleteCustomer` del servizio.In modo analogo a quanto avviene con <xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalRetrieve%2A>, è importante notare che le chiamate a <xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalUpdate%2A> potrebbero non restituire alcun risultato.Gli sviluppatori devono implementare l'operazione in modo tale che sia possibile determinare l'esito positivo della richiesta prima che venga eseguita la chiamata a <xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalUpdate%2A>. In mancanza della chiamata a <xref:System.ServiceModel.Web.IncomingWebRequestContext.CheckConditionalUpdate%2A>, il servizio invierebbe in questo modo una risposta con un codice di stato che indica un'esito positivo.  
  
 L'esempio è costituito da un servizio indipendente e da un client in esecuzione in un'applicazione console.Quando l'applicazione console è in esecuzione, il client invia richieste al servizio e scrive nella finestra della console le informazioni pertinenti incluse nelle risposte.  
  
#### Per eseguire l'esempio  
  
1.  Aprire la soluzione per l'esempio relativo alla verifica Get e Put condizionale.Per garantire l'esecuzione corretta dell'esempio, è necessario avviare [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] come amministratore.A tale scopo, fare clic con il pulsante destro del mouse sull'icona [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] e scegliere **Esegui come amministratore** dal menu di scelta rapida.  
  
2.  Premere CTRL\+MAIUSC\+B per compilare la soluzione, quindi premere CTRL\+F5 per eseguire il progetto di applicazione console.Se nell'esecuzione del progetto il debug è abilitato \(premendo F5 anziché CTRL\+F5\), il debugger si arresta quando viene generata un'eccezione dalla verifica GET e PUT condizionale.Quando ciò si verifica, premere F5 per continuare l'esecuzione dell'esempio.  
  
3.  Viene visualizzata la finestra della console, che fornisce l'URI del servizio in esecuzione e l'URI della pagina della Guida HTML per il servizio in esecuzione.  
  
4.  Quando l'esempio è in esecuzione, il client invia richieste al servizio e scrive le risposte nella finestra della console.  
  
5.  Premere un tasto qualsiasi per chiudere l'esempio.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Web\ConditionalGetAndPut`