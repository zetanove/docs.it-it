---
title: "Trasferimento dei messaggi di flusso | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 72a47a51-e5e7-4b76-b24a-299d51e0ae5a
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Trasferimento dei messaggi di flusso
I trasporti di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] supportano due modalità di trasferimento dei messaggi:  
  
-   Trasferimento con memorizzazione nel buffer: in questa modalità, l'intero messaggio viene memorizzato in un buffer fino al completamento del trasferimento.Un messaggio memorizzato nel buffer deve essere completamente recapitato prima che un destinatario sia in grado di leggerlo.  
  
-   Trasferimento con flusso: in questa modalità il messaggio viene esposto come flusso.Il destinatario inizia a elaborare il messaggio prima che quest'ultimo venga recapitato per intero.  
  
-   I trasferimenti con flusso possono migliorare la scalabilità di un servizio eliminando l'esigenza di utilizzare buffer di memoria di grandi dimensioni.La capacità di migliorare la scalabilità mediante l'impostazione della modalità di trasferimento con flusso dipende dalle dimensioni dei messaggi da trasferire.In particolare, la modalità di trasferimento con flusso risulta essere più efficiente negli scenari che prevedono messaggi di grandi dimensioni.  
  
 Per impostazione predefinita, i trasporti HTTP, TCP\/IP e pipe con nome utilizzano la modalità di trasferimento con memorizzazione nel buffer.Questo documento descrive come configurare questi trasporti in modo che utilizzino la modalità di trasferimento con flusso e le relative conseguenze.  
  
## Attivazione dei trasferimenti con flusso  
 Per impostare una delle due modalità di trasferimento occorre intervenire sull'elemento di associazione del trasporto.L'elemento di associazione presenta una proprietà <xref:System.ServiceModel.TransferMode> che può essere impostata su `Buffered`, `Streamed`, `StreamedRequest` o `StreamedResponse`.L'impostazione della modalità di trasferimento su `Streamed` consente di attivare la comunicazione con flusso bidirezionale.L'impostazione della modalità di trasferimento su `StreamedRequest` o `StreamedResponse` consente di attivare la comunicazione con flusso soltanto nella direzione scelta.  
  
 Le associazioni <xref:System.ServiceModel.BasicHttpBinding>, <xref:System.ServiceModel.NetTcpBinding> e <xref:System.ServiceModel.NetNamedPipeBinding> espongono la proprietà <xref:System.ServiceModel.TransferMode>.Per impostare la modalità di trasferimento degli altri trasporti è necessario creare un'associazione personalizzata.  
  
 La scelta della modalità di trasferimento da utilizzare viene effettuata localmente dall'endpoint specifico.Per i trasporti HTTP, la modalità di trasferimento non si propaga attraverso una connessione, né verso server o altri intermediari.L'impostazione della modalità di trasferimento non influisce sulla descrizione dell'interfaccia del servizio.Dopo aver generato una classe client per un servizio, per impostare la modalità è necessario modificare il file di configurazione dei servizi per cui si desidera utilizzare la modalità di trasferimento con flusso.Per i trasporti TCP e named pipe, la modalità di trasferimento viene propagata come un'asserzione di criteri.  
  
 Per esempi di codice, vedere [Procedura: attivare il flusso](../../../../docs/framework/wcf/feature-details/how-to-enable-streaming.md).  
  
## Abilitazione del flusso asincrono  
 Per abilitare il flusso asincrono, aggiungere il comportamento dell'endpoint <xref:System.ServiceModel.Description.DispatcherSynchronizationBehavior> all'host del servizio e impostare la relativa proprietà <xref:System.ServiceModel.Description.DispatcherSynchronizationBehavior.AsynchronousSendEnabled%2A> su `true`.  
  
 In questa versione di WCF è stata inoltre aggiunta la funzionalità di un vero flusso asincrono sul lato di invio.In questo modo si migliora la scalabilità del servizio negli scenari in cui sta trasmettendo messaggi a più client, alcuni dei quali sono lenti nella lettura, probabilmente a causa della congestione della rete o della totale assenza di tale operazione.In questi scenari, WCF non blocca più i singoli thread sul servizio per client.In questo modo si garantisce che il servizio possa elaborare molti più client, migliorando pertanto la scalabilità del servizio.  
  
## Restrizioni sui trasferimenti con flusso  
 L'utilizzo della modalità di trasferimento con flusso comporta l'applicazione di restrizioni aggiuntive da parte del runtime.  
  
 Le operazioni che si verificano in un trasporto con flusso possono presentare un contratto avente al massimo un solo parametro di input oppure un solo parametro output.Questo parametro corrisponde al corpo intero del messaggio e deve essere un messaggio <xref:System.ServiceModel.Channels.Message>, un tipo derivato dal flusso <xref:System.IO.Stream> oppure un'implementazione dell'interfaccia <xref:System.Xml.Serialization.IXmlSerializable>.Definire un valore restituito di un'operazione equivale a definire un parametro di output.  
  
 Alcune funzionalità di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], ad esempio la messaggistica affidabile, le transazioni e la protezione a livello di messaggio SOAP, utilizzano la modalità di trasferimento con memorizzazione nel buffer.L'utilizzo di queste funzionalità può ridurre o eliminare del tutto i vantaggi in termini di prestazioni ottenuti mediante i flussi.Per proteggere un trasporto con flusso, utilizzare soltanto la protezione a livello di trasporto oppure utilizzare la protezione a livello di trasporto insieme a una protezione a livello di messaggio di sola autenticazione.  
  
 Le intestazioni SOAP vengono sempre memorizzate nel buffer, anche quando si utilizza la modalità di trasferimento con flusso.Le intestazioni di un messaggio non devono superare la quota di trasporto indicata da `MaxBufferSize`.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] questa impostazione, vedere [Quote dei trasporti](../../../../docs/framework/wcf/feature-details/transport-quotas.md).  
  
## Differenze tra trasferimenti con memorizzazione nel buffer e con flusso  
 Il passaggio dalla modalità di trasferimento con memorizzazione nel buffer alla modalità di trasferimento con flusso comporta la modifica della forma del canale nativo dei trasporti TCP e pipe con nome.Per i trasferimenti con memorizzazione nel buffer, la forma del canale nativo è <xref:System.ServiceModel.Channels.IDuplexSessionChannel>.Per i trasferimenti con flusso, i canali nativi sono <xref:System.ServiceModel.Channels.IRequestChannel> e <xref:System.ServiceModel.Channels.IReplyChannel>.La modifica della modalità di trasferimento di un'applicazione esistente che utilizza questi trasporti in modo diretto \(ovvero non tramite un contratto di servizio\) richiede la modifica della forma del canale previsto di channel factory e listener.  
  
## Vedere anche  
 [Procedura: attivare il flusso](../../../../docs/framework/wcf/feature-details/how-to-enable-streaming.md)