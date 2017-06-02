---
title: "Panoramica dei servizi flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e536dda3-e286-441e-99a7-49ddc004b646
caps.latest.revision: 30
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 30
---
# Panoramica dei servizi flusso di lavoro
I servizi flusso di lavoro sono servizi basati su [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implementati mediante flussi di lavoro.  Si tratta di flussi di lavoro che usano le attività di messaggistica per inviare e ricevere messaggi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  .NET Framework 4.5 introduce una serie di attività di messaggistica che consentono di inviare e ricevere messaggi da un flusso di lavoro.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]lle attività di messaggistica e su come usarle per implementare diversi modelli per lo scambio di messaggi, vedere [Attività di messaggistica](../../../../docs/framework/wcf/feature-details/messaging-activities.md).  
  
## Vantaggi derivanti dall'utilizzo dei servizi flusso di lavoro  
 Con l'aumento del livello di distribuzione delle applicazioni, i singoli servizi divengono responsabili delle chiamate ad altri servizi per la ripartizione di parte del carico di lavoro.  L'implementazione di queste chiamate come operazioni asincrone introduce un livello di complessità nel codice.  La gestione degli errori aggiunge ulteriore complessità con la gestione delle eccezioni e fornendo informazioni di rilevamento dettagliate.  Alcuni servizi presentano spesso un'esecuzione prolungata e possono impegnare risorse di sistema utili in attesa dell'input.  A causa di questi problemi, le applicazioni distribuite risultano spesso molto complesse e difficili da scrivere e gestire.  I flussi di lavoro rappresentano un metodo naturale per esprimere la coordinazione del lavoro asincrono, soprattutto per quanto riguarda le chiamate ai servizi esterni.  I flussi di lavoro risultano inoltre efficaci nel rappresentare processi aziendali con esecuzione prolungata.  Sono queste qualità che rendono il flusso di lavoro una risorsa essenziale per la compilazione di servizi in un ambiente distribuito.  
  
## Implementazione di un servizio flusso di lavoro  
 In caso di implementazione di un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene definito un numero di contratti che descrivono il servizio e i dati inviati e ricevuti.  I dati vengono rappresentati come contratti dati e contratti di messaggio.  I servizi flusso di lavoro e WFC usano definizioni del contratto dati e del contratto messaggio nell'ambito delle descrizioni del servizio.  Il servizio stesso espone metadati \(nel formato WSDL\) per descrivere le operazioni del servizio.  In WCF i contratti di servizio e i contratti di operazione definiscono il servizio e le operazioni supportate.  Tuttavia in un servizio flusso di lavoro questi contratti rientrano nel processo aziendale stesso.  Vengono esposti nei metadati da un processo denominato inferenza del contratto.  Se un servizio flusso di lavoro viene ospitato mediante <xref:System.ServiceModel.Activities.WorkflowServiceHost>, viene esaminata la definizione del flusso di lavoro e viene generato un contratto in base al set delle attività di messaggistica rilevato nel flusso di lavoro.  In particolare vengono usate le attività e le proprietà indicate di seguito per generare il contratto:  
  
 Attività <xref:System.ServiceModel.Activities.Receive>  
  
-   <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A>  
  
-   <xref:System.ServiceModel.Activities.Receive.OperationContractName%2A>  
  
-   <xref:System.ServiceModel.Activities.Receive.Action%2A>  
  
-   <xref:System.ServiceModel.Activities.Receive.ValueType%2A>  
  
 Attività <xref:System.ServiceModel.Activities.SendReply>  
  
-   <xref:System.ServiceModel.Activities.SendReply.Action%2A>  
  
-   <xref:System.ServiceModel.Activities.SendReply.ValueType%2A>  
  
 Attività <xref:System.ServiceModel.Activities.TransactedReceiveScope>  
  
 Il risultato finale di inferenza del contratto rappresenta una descrizione del servizio usando le stesse strutture dei dati dei contratti dell'operazione e dei servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  Queste informazioni vengono quindi usate per esporre WSDL per il servizio flusso di lavoro.  
  
