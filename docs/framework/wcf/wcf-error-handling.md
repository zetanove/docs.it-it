---
title: "Gestione errori WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1e4b1e0f-9598-449d-9d73-90bda62305b8
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Gestione errori WCF
Gli errori rilevati da un'applicazione WCF appartengono a uno dei seguenti tre gruppi:  
  
1.  errori di comunicazione  
  
2.  errori di proxy\/canale  
  
3.  errori di applicazione  
  
 Gli errori di comunicazione si verificano quando una rete non è disponibile, un client utilizza un indirizzo errato o l'host del servizio non è in ascolto dei messaggi in arrivo.Errori di questo tipo vengono restituiti al client come <xref:System.ServiceModel.CommunicationException> o <xref:System.ServiceModel.CommunicationException> \(classi derivate\).  
  
 Gli errori di proxy\/canale si verificano all'interno del canale o nel proxy stesso.Gli errori di questo tipo includono il tentativo di utilizzare un proxy o un canale chiuso, un contratto non corrispondente tra il client e il servizio o il rifiuto delle credenziali del client da parte del servizio.In questa categoria sono presenti molti tipi di errori diversi, troppo numerosi per essere elencati in questo documento.Gli errori di questo tipo vengono restituiti al client così come sono, non viene eseguita alcuna trasformazione sugli oggetti dell'eccezione.  
  
 Gli errori di applicazione si verificano durante l'esecuzione di un'operazione del servizio.Errori di questo tipo vengono inviati al client come <xref:System.ServiceModel.FaultException> o <xref:System.ServiceModel.FaultException%601>.  
  
 La gestione degli errori in WCF viene eseguita secondo uno o più dei modi indicati di seguito.  
  
-   Gestione diretta dell'eccezione generata.Viene eseguita solo per gli errori di comunicazione di proxy\/canale.  
  
-   Utilizzo dei contratti di errore.  
  
-   Implementazione dell'interfaccia <xref:System.ServiceModel.Dispatcher.IErrorHandler>  
  
-   Gestione degli eventi <xref:System.ServiceModel.ServiceHost>  
  
## Contratti di errore  
 I contratti di errore consentono all'utente di definire gli errori che si possono verificare durante l'operazione del servizio in una modalità indipendente dalla piattaforma.Per impostazione predefinita tutte le eccezioni generate da un'operazione del servizio saranno restituite al client come oggetto <xref:System.ServiceModel.FaultException>.L'oggetto <xref:System.ServiceModel.FaultException> conterrà un numero molto contenuto di informazioni.È possibile controllare le informazioni inviate al client definendo un contratto di errori e restituendo l'errore come <xref:System.ServiceModel.FaultException%601>.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Specifica e gestione di errori in contratti e servizi](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md).  
  
## IErrorHandler  
 L'interfaccia <xref:System.ServiceModel.Dispatcher.IErrorHandler> consente un maggiore controllo delle risposte dell'applicazione WCF agli errori.Fornisce un controllo completo sul messaggio di errore restituito al client e consente di eseguire elaborazioni personalizzate dell'errore, ad esempio la registrazione.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)]<xref:System.ServiceModel.Dispatcher.IErrorHandler> e [Estensione del controllo sulla gestione e sulla segnalazione degli errori](../../../docs/framework/wcf/samples/extending-control-over-error-handling-and-reporting.md)  
  
## Eventi ServiceHost  
 La classe <xref:System.ServiceModel.ServiceHost> ospita i servizi e definisce diversi eventi che possono essere necessari per la gestione degli errori.Ad esempio:  
  
1.  <xref:System.ServiceModel.ServiceHost.Faulted>  
  
2.  <xref:System.ServiceModel.ServiceHost.UnknownMessageReceived>  
  
 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] <xref:System.ServiceModel.ServiceHost>