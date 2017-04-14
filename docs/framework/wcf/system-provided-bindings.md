---
title: "Associazioni fornite dal sistema | Microsoft Docs"
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
  - "associazione [WCF], fornito dal sistema"
ms.assetid: 2c243746-45ce-4588-995e-c17126a579a6
caps.latest.revision: 60
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 60
---
# Associazioni fornite dal sistema
Le associazioni specificano il meccanismo di comunicazione da utilizzare durante la comunicazione con un endpoint e indicano come collegarsi a un endpoint.Un'associazione contiene gli elementi seguenti:  
  
-   Lo stack del protocollo determina la protezione, l'affidabilità e le impostazioni del flusso di contesto da utilizzare per i messaggi inviati all'endpoint.  
  
-   Il trasporto determina il protocollo di trasporto sottostante da utilizzare quando si inviano messaggi all'endpoint, ad esempio, TCP o HTTP.  
  
-   La codifica determina la codifica di trasmissione da utilizzare per i messaggi inviati all'endpoint, ad esempio, testo\/XML, binaria o MTOM \(Message Transmission Optimization Mechanism\).  
  
 In questo argomento vengono illustrate tutte le associazioni [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] fornite dal sistema.Se nessuna di queste soddisfa i criteri esatti per l'applicazione, è possibile creare un'associazione personalizzata.[!INCLUDE[crabout](../../../includes/crabout-md.md)] creazione di associazioni personalizzate, vedere [Associazioni personalizzate](../../../docs/framework/wcf/extending/custom-bindings.md).  
  
 Un'associazione protetta e interoperabile che supporta il protocollo WS\-Federation consente alle organizzazioni di una federazione di autenticare e autorizzare gli utenti in modo efficiente.  
  
> [!IMPORTANT]
>  Selezionare sempre un'associazione che include la protezione.Per impostazione predefinita, tutte le associazioni, tranne l'elemento [\<basicHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md), hanno la protezione attivata.Se non si seleziona un'associazione protetta o se si disattiva la protezione, assicurarsi di proteggere i dati in altro modo, ad esempio archiviandoli in un centro dati protetto o in una rete isolata.  
  
> [!IMPORTANT]
>  Non utilizzare mai contratti duplex con associazioni che non supportano la protezione o che hanno la protezione disattivata, a meno che non si proteggano i dati in altro modo.  
  
## Associazioni fornite dal sistema  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è dotato delle associazioni seguenti.  
  
|Associazione|Elemento di configurazione|Descrizione|  
|------------------|--------------------------------|-----------------|  
|<xref:System.ServiceModel.BasicHttpBinding>|[\<basicHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)|Associazione idonea per comunicare con servizi Web conformi a WS\-Basic Profile, ad esempio, servizi su servizi Web ASP.NET \(ASMX\).Questa associazione utilizza HTTP come trasporto e testo\/XML come codifica dei messaggi predefinita.|  
|<xref:System.ServiceModel.WSHttpBinding>|[\<wsHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)|Un'associazione protetta e interoperabile adatta per contratti di servizio non duplex.|  
|<xref:System.ServiceModel.WSDualHttpBinding>|[\<wsDualHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md)|Associazione protetta e interoperabile adatta per contratti di servizio duplex o per la comunicazione tramite intermediari SOAP.|  
|<xref:System.ServiceModel.WSFederationHttpBinding>|[\<wsFederationHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md)|Associazione protetta e interoperabile che supporta il protocollo WS\-Federation che consente alle organizzazioni di una federazione di autenticare e autorizzare gli utenti in modo efficiente.|  
|<xref:System.ServiceModel.NetHttpBinding>|\<netHttpBinding\>|Associazione progettata per utilizzare i servizi HTTP o WebSocket che utilizza la codifica binaria per impostazione predefinita.|  
|<xref:System.ServiceModel.NetHttpsBinding>|\<netHttpsBinding\>|Associazione protetta progettata per utilizzare i servizi HTTP o WebSocket che utilizza la codifica binaria per impostazione predefinita.|  
|<xref:System.ServiceModel.NetTcpBinding>|[\<netTcpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md)|Associazione protetta e ottimizzata adatta per le comunicazioni tra computer tra applicazioni [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].|  
|<xref:System.ServiceModel.NetNamedPipeBinding>|[\<netNamedPipeBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/netnamedpipebinding.md)|Associazione protetta, affidabile e ottimizzata adatta per la comunicazione in un computer, tra applicazioni [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].|  
|<xref:System.ServiceModel.NetMsmqBinding>|[\<netMsmqBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/netmsmqbinding.md)|Associazione in coda adatta per la comunicazione tra computer, tra applicazioni [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].|  
|<xref:System.ServiceModel.NetPeerTcpBinding>|[\<netPeerTcpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/netpeertcpbinding.md)|Associazione che consente comunicazioni sicure tra più computer.|  
|<xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>|[\<msmqIntegrationBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/msmqintegrationbinding.md)|Associazione adatta per la comunicazione tra computer, tra un'applicazione [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e le applicazioni di Accodamento messaggi esistenti.|  
|<xref:System.ServiceModel.BasicHttpContextBinding>|[\<basicHttpContextBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/basichttpcontextbinding.md)|Associazione adatta per la comunicazione con servizi Web conformi a WS\-Basic Profile che consente l'utilizzo di cookie HTTP per lo scambio del contesto.|  
|<xref:System.ServiceModel.NetTcpContextBinding>|[\<netTcpContextBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/nettcpcontextbinding.md)|Associazione sicura e ottimizzata adatta per le comunicazioni tra computer, tra applicazioni [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]. Consente l'utilizzo delle intestazioni SOAP per lo scambio del contesto.|  
|<xref:System.ServiceModel.WebHttpBinding>|[\<webHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/webhttpbinding.md)|Associazione utilizzata per configurare endpoint per servizi Web [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] esposti tramite richieste HTTP anziché tramite messaggi SOAP.|  
|<xref:System.ServiceModel.WSHttpContextBinding>|[\<wsHttpContextBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/wshttpcontextbinding.md)|Associazione sicurea e interoperativa adatta per contratti di servizio non duplex che consente l'utilizzo delle intestazioni SOAP per lo scambio del contesto.|  
|<xref:System.ServiceModel.Channels.UdpBinding>|\<udpBinding\>|Associazione da utilizzare quando si invia un burst di messaggi semplici a numerosi client contemporaneamente.|  
  
 Nella tabella seguente sono riportate le funzionalità di ogni associazione fornita dal sistema:Le associazioni sono riportate nelle colonne della tabella, mentre le funzionalità sono elencate nelle righe e descritte in una seconda tabella.Nella tabella seguente viene fornita una chiave per le abbreviazioni delle associazioni utilizzate.Per selezionare un'associazione, stabilire qual è la colonna che soddisfa tutte le funzioni della riga richieste.  
  