> [!NOTE]
>  [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] non consente di scrivere servizi flusso di lavoro usando una definizione del contratto esistente senza il supporto di strumenti aggiuntivi.  I contratti del servizio flusso di lavoro vengono creati dal processo di inferenza del contratto illustrato in precedenza.  I contratti di messaggio e i contratti dati sono tuttavia completamente supportati.  
  
## Servizi flusso di lavoro e associazioni basate su MSMQ  
 WCF definisce due associazioni <xref:System.ServiceModel.NetMsmqBinding> e <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> basate su MSMQ.  Le associazioni basate su MSMQ vengono spesso usate con i servizi flusso di lavoro, poiché tali servizi presentano un'esecuzione prolungata.  Le associazioni basate su MSMQ dispongono di una proprietà `ValidityDuration` che specifica per quanto tempo i messaggi MSMQ possono essere ritenuti validi.  A causa della natura prolungata dei servizi flusso di lavoro, la durata di validità di un messaggio MSMQ potrebbe scadere prima che il servizio flusso di lavoro possa elaborarlo.  È pertanto estremamente importante impostare la durata di validità di un'associazione MSMQ su un valore appropriato.  Questo valore deve essere scelto in base al flusso di lavoro e alla relativa modalità di elaborazione dei messaggi.  Se ad esempio si dispone di un flusso di lavoro con un'attività <xref:System.ServiceModel.Activities.Receive> seguita da un'attività personalizzata con tempo di esecuzione pari a 10 minuti, seguita da un'altra attività <xref:System.ServiceModel.Activities.Receive>, il valore corretto per `ValidityDuration` dovrà essere superiore a 10 minuti.  
  
## Hosting di un servizio flusso di lavoro  
 Come i servizi di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], i servizi flusso di lavoro devono essere ospitati.  I servizi di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] usano la classe <xref:System.ServiceModel.ServiceHost> per ospitare servizi, mentre i servizi flusso di lavoro usano <xref:System.ServiceModel.Activities.WorkflowServiceHost> per ospitare i servizi.  Come per i servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], i servizi flusso di lavoro possono essere ospitati in vari modi, ad esempio:  
  
-   in un'applicazione [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] gestita;  
  
-   In Internet Information Services \(IIS\).  
  
-   nel servizio Attivazione Processo Windows \(WAS, Windows Process Activation Service\);  
  
-   in un servizio Windows gestito.  
  
 I servizi flusso di lavoro ospitati in un'applicazione [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] o in un servizio Windows gestito creano un'istanza della classe <xref:System.ServiceModel.Activities.WorkflowServiceHost> e la passano a un'istanza di <xref:System.ServiceModel.Activities.WorkflowService> che contiene la definizione del flusso di lavoro all'interno della proprietà <xref:System.ServiceModel.Activities.WorkflowService.Body%2A>.  Una definizione del flusso di lavoro contenente le attività di messaggistica viene esposta come servizio flusso di lavoro.  
  
 Per ospitare un servizio flusso di lavoro in IIS o WAS, posizionare il file con estensione xamlx contenente la definizione del servizio flusso di lavoro in una directory virtuale.  Viene creato automaticamente un endpoint predefinito \(che usa <xref:System.ServiceModel.BasicHttpBinding>\) [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Configurazione semplificata](../../../../docs/framework/wcf/simplified-configuration.md).  È anche possibile posizionare un file Web.config nella directory virtuale per specificare specifici endpoint.  Se la definizione del flusso di lavoro si trova in un assembly, è possibile posizionare un file con estensione svc nella directory virtuale e l'assembly del flusso di lavoro nella directory App\_Code.  Il file con estensione svc deve specificare la factory di host del servizio e la classe che implementa il servizio flusso di lavoro.  Nell'esempio seguente viene mostrato come specificare la factory di host del servizio e la classe che implementa il servizio flusso di lavoro.  
  
```  
<%@ServiceHost Factory=" System.ServiceModel.Activities.Activation.WorkflowServiceHostFactory  
Service="EchoService"%>  
```