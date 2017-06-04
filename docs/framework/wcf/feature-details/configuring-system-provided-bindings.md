---
title: "Configurazione di associazioni fornite dal sistema | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "associazione [WCF], fornito dal sistema"
  - "WCF [WCF], associazioni fornite dal sistema"
  - "Windows Communication Foundation [WCF], associazioni fornite dal sistema"
ms.assetid: 443f8d65-f1f2-4311-83b3-4d8fdf7ccf16
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# Configurazione di associazioni fornite dal sistema
Le associazioni specificano il meccanismo di comunicazione da utilizzare durante la comunicazione con un endpoint e indicano come collegarsi a un endpoint.  Le associazioni sono costituite da elementi che definiscono come sono sovrapposti i canali [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per fornire le funzionalità di comunicazione richieste.  Un'associazione contiene tre tipi di elementi:  
  
-   Elementi di associazione dei canali di protocollo che determinano la sicurezza, l'affidabilità, le impostazioni di flusso del contesto o i protocolli definiti dall'utente da utilizzare con i messaggi inviati all'endpoint.  
  
-   Elementi di associazione del canale di trasporto, che determinano il protocollo di trasporto sottostante da utilizzare quando si inviano messaggi all'endpoint, ad esempio, TCP o HTTP.  
  
-   Elementi di associazione della codifica dei messaggi, che determinano la codifica di trasmissione da utilizzare per i messaggi inviati all'endpoint, ad esempio, testo\/XML, binari o MTOM \(Message Transmission Optimization Mechanism\).  
  
 In questo argomento vengono illustrate tutte le associazioni [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] fornite dal sistema.  Se nessuna di esse soddisfa i requisiti specifici dell'applicazione, è possibile creare un'associazione utilizzando la classe <xref:System.ServiceModel.Channels.CustomBinding>.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]lla creazione di associazioni personalizzate, vedere [Associazioni personalizzate](../../../../docs/framework/wcf/extending/custom-bindings.md).  
  
> [!IMPORTANT]
>  Selezionare un'associazione con la sicurezza attivata.  Per impostazione predefinita, tutte le associazioni, tranne l'associazione <xref:System.ServiceModel.BasicHttpBinding>, hanno la sicurezza attivata.  Se non si seleziona un'associazione protetta o se si disattiva la sicurezza, assicurarsi che gli scambi di rete siano protetti in qualche altro modo, ad esempio archiviandoli in un centro dati protetto o in una rete isolata.  
  
> [!IMPORTANT]
>  Non utilizzare contratti duplex con associazioni che non supportano la sicurezza o che hanno la sicurezza disattivata, a meno che lo scambio di rete non sia protetto in altro modo.  
  
## Associazioni fornite dal sistema  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è dotato delle associazioni seguenti.  
  
|Binding|Elemento di configurazione|Descrizione|  
|-------------|--------------------------------|-----------------|  
|<xref:System.ServiceModel.BasicHttpBinding>|[\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)|Associazione idonea per comunicare con servizi Web conformi a WS\-Basic Profile, ad esempio servizi basati su servizi Web ASP.NET \(ASMX\).  Questa associazione utilizza HTTP come trasporto e testo\/XML come codifica dei messaggi predefinita.|  
|<xref:System.ServiceModel.WSHttpBinding>|[\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)|Un'associazione protetta e interoperabile adatta per contratti di servizio non duplex.|  
|<xref:System.ServiceModel.WS2007HttpBinding>|[\<ws2007HttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/ws2007httpbinding.md)|Associazione protetta e interoperabile che fornisce il supporto per le versioni corrette degli elementi di associazione <xref:System.ServiceModel.WSHttpBinding.Security%2A>, <xref:System.ServiceModel.ReliableSession> e <xref:System.ServiceModel.WSHttpBindingBase.TransactionFlow%2A>.|  
|<xref:System.ServiceModel.WSDualHttpBinding>|[\<wsDualHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md)|Associazione protetta e interoperabile adatta per contratti di servizio duplex o per la comunicazione tramite intermediari SOAP.|  
|<xref:System.ServiceModel.WSFederationHttpBinding>|[\<wsFederationHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md)|Associazione protetta e interoperabile che supporta il protocollo WS\-Federation, che consente alle organizzazioni di una federazione di autenticare e autorizzare gli utenti in modo efficiente.|  
|<xref:System.ServiceModel.WS2007FederationHttpBinding>|[\<ws2007FederationHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/ws2007federationhttpbinding.md)|Associazione protetta e interoperabile che deriva da <xref:System.ServiceModel.WS2007HttpBinding> e supporta la sicurezza federata.|  
|<xref:System.ServiceModel.NetTcpBinding>|[\<netTcpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md)|Associazione protetta e ottimizzata adatta per le comunicazioni tra computer, tra applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].|  
|<xref:System.ServiceModel.NetNamedPipeBinding>|[\<netNamedPipeBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/netnamedpipebinding.md)|Associazione protetta, affidabile e ottimizzata adatta per la comunicazione in un computer, tra applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].|  
|<xref:System.ServiceModel.NetMsmqBinding>|[\<netMsmqBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/netmsmqbinding.md)|Associazione in coda adatta per la comunicazione tra computer, tra applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].|  
|<xref:System.ServiceModel.NetPeerTcpBinding>|[\<netPeerTcpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/netpeertcpbinding.md)|Associazione che consente comunicazioni protette tra più computer.|  
|<xref:System.ServiceModel.WebHttpBinding>|[\<webHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/webhttpbinding.md)|Associazione utilizzata per configurare endpoint per servizi Web [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] esposti tramite richieste HTTP anziché tramite messaggi SOAP.|  
|<xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>|[\<msmqIntegrationBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/msmqintegrationbinding.md)|Associazione adatta per la comunicazione tra computer, tra un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e le applicazioni di Accodamento messaggi esistenti \(note anche come MSMQ\).|  
  
