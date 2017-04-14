---
title: "Utilizzo di contratti nel flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 939c64e9-e7cc-4abc-b41e-27cfce1d7e50
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Utilizzo di contratti nel flusso di lavoro
In caso di implementazione di un servizio, viene definito un numero di contratti che descrivono il servizio e i dati inviati e ricevuti.I dati vengono rappresentati come contratti dati e contratti di messaggio; sia [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sia i servizi flusso di lavoro utilizzano definizioni del contratto dati e del contratto messaggio nell'ambito delle descrizioni del servizio.Il servizio stesso espone metadati \(nel formato WSDL\) per descrivere le operazioni del servizio.In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] i contratti di servizio e contratti di operazione definiscono il servizio e le operazioni supportate.Tuttavia, in un servizio flusso di lavoro, questi contratti costituiscono parte del processo aziendale stesso e vengono esposti nei metadati da un processo denominato inferenza del contratto.  
  
## Inferenza del contratto  
 Se un servizio flusso di lavoro viene ospitato mediante <xref:System.ServiceModel.Activities.WorkflowServiceHost>, viene esaminata la definizione del flusso di lavoro e viene generato un contratto in base al set delle attività di messaggistica rilevato nel flusso di lavoro.In particolare vengono utilizzate le attività e le proprietà indicate di seguito per generare il contratto:  
  
 Attività <xref:System.ServiceModel.Activities.Receive>  
  
-   <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A>  
  
-   <xref:System.ServiceModel.Activities.Receive.OperationContractName%2A>  
  
-   <xref:System.ServiceModel.Activities.Receive.Action%2A>  
  
-   <xref:System.ServiceModel.Activities.Receive.ValueType%2A>  
  
 Attività <xref:System.ServiceModel.Activities.SendReply>  
  
-   <xref:System.ServiceModel.Activities.SendReply.Action%2A>  
  
-   <xref:System.ServiceModel.Activities.SendReply.ValueType%2A>  
  
 Attività <xref:System.ServiceModel.Activities.TransactedReceiveScope>  
  
 Il risultato finale di inferenza del contratto rappresenta una descrizione del servizio utilizzando le stesse strutture dei dati del servizio WCF e dei contratti dell'operazione.Queste informazioni vengono quindi utilizzate per esporre WSDL per il servizio flusso di lavoro.  
  
## Vedere anche  
 [Servizi flusso di lavoro](../../../../docs/framework/wcf/feature-details/workflow-services.md)   
 [Attività di messaggistica](../../../../docs/framework/wcf/feature-details/messaging-activities.md)   
 [Procedura: creare un servizio flusso di lavoro con attività di messaggistica](../../../../docs/framework/wcf/feature-details/how-to-create-a-workflow-service-with-messaging-activities.md)   
 [Procedura: creare un servizio di flusso di lavoro che utilizza un contratto di servizio esistente](../../../../docs/framework/windows-workflow-foundation//how-to-create-a-workflow-service-that-consumes-an-existing-service-contract.md)