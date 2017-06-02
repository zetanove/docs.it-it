---
title: "Code e sessioni affidabili | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7e794d03-141c-45ed-b6b1-6c0e104c1464
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Code e sessioni affidabili
Code e sessioni affidabili rappresentano le funzionalità di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per l'implementazione della messaggistica affidabile.Gli argomenti contenuti in questa sezione trattano le funzionalità della messaggistica affidabile di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 La messaggistica affidabile riguarda il modo in cui un'origine di messaggistica affidabile \(definita origine\) trasferisce in modo affidabile i messaggi a una destinazione di messaggistica affidabile \(definita destinazione\).  
  
 Gli aspetti chiave della messaggistica affidabile sono i seguenti:  
  
-   Garanzie di trasferimento dei messaggi inviati da un'origine a una destinazione indipendentemente dagli errori di trasporto o di trasferimento dei messaggi.  
  
-   Separazione dell'origine e della destinazione, che fornisce funzioni di errore e un recupero indipendente dell'origine e della destinazione, nonché un trasferimento e un recapito affidabili dei messaggi, anche se l'origine o la destinazione non è disponibile.  
  
 La messaggistica affidabile comporta spesso il costo di una latenza elevata.Per latenza si intende il tempo che un messaggio impiega per giungere dall'origine alla destinazione.In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vengono pertanto forniti i tipi seguenti di messaggistica affidabile:  
  
-   [Sessioni affidabili](../../../../docs/framework/wcf/feature-details/reliable-sessions.md), che offrono un trasferimento affidabile senza il costo di una latenza elevata.  
  
-   [Code in WCF](../../../../docs/framework/wcf/feature-details/queues-in-wcf.md), che offrono trasferimenti affidabili e separazione tra l'origine e la destinazione.  
  
## Sessioni affidabili  
 Le sessioni affidabili forniscono un trasferimento affidabile end\-to\-end dei messaggi tra un'origine e una destinazione utilizzando il protocollo WS\-ReliableMessaging indipendentemente dal numero o dal tipo di intermediari che separano gli endpoint di messaggistica \(origine e destinazione\).In questo modo vengono inclusi tutti gli intermediari di trasporto che non utilizzano SOAP \(ad esempio proxy HTTP\) o gli intermediari che utilizzano SOAP \(ad esempio bridge o router basati su SOAP\) necessari per il flusso dei messaggi tra gli endpoint.Le sessioni affidabili utilizzano una finestra di trasferimento in memoria per mascherare gli errori a livello di messaggio SOAP e riattivare le connessioni in caso di errori di trasporto.  
  
 Le sessioni affidabili forniscono trasferimenti affidabili dei messaggi con una latenza bassa.Esse forniscono per i messaggi SOAP su qualsiasi proxy o intermediario l'equivalente di ciò che TCP fornisce per i pacchetti su bridge IP.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] sessioni affidabili, vedere [Sessioni affidabili](../../../../docs/framework/wcf/feature-details/reliable-sessions.md).  
  
### Code  
 Le code in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] forniscono il trasferimento affidabile dei messaggi e la separazione tra le origini e le destinazioni al costo di una latenza elevata.La comunicazione in coda di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si basa sull'accodamento messaggi \(noto anche come MSMQ\).  
  
 MSMQ viene fornito con Windows come opzione e viene eseguito come servizio NT.Acquisisce i messaggi da trasmettere in una coda di trasmissione per conto dell'origine e li recapita a una coda di destinazione.La coda di destinazione accetta i messaggi per conto della destinazione a cui verranno recapitati in seguito quando la destinazione richiede i messaggi.I gestori code MSMQ implementano un protocollo di trasferimento messaggi affidabile, in modo che i messaggi non vengano persi durante la trasmissione.Il protocollo può essere nativo o un protocollo basato su SOAP, come SRMP \(SOAP Reliable Messagging Protocol\).  
  
 La separazione, abbinata ai trasferimenti affidabili dei messaggi tra le code, consente alle applicazioni ad accoppiamento debole di comunicare in modo affidabile.A differenza delle sessioni affidabili, non è necessario che l'origine e la destinazione siano in esecuzione contemporaneamente.Questo consente implicitamente scenari in cui le code vengono di fatto utilizzate come un meccanismo di livellamento del carico nei casi in cui non vi è corrispondenza tra il tasso di produzione di messaggi dell'origine e il tasso di utilizzo di messaggi da parte della destinazione.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] code, vedere [Code in WCF](../../../../docs/framework/wcf/feature-details/queues-in-wcf.md).  
  
## Vedere anche  
 [Code in WCF](../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)   
 [Accodamento in WCF](../../../../docs/framework/wcf/feature-details/queuing-in-wcf.md)   
 [Sessioni affidabili](../../../../docs/framework/wcf/feature-details/reliable-sessions.md)   
 [Panoramica delle sessioni affidabili](../../../../docs/framework/wcf/feature-details/reliable-sessions-overview.md)