|Associazione|Interoperabilità|Protezione \(predefinita\)|Sessione<br /><br /> \(Predefinito\)|Transazioni|Duplex|Codifica \(predefinita\)|Flusso<br /><br /> \(Predefinito\)|  
|------------------|----------------------|--------------------------------|----------------------------------|-----------------|------------|------------------------------|--------------------------------|  
|<xref:System.ServiceModel.BasicHttpBinding>|Basic Profile 1.1|\(None\), Transport, Message, misto|\(Nessuno\)|\(Nessuno\)|n\/d|Text, \(MTOM\)|Sì<br /><br /> \(memorizzato nel buffer\)|  
|<xref:System.ServiceModel.WSHttpBinding>|WS|Transport, \(Message\), misto|\(None\), sessione affidabile, sessione di sicurezza|\(None\), sì|n\/d|\(Text\), MTOM|No|  
|<xref:System.ServiceModel.WSDualHttpBinding>|WS|\(Message\), None|\(Sessione affidabile\), sessione di sicurezza|\(None\), sì|Sì|\(Text\), MTOM|No|  
|<xref:System.ServiceModel.WSFederationHttpBinding>|WS\-Federation|\(Message\), misto, None|\(None\), sessione affidabile, sessione di sicurezza|\(None\), sì|No|\(Text\), MTOM|No|  
|<xref:System.ServiceModel.NetHttpBinding>|.NET|\(None\), Transport, Message, TransportWithMessageCredential, TransportCredentialOnly|Vedere la nota più avanti|None|Vedere la nota più avanti|\(Binary\), Text,MTOM|Sì \(memorizzato nel buffer\)|  
|T:System.ServiceModel.NetHttpsBinding|.NET|\(Transport\), TransportWithMessageCredential|Vedere la nota più avanti|None|Vedere la nota più avanti|\(Binary\), Text,MTOM|Sì \(memorizzato nel buffer\)|  
|<xref:System.ServiceModel.NetTcpBinding>|.NET|\(Transport\), Message, None, misto|\(Transport\), sessione affidabile, sessione di sicurezza|\(None\), sì|Sì|binari|Sì<br /><br /> \(memorizzato nel buffer\)|  
|<xref:System.ServiceModel.NetNamedPipeBinding>|.NET|\(Transport\), None|None, \(Transport\)|\(None\), sì|Sì|binari|Sì<br /><br /> \(memorizzato nel buffer\)|  
|<xref:System.ServiceModel.NetMsmqBinding>|.NET|Message, \(Transport\), None|\(None\), Transport|None, \(sì\)|No|binari|No|  
|<xref:System.ServiceModel.NetPeerTcpBinding>|Peer|\(Transport\)|\(Nessuno\)|\(Nessuno\)|Sì||No|  
|<xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>|MSMQ|\(Transport\)|\(Nessuno\)|None, \(sì\)|n\/d|n\/d|No|  
|<xref:System.ServiceModel.BasicHttpContextBinding>|Basic Profile 1.1|\(None\), Transport, Message, misto|\(Nessuno\)|\(Nessuno\)|n\/d|Text, \(MTOM\)|Sì<br /><br /> \(memorizzato nel buffer\)|  
|<xref:System.ServiceModel.NetTcpContextBinding>|.NET|\(Transport\), Message, None, misto|\(Transport\), sessione affidabile, sessione di sicurezza|\(None\), sì|Sì|Binario|Sì<br /><br /> \(memorizzato nel buffer\)|  
|<xref:System.ServiceModel.WSHttpContextBinding>|WS|Transport, \(Message\), misto|\(None\), sessione affidabile, sessione di sicurezza|\(None\), sì|n\/d|Text, \(MTOM\)|No|  
|<xref:System.ServiceModel.Channels.UdpBinding>|.NET **Note:**  L'interoperabilità può essere ottenuta implementando la specifica standard SOAP\-over\-UDP implementata da questa associazione.|\(Nessuno\)|\(Nessuno\)|\(Nessuno\)|n\/d|\(Text\)|No|  
  
