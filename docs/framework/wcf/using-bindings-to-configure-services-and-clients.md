---
title: "Uso di associazioni per configurare servizi e client | Microsoft Docs"
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
  - "associazione [WCF], utilizzo"
ms.assetid: c39479c3-0766-4a17-ba4c-97a74607f392
caps.latest.revision: 33
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 33
---
# Uso di associazioni per configurare servizi e client
Le associazioni sono oggetti che specificano i dettagli di comunicazione necessari per connettersi a un endpoint.  In particolare, le associazioni contengono le informazioni di configurazione usate per creare il client o il runtime del servizio definendo le specifiche dei trasporti, i formati di trasmissione \(codifica del messaggio\) e i protocolli da usare per il relativo endpoint o canale client.  Per creare un servizio [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] funzionante, ogni endpoint nel servizio richiede un'associazione.  In questo argomento viene illustrato cosa sono le associazioni, come vengono definite e come viene specificata una particolare associazione per un endpoint.  
  
## Elementi definiti da un'associazione  
 Le informazioni presenti in un'associazione possono essere molto semplici o molto complesse.  L'associazione più semplice specifica solo il protocollo di trasporto \(ad esempio HTTP\) che deve essere usato per connettersi all'endpoint.  In termini più generali, le informazioni contenute in un'associazione sulla modalità di connessione a un endpoint rientrano in una delle categorie della tabella seguente.  
  
 Protocolli  
 Determina il meccanismo di sicurezza usato: la funzionalità di messaggistica affidabile o le impostazioni di flusso del contesto della transazione.  
  
 Trasporto  
 Determina il protocollo di trasporto sottostante da usare \(ad esempio, TCP o HTTP\).  
  
 Codifica  
 Determina la codifica del messaggio, ad esempio, testo\/XML, binaria o MTOM \(Message Transmission Optimization Mechanism\), che determina il modo in cui i messaggi vengono rappresentati come flussi di byte durante la trasmissione.  
  
## Associazioni fornite dal sistema  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] include un set di associazioni fornite dal sistema progettate per soddisfare la maggior parte dei requisiti e degli scenari delle applicazioni.  Le classi seguenti rappresentano alcuni esempi di associazioni fornite dal sistema:  
  
-   <xref:System.ServiceModel.BasicHttpBinding>: associazione di protocollo HTTP adatta alla connessione a servizi Web conformi alla specifica WS\-I Basic Profile 1.1 \(ad esempio, servizi basati sui servizi Web ASP.NET \[ASMX\]\).  
  
-   <xref:System.ServiceModel.WsHttpBinding>: associazione di protocollo HTTP adatta alla connessione agli endpoint conformi ai protocolli e alle specifiche dei servizi Web.  
  
-   <xref:System.ServiceModel.NetNamedPipeBinding>: usa la codifica binaria .NET e le tecnologie di frame insieme al trasporto delle named pipe di Windows per la connessione ad altri endpoint [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] sullo stesso computer.  
  
-   <xref:System.ServiceModel.NetMsmqBinding>: usa la codifica binaria .NET e tecnologie di frame insieme al servizio di accodamento messaggi \(MSMQ\) per creare connessioni dei messaggi in coda con gli altri endpoint [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
 Per un elenco completo, con le descrizioni, di tutte le associazioni fornite dal sistema, vedere [Associazioni fornite dal sistema](../../../docs/framework/wcf/system-provided-bindings.md).  
  
## Associazioni personalizzate  
 Se la raccolta di associazioni fornite dal sistema non include la corretta combinazione di funzionalità richiesta da un'applicazione di servizio, è possibile creare un'associazione <xref:System.ServiceModel.Channels.CustomBinding>.  [!INCLUDE[crabout](../../../includes/crabout-md.md)]gli elementi di un'associazione <xref:System.ServiceModel.Channels.CustomBinding>, vedere [\<customBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) e [Associazioni personalizzate](../../../docs/framework/wcf/extending/custom-bindings.md).  
  
## Uso di associazioni  
 L'utilizzo di associazioni comporta due passaggi di base:  
  
1.  Selezionare o definire un'associazione.  Il metodo più facile consiste nello scegliere una delle associazioni fornite dal sistema e usarla con le relative impostazioni predefinite.  È inoltre possibile scegliere un'associazione fornita dal sistema e reimpostarne i valori delle proprietà per adattarli ai propri requisiti.  In alternativa, è possibile creare un'associazione personalizzata e impostare ogni proprietà in base alle esigenze.  
  
2.  Creare un endpoint che usa questa associazione.  
  
## Codice e configurazione  
 È possibile definire o configurare associazioni tramite il codice o la configurazione.  Questi due approcci sono indipendenti dal tipo di associazione usato, ad esempio, se si usa un'associazione fornita dal sistema o <xref:System.ServiceModel.Channels.CustomBinding>.  In generale, l'uso del codice garantisce il controllo completo sulla definizione di un'associazione durante la compilazione.  La configurazione, d'altra parte, consente a un amministratore di sistema o all'utente di un servizio o di un client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] di modificare i parametri delle associazioni.  Questa flessibilità è spesso utile in quando non è possibile prevedere in alcun modo i requisiti specifici del computer e le condizioni della rete in cui deve essere distribuita un'applicazione [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  Se le informazioni sull'associazione \(e l'indirizzo\) vengono separate dal codice, gli amministratori possono modificare i dettagli dell'associazione senza dover compilare o distribuire nuovamente l'applicazione.  Si noti che se l'associazione viene definita nel codice, sovrascrive qualsiasi definizione basata sulla configurazione creata nel file di configurazione.  Per esempi di questi approcci, vedere gli argomenti seguenti:  
  
-   In  [Procedura: ospitare un servizio WCF in un'applicazione gestita](../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md) viene fornito un esempio della creazione di un'associazione nel codice.  
  
-   In  [Procedura: descrizione della configurazione di un client](../../../docs/framework/wcf/how-to-configure-a-basic-wcf-client.md) viene fornito un esempio della creazione di un client mediante la configurazione.  
  
## Vedere anche  
 [Cenni preliminari sulla creazione di endpoint](../../../docs/framework/wcf/endpoint-creation-overview.md)   
 [Procedura: specificare un'associazione al servizio in configurazione](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md)   
 [Procedura: specificare un'associazione al servizio in codice](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-code.md)   
 [Procedura: specificare un'associazione client nella configurazione](../../../docs/framework/wcf/how-to-specify-a-client-binding-in-configuration.md)   
 [Procedura: specificare un'associazione al client in codice](../../../docs/framework/wcf/how-to-specify-a-client-binding-in-code.md)