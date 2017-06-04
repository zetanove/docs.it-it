---
title: "Informazioni su Windows Communication Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "Windows Communication Foundation [WCF], panoramica della tecnologia"
  - "panoramica della tecnologia [WCF]"
  - "WCF [WCF], panoramica della tecnologia"
ms.assetid: 40e1009d-ef15-450b-9848-62eabe5e5738
caps.latest.revision: 51
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 49
---
# Informazioni su Windows Communication Foundation
[!INCLUDE[indigo1](../../../includes/indigo1-md.md)] è un framework per la compilazione di applicazioni orientate ai servizi. Grazie a [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è possibile inviare dati come messaggi asincroni da un endpoint del servizio a un altro. Un endpoint del servizio può appartenere a un servizio disponibile in modo continuo ospitato da IIS oppure essere un servizio ospitato in un'applicazione. Un endpoint può essere un client di un servizio che richiede dati da un endpoint del servizio. Il messaggio può essere semplice come una parola o come un singolo carattere inviato in formato XML o complesso come un flusso di dati binari. Di seguito vengono indicati alcuni scenari di esempio:  
  
-   Servizio protetto per elaborare le transazioni aziendali.  
  
-   Servizio che fornisce dati correnti ad altri, ad esempio un rapporto sul traffico o un altro servizio di monitoraggio.  
  
-   Servizio di chat che consente a due persone di comunicare o di scambiare dati in tempo reale.  
  
-   Applicazione dashboard che esegue il polling di uno o più servizi per i dati e che li visualizza in una presentazione logica.  
  
-   Esposizione di un flusso di lavoro implementato utilizzando Windows Workflow Foundation come servizio WCF.  
  
-   Applicazione Silverlight per eseguire il polling di un servizio per i feed di dati più recenti.  
  
 Sebbene fosse possibile creare queste applicazioni anche con programmi precedenti a [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], grazie a [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] lo sviluppo degli endpoint è stato semplificato. In breve, [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è stato progettato per consentire un approccio gestibile alla creazione di servizi Web e dei relativi client.  
  
## Funzionalità di WCF  
 In [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è disponibile il set di funzionalità seguente.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Dettagli delle funzioni di WCF](../../../docs/framework/wcf/feature-details/index.md).  
  
-   **Orientamento ai servizi**  
  
     L'utilizzo degli standard WS in [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] consente di creare applicazioni *orientate ai servizi*. Per architettura orientata ai servizi \(SOA, Service\-oriented architecture\) si intende un'architettura che si basa sui servizi Web per inviare e ricevere dati. I servizi sono in genere caratterizzati dal vantaggio di essere ad accoppiamento debole anziché hardcoded da un'applicazione a un'altra. Una relazione ad accoppiamento debole implica che un client creato in una qualsiasi piattaforma possa connettersi a un servizio qualsiasi a condizione che vengano soddisfatti i contratti essenziali.  
  
-   **Interoperabilità**  
  
     In [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] vengono implementati i moderni standard del settore per l'interoperabilità dei servizi Web.[!INCLUDE[crabout](../../../includes/crabout-md.md)]gli standard supportati, vedere [Interoperabilità e integrazione](../../../docs/framework/wcf/feature-details/interoperability-and-integration.md).  
  
-   **Più modelli di messaggio**  
  
     Per scambiare i messaggi, sono disponibili più modelli. Il modello più comune è di tipo request\/reply, in base al quale un endpoint richiede i dati a un altro endpoint che invia la risposta. Sono disponibili altri tipi di modelli in cui ad esempio un singolo endpoint invia un messaggio unidirezionale senza attendere una risposta. Un modello più complesso è costituito da un modello di scambio duplex in base al quale due endpoint stabiliscono una connessione e inviano i dati dall'uno all'altro in modo analogo a un'applicazione di messaggistica immediata.[!INCLUDE[crabout](../../../includes/crabout-md.md)] come implementare modelli di scambio di messaggi diversi usando [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], vedere [Contratti](../../../docs/framework/wcf/feature-details/contracts.md).  
  
-   **Metadati del servizio**  
  
     In [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è supportata la pubblicazione dei metadati del servizio tramite formati specificati in standard del settore, ad esempio WSDL, XML Schema e WS\-Policy. Tali metadati possono essere utilizzati per generare e configurare in modo automatico client per accedere a servizi di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]. I metadati possono inoltre essere pubblicati tramite protocolli HTTP e HTTPS oppure utilizzando lo standard WS\-Metadata Exchange.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Metadata](../../../docs/framework/wcf/feature-details/metadata.md).  
  
-   **Contratti dati**  
  
     Poiché è stato compilato utilizzando [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], in [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] sono inoltre inclusi metodi intuitivi per fornire i contratti da applicare. Uno dei tipi di contratti più generali è il contratto dati. In pratica, quando si crea il codice del servizio in Visual C\# o Visual Basic, il modo più semplice di gestire i dati è costituito dalla creazione di classi che rappresentano un'entità dati con proprietà che appartengono all'entità stessa. In [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è incluso un sistema completo per utilizzare i dati in base a questa semplice modalità. Dopo che sono state create le classi che rappresentano i dati, il servizio genera automaticamente i metadati che consentono ai client di essere conformi ai tipi di dati progettati.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Uso di contratti dati](../../../docs/framework/wcf/feature-details/using-data-contracts.md)  
  
-   **Sicurezza**  
  
     È possibile crittografare i dati per proteggere la privacy nonché chiedere agli utenti di eseguire l'autenticazione prima che siano in grado di ricevere messaggi. La sicurezza può essere implementata utilizzando standard noti, ad esempio SSL o WS\-SecureConversation.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Sicurezza](../../../docs/framework/wcf/feature-details/security.md).  
  
-   **Più trasporti e codifiche**  
  
     Per inviare i messaggi, è possibile utilizzare uno dei numerosi protocolli di trasporto e codifiche predefiniti. Il protocollo e la codifica più comuni prevedono l'invio di messaggi di testo SOAP codificati tramite il protocollo HTTP \(HyperText Transfer Protocol\) da utilizzare nel World Wide Web. In alternativa, [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] consente di inviare messaggi tramite TCP, named pipe o MSMQ. Tali messaggi possono essere codificati come testo oppure utilizzando un formato binario ottimizzato.  I dati binari possono essere inviati in modo efficiente tramite lo standard MTOM. Se nessuna delle codifiche o nessuno dei trasporti forniti soddisfa le esigenze, è possibile creare una codifica o un trasporto personalizzato.[!INCLUDE[crabout](../../../includes/crabout-md.md)]lle codifiche e sui trasporti supportati da [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], vedere [Trasporti](../../../docs/framework/wcf/feature-details/transports.md).  
  
-   **Messaggi in coda e affidabili**  
  
     In [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è supportato lo scambio affidabile di messaggi grazie a sessioni sicure implementate tramite WS\-Reliable Messaging e MSMQ.[!INCLUDE[crabout](../../../includes/crabout-md.md)]l supporto della messaggistica in coda e affidabile in [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], vedere [Code e sessioni affidabili](../../../docs/framework/wcf/feature-details/queues-and-reliable-sessions.md).  
  
-   **Messaggi durevoli**  
  
     Per messaggio durevole si intende un messaggio che non viene mai perso a causa di un'interruzione della comunicazione. I messaggi presenti in un modello di questo tipo vengono sempre salvati in un database. Se si verifica un'interruzione, quando la connessione viene ripristinata è possibile riprendere lo scambio dei messaggi. È inoltre possibile creare un messaggio durevole utilizzando [!INCLUDE[wf](../../../includes/wf-md.md)].[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Servizi flusso di lavoro](../../../docs/framework/wcf/feature-details/workflow-services.md).  
  
-   **Transazioni**  
  
     In WCF il supporto delle transazioni viene inoltre realizzato tramite uno dei tre modelli seguenti: WS\-AtomicTtransactions, le interfacce API nello spazio dei nomi <xref:System.Transactions> e Microsoft Distributed Transaction Coordinator.[!INCLUDE[crabout](../../../includes/crabout-md.md)]l supporto delle transazioni in [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], vedere [Transazioni](../../../docs/framework/wcf/feature-details/transactions-in-wcf.md).  
  
-   **Supporto AJAX e REST**  
  
     REST è un esempio di una tecnologia Web 2.0 in evoluzione.[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] può essere configurato per elaborare dati XML "semplici" che non sono incapsulati in una SOAP envelope. È inoltre possibile estendere [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] per supportare formati XML specifici, ad esempio ATOM \(uno standard RSS diffuso\) e anche formati non XML, ad esempio JSON \(JavaScript Object Notation\).  
  
-   **Extensibility**  
  
     L'architettura di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] dispone di un certo numero di punti di estensibilità. Se è necessaria ulteriore capacità, sono disponibili punti di ingresso che consentono di personalizzare il comportamento di un servizio.[!INCLUDE[crabout](../../../includes/crabout-md.md)]i punti di estendibilità disponibili, vedere [Estensione di WCF](../../../docs/framework/wcf/extending/extending-wcf.md).  
  
## Integrazione di WCF con altre tecnologie  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è una piattaforma estremamente flessibile. Grazie a questa notevole flessibilità, [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] viene usato anche in diversi altri prodotti Microsoft. Dopo aver acquisito familiarità con i concetti fondamentali di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], è possibile sfruttarne la conoscenza per utilizzare uno di tali prodotti.  
  
 La prima tecnologia associata a [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è stata Windows Workflow Foundation \(WF\). I flussi di lavoro semplificano lo sviluppo di applicazioni incapsulando i passaggi nel flusso di lavoro come "attività". Nella prima versione di [!INCLUDE[wf2](../../../includes/wf2-md.md)], lo sviluppatore doveva creare un host per il flusso di lavoro. La versione successiva di [!INCLUDE[wf2](../../../includes/wf2-md.md)] è stata integrata con [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]. In questo modo era possibile ospitare qualsiasi flusso di lavoro in un servizio di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] scegliendo automaticamente WF\/WCF come tipo di progetto in [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)].  
  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] viene inoltre utilizzato in Microsoft BizTalk Server R2 come tecnologia di comunicazione. BizTalk è progettato per ricevere e trasformare i dati da un formato standardizzato in un altro. I messaggi devono essere recapitati nel MessageBox centrale di BizTalk in cui il messaggio può essere trasformato tramite un mapping rigoroso o tramite una delle funzionalità di BizTalk, ad esempio il motore del flusso di lavoro. A questo punto in BizTalk è possibile utilizzare l'adattatore line\-of\-business di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] per recapitare i messaggi al MessageBox.  
  
 Microsoft Silverlight è una piattaforma per la creazione di applicazioni Web interoperabili e potenti che consentono agli sviluppatori di realizzare siti Web con contenuto multimediale completo, ad esempio flusso video. A partire dalla versione 2, in Silverlight è stato incorporato [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] come tecnologia di comunicazione per connettere le applicazioni di Silverlight agli endpoint di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
 Il server applicazioni [!INCLUDE[dublin](../../../includes/dublin-md.md)] è stato compilato appositamente per la distribuzione e la gestione di applicazioni che utilizzano [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] per la comunicazione. In [!INCLUDE[dublin2](../../../includes/dublin2-md.md)] sono disponibili strumenti e opzioni di configurazione potenti progettati in modo specifico per applicazioni abilitate all'utilizzo di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
## Vedere anche  
 <xref:System.ServiceModel>   
 [Concetti fondamentali di Windows Communication Foundation](../../../docs/framework/wcf/fundamental-concepts.md)   
 [Architettura di Windows Communication Foundation](../../../docs/framework/wcf/architecture.md)   
 [Linee guida e procedure consigliate](../../../docs/framework/wcf/guidelines-and-best-practices.md)   
 [Esercitazione introduttiva](../../../docs/framework/wcf/getting-started-tutorial.md)   
 [Guida alla documentazione](../../../docs/framework/wcf/guide-to-the-documentation.md)   
 [Programmazione WCF di base](../../../docs/framework/wcf/basic-wcf-programming.md)   
 [Windows Communication Foundation Samples](http://msdn.microsoft.com/it-it/8ec9d192-5d81-4f64-bfd3-90c5e5858c91)