## Funzionalità di associazione  
 Nella tabella seguente sono riportate alcune delle funzionalità chiave di ogni associazione fornita dal sistema:  Le associazioni sono riportate nella prima colonna, mentre le informazioni relative alle funzionalità sono descritte nella tabella.  Nella tabella seguente viene fornita una chiave per le abbreviazioni delle associazioni utilizzate.  Per selezionare un'associazione, stabilire qual è la colonna che soddisfa tutte le funzioni della riga necessarie.  
  
|Binding|Interoperabilità|Modalità di sicurezza \(impostazione predefinita\)|Sessione<br /><br /> \(Predefinito\)|Transazioni|Duplex|  
|-------------|----------------------|--------------------------------------------------------|----------------------------------|-----------------|------------|  
|<xref:System.ServiceModel.BasicHttpBinding>|Basic Profile 1.1|\(None\), Transport, Message, misto|None, \(None\)|\(Nessuno\)|N\/D|  
|<xref:System.ServiceModel.WSHttpBinding>|WS|None, Transport, \(Message\), misto|\(None\), Transport, sessione affidabile|\(None\), sì|N\/D|  
|<xref:System.ServiceModel.WS2007HttpBinding>|WS\-Security, WS\-Trust, WS\-SecureConversation, WS\-SecurityPolicy|None, Transport, \(Message\), misto|\(None\), Transport, sessione affidabile|\(None\), sì|N\/D|  
|<xref:System.ServiceModel.WSDualHttpBinding>|WS|None, \(Message\)|\(Sessione affidabile\)|\(None\), sì|Sì|  
|<xref:System.ServiceModel.WSFederationHttpBinding>|WS\-Federation|None, \(Message\), misto|\(None\), sessione affidabile|\(None\), sì|No|  
|<xref:System.ServiceModel.WS2007FederationHttpBinding>|WS\-Federation|None, \(Message\), misto|\(None\), sessione affidabile|\(None\), sì|No|  
|<xref:System.ServiceModel.NetTcpBinding>|.NET|None, \(Transport\), Message,<br /><br /> Mixed|Sessione affidabile, \(Transport\)|\(None\), sì|Sì|  
|<xref:System.ServiceModel.NetNamedPipeBinding>|.NET|None,<br /><br /> \(Transport\)|None, \(Transport\)|\(None\), sì|Sì|  
|<xref:System.ServiceModel.NetMsmqBinding>|.NET|None, Message, \(Transport\), Both|\(Nessuno\)|\(None\), sì|No|  
|<xref:System.ServiceModel.NetPeerTcpBinding>|Peer|None, Message, \(Transport\), misto|\(Nessuno\)|\(Nessuno\)|Sì|  
|<xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>|MSMQ|None, \(Transport\)|\(Nessuno\)|\(None\), sì|n\/d|  
  
 Nella tabella seguente sono spiegate le funzionalità elencate nella tabella precedente.  
  
|Funzionalità|Descrizione|  
|------------------|-----------------|  
|Tipo di interoperabilità|Denomina il protocollo o la tecnologia con cui l'associazione assicura l'interoperatività.|  
|Sicurezza|Specifica come il canale viene protetto:<br /><br /> -   None: il messaggio SOAP non è protetto e il client non è autenticato.<br />-   Transport: i requisiti di sicurezza sono soddisfatti a livello di trasporto.<br />-   Message: i requisiti di sicurezza sono soddisfatti a livello di messaggio.<br />-   Misto: questa modalità di sicurezza è nota come `TransportWithMessageCredentials`.  Gestisce le credenziali a livello di messaggio, mentre i requisiti di integrità e riservatezza sono soddisfatti dal livello di trasporto.<br />-   Both: viene utilizzata sia la sicurezza a livello di messaggio sia quella a livello di trasporto.  Questa possibilità è disponibile solo per <xref:System.ServiceModel.NetMsmqBinding>.|  
|Sessione|Specifica se questa associazione supporta contratti di sessione.|  
|Transazioni|Specifica se le transazioni sono attivate.|  
|Duplex|Specifica se sono supportati contratti duplex.  Si noti che questa funzionalità richiede il supporto delle sessioni nell'associazione.|  
|Flusso|Specifica se il flusso dei messaggi è supportato.|  
  
## Vedere anche  
 [Cenni preliminari sulla creazione di endpoint](../../../../docs/framework/wcf/endpoint-creation-overview.md)   
 [Uso di associazioni per configurare servizi e client](../../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)   
 [Programmazione WCF di base](../../../../docs/framework/wcf/basic-wcf-programming.md)