> [!IMPORTANT]
>  <xref:System.ServiceModel.NetHttpBinding> è un'associazione progettata per utilizzare i servizi HTTP o WebSocket e utilizza la codifica binaria per impostazione predefinita.L'oggetto <xref:System.ServiceModel.NetHttpBinding> rileverà se viene utilizzato con un contratto request\/reply o un contratto duplex e modificherà il comportamento di conseguenza. Utilizzerà HTTP per il primo caso e WebSockets per il secondo.Questo comportamento può essere modificato mediante le impostazioni dell'associazione <xref:System.ServiceModel.NetHttpBinding.WebSocketTransportUsage%2A>, cioè Allowed, ovvero il valore predefinito che determina il comportamento descritto in precedenza o NotAllowed, con cui si evita l'utilizzo di WebSockets.Il tentativo di utilizzo di un contratto duplex con questa impostazione genererà un'eccezione. Required: questa impostazione impone l'utilizzo di WebSockets anche per i contratti request\/reply. NetHttpBinding supporta sessioni affidabili sia in modalità HTTP sia in modalità WebSocket.Nella modalità WebSocket, le sessioni vengono fornite dal trasporto.  
  
 Nella tabella seguente sono spiegate le funzionalità elencate nella tabella precedente.  
  
|Funzionalità|Descrizione|  
|------------------|-----------------|  
|Tipo di interoperabilità|Denomina il protocollo o la tecnologia con cui l'associazione assicura l'interoperatività.|  
|Protezione|Specifica come il canale viene protetto:<br /><br /> -   None: il messaggio SOAP non è protetto e il client non è autenticato.<br />-   Transport: i requisiti di sicurezza sono soddisfatti a livello di trasporto.<br />-   Message: i requisiti di sicurezza sono soddisfatti a livello di messaggio.<br />-   Misto: le attestazioni sono contenute nel messaggio, i requisiti di integrità e riservatezza sono soddisfatti dal livello di trasporto.|  
|Sessione|Specifica se questa associazione supporta contratti di sessione.|  
|Transactions|Specifica se le transazioni sono attivate.|  
|Duplex|Specifica se sono supportati contratti duplex.Si noti che questa funzionalità richiede il supporto delle sessioni nell'associazione.|  
|Codifica|Specifica il formato di trasmissione del messaggio.I valori consentiti includono:<br /><br /> -   Text: ad esempio UTF\-8.<br />-   Binario<br />-   MTOM \(Message Transmission Optimization Mechanism\): consente di codificare in modo efficiente elementi XML binari all'interno del contesto di una SOAP envelope.|  
|Flusso|Specifica se il flusso è supportato per i messaggi in ingresso e in uscita.Utilizzare la proprietà `TransferMode` nell'associazione per impostare il valore.I valori consentiti includono:<br /><br /> -   <xref:System.ServiceModel.TransferMode>: i messaggi di richiesta e risposta vengono entrambi memorizzati nel buffer.<br />-   <xref:System.ServiceModel.TransferMode>: i messaggi di richiesta e risposta vengono entrambi inviati nel flusso.<br />-   <xref:System.ServiceModel.TransferMode>: il messaggio di richiesta viene inviato nel flusso e quello di risposta viene memorizzato nel buffer.<br />-   <xref:System.ServiceModel.TransferMode>: il messaggio di richiesta viene memorizzato nel buffer e quello di risposta viene inviato nel flusso.|  
  
## Vedere anche  
 [Cenni preliminari sulla creazione di endpoint](../../../docs/framework/wcf/endpoint-creation-overview.md)   
 [Uso di associazioni per configurare servizi e client](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)   
 [Programmazione WCF di base](../../../docs/framework/wcf/basic-wcf-programming.md)