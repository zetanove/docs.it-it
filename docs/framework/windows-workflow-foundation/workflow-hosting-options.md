---
title: "Opzioni di hosting di flussi di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 37bcd668-9c5c-4e7c-81da-a1f1b3a16514
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Opzioni di hosting di flussi di lavoro
Nella maggior parte degli esempi di [!INCLUDE[wf](../../../includes/wf-md.md)] vengono utilizzati flussi di lavoro ospitati in un'applicazione console, ma non si tratta di uno scenario realistico per i flussi di lavoro generalmente utilizzati.I flussi di lavoro nelle applicazioni aziendali reali saranno ospitati in processi persistenti, ad esempio un servizio Windows creato dallo sviluppatore o un'applicazione server come [!INCLUDE[iisver](../../../includes/iisver-md.md)] o AppFabric.Di seguito sono riportate le differenze tra questi approcci.  
  
## Hosting di flussi di lavoro in IIS con Windows AppFabric  
 IIS con AppFabric è l'host preferito per i flussi di lavoro.L'applicazione host per i flussi di lavoro che utilizzano AppFabric è Windows Activation Service che rimuove la dipendenza di HTTP su IIS indipendente.  
  
## Hosting di flussi di lavoro in IIS indipendente  
 L'utilizzo di [!INCLUDE[iisver](../../../includes/iisver-md.md)] indipendente non è consigliato perché con AppFabric sono disponibili strumenti di gestione e monitoraggio che facilitano la manutenzione delle applicazioni in esecuzione.I flussi di lavoro devono essere ospitati in [!INCLUDE[iisver](../../../includes/iisver-md.md)] indipendente solo in caso di problemi di infrastruttura per il passaggio ad AppFabric.  
  
> [!WARNING]
>  [!INCLUDE[iisver](../../../includes/iisver-md.md)] ricicla periodicamente i pool di applicazioni per diversi motivi.Quando un pool di applicazioni viene riciclato, IIS smette di accettare i messaggi del pool precedente e crea un'istanza di un nuovo pool di applicazioni per accettare le nuove richieste.Se il flusso di lavoro continua dopo l'invio di una risposta, [!INCLUDE[iisver](../../../includes/iisver-md.md)] non verrà informato del lavoro eseguito e può riciclare il pool di applicazioni host.In questo caso, il flusso di lavoro verrà interrotto e i servizi di rilevamento registreranno un messaggio [1004 \- WorkflowInstanceAborted](../../../docs/framework/windows-workflow-foundation//1004-workflowinstanceaborted.md) con il campo relativo al motivo vuoto.  
>   
>  Se si utilizza la persistenza, l'host deve esplicitamente riavviare le istanze arrestate dall'ultimo punto di persistenza.  
>   
>  Se si utilizza AppFabric, il servizio di gestione del flusso di lavoro eventualmente riprenderà il flusso di lavoro dall'ultimo il punto di persistenza riuscito se si utilizza la persistenza.Se la persistenza non viene utilizzata e il flusso di lavoro esegue operazioni all'esterno di un modello di risposta\-richiesta, i dati verranno persi quando il flusso di lavoro viene interrotto.  
  
## Hosting di un flusso di lavoro in un servizio Windows personalizzato  
 La creazione di un servizio personalizzato di flusso di lavoro per ospitare il flusso di lavoro richiede allo sviluppatore di duplicare molte funzionalità fornite in modo predefinito da AppFabric, ma consente maggiore flessibilità con le funzionalità personalizzate.Da tenere in considerazione solo se AppFabric dimostra di non essere un'opzione.