---
title: "Programmazione delle funzionalit&#224; di sicurezza di WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "sicurezza del messaggio [WCF], cenni preliminari sulla programmazione"
ms.assetid: 739ec222-4eda-4cc9-a470-67e64a7a3f10
caps.latest.revision: 25
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 25
---
# Programmazione delle funzionalit&#224; di sicurezza di WCF
Questo argomento descrive le attività di programmazione fondamentali utilizzate per creare un'applicazione [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] protetta.In particolare, questo argomento tratta le funzionalità di autenticazione, riservatezza e integrità, complessivamente note come *sicurezza di trasferimento*.Questo argomento non descrive l'autorizzazione \(ovvero il controllo dell'accesso a risorse o servizi\). Per ottenere informazioni in merito, vedere [Autorizzazione](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md).  
  
> [!NOTE]
>  Per un'introduzione ai concetti di sicurezza, in particolare quelli correlati a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vedere il set di modelli ed esercitazioni pratiche disponibili in MSDN nella pagina relativa a [scenari, modelli e istruzioni di implementazione per Web Services Enhancements \(WSE\) 3.0](http://go.microsoft.com/fwlink/?LinkID=88250) \(il contenuto potrebbe essere in inglese\).  
  
 La programmazione delle funzionalità di sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si basa su tre passaggi: impostazione della modalità di sicurezza, impostazione di un tipo di credenziale client e impostazione dei valori di credenziale.Questi passaggi possono essere eseguiti in codice o in configurazione.  
  
## Impostazione della modalità di sicurezza  
 Di seguito vengono descritti i passaggi generali per programmare la modalità di sicurezza in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
1.  Scegliere fra le associazioni predefinite un'associazione appropriata ai requisiti dell'applicazione.Per un elenco delle associazioni disponibili, vedere [Associazioni fornite dal sistema](../../../../docs/framework/wcf/system-provided-bindings.md).Per impostazione predefinita, quasi tutte le associazioni presentano un meccanismo di sicurezza abilitato.L'unica eccezione è la classe <xref:System.ServiceModel.BasicHttpBinding>, che in configurazione è rappresentata dall'[\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md).  
  
     L'associazione scelta determina il trasporto.Ad esempio, l'associazione <xref:System.ServiceModel.WSHttpBinding> utilizza il protocollo HTTP come trasporto, mentre l'associazione <xref:System.ServiceModel.NetTcpBinding> utilizza il trasporto TCP.  
  
2.  Selezionare per l'associazione una delle modalità di sicurezza.Si noti che l'insieme delle modalità fra cui è possibile scegliere dipende dall'associazione scelta.Ad esempio, l'associazione <xref:System.ServiceModel.WSDualHttpBinding> non consente di scegliere la sicurezza a livello di trasporto.Analogamente, né l'associazione <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> né l'associazione <xref:System.ServiceModel.NetNamedPipeBinding> consentono di scegliere la sicurezza a livello di messaggio.  
  
     Sono disponibili tre opzioni:  
  
    1.  `Transport`  
  
         La sicurezza a livello di trasporto dipende dal meccanismo utilizzato dall'associazione scelta.Ad esempio, se si utilizza l'associazione `WSHttpBinding`, il meccanismo di sicurezza è Secure Sockets Layer \(SSL\), che peraltro è anche il meccanismo del protocollo HTTPS.In generale, il vantaggio principale della sicurezza a livello di trasporto è che offre una buona velocità effettiva indipendentemente dal trasporto utilizzato.Tuttavia, tale tipo di sicurezza presenta due limiti. Anzitutto, il meccanismo di trasporto impone il tipo di credenziale utilizzato per autenticare un utente.Di fatto ciò rappresenta uno svantaggio solo se un servizio deve garantire l'interoperabilità con altri servizi che richiedono vari tipi di credenziali.Inoltre, poiché la sicurezza non viene applicata a livello di messaggio, la sicurezza viene implementata in modo hop\-by\-hop anziché end\-to\-end.Questo secondo limite rappresenta un problema solo se il percorso dei messaggi fra client e servizio prevede intermediari.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] quale trasporto utilizzare, vedere [Scelta di un trasporto](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] utilizzo della sicurezza a livello di trasporto, vedere [Panoramica sulla sicurezza del trasporto](../../../../docs/framework/wcf/feature-details/transport-security-overview.md).  
  
    2.  `Message`  
  
         Nella sicurezza a livello di messaggio, ogni messaggio contiene le intestazioni e i dati necessari a garantire la sicurezza del messaggio.Poiché la composizione delle intestazioni è variabile, è possibile includere qualsiasi numero di credenziali.Ciò risulta essere un fattore rilevante se occorre interoperare con altri servizi che richiedono un tipo di credenziale specifico che un meccanismo di trasporto non è in grado di fornire, oppure se il messaggio deve essere utilizzato in più servizi, ognuno avente un requisito specifico di tipo di credenziale.  
  
         [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Protezione dei messaggi](../../../../docs/framework/wcf/feature-details/message-security-in-wcf.md).  
  
    3.  `TransportWithMessageCredential`  
  
         Questa scelta utilizza il livello di trasporto per proteggere il trasferimento dei messaggi, ognuno dei quali contiene le credenziali dettagliate richieste dagli altri servizi.Ciò combina il vantaggio in termini di prestazioni della sicurezza a livello di trasporto con il vantaggio delle credenziali dettagliate della sicurezza a livello di messaggio.Questa opzione è disponibile per le associazioni seguenti: <xref:System.ServiceModel.BasicHttpBinding>, <xref:System.ServiceModel.WSFederationHttpBinding>, <xref:System.ServiceModel.NetPeerTcpBinding> e <xref:System.ServiceModel.WSHttpBinding>.  
  
3.  Se si decide di utilizzare la sicurezza a livello di trasporto per il protocollo HTTP \(ovvero il protocollo HTTPS\), è inoltre necessario configurare l'host con un certificato SSL e quindi abilitare il protocollo SSL su una porta.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Protezione del trasporto HTTP](../../../../docs/framework/wcf/feature-details/http-transport-security.md).  
  
4.  Se si utilizza l'associazione <xref:System.ServiceModel.WSHttpBinding> e non occorre stabilire una sessione protetta, impostare la proprietà <xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A> su `false`.  
  
     Una sessione protetta si verifica quando un client e un servizio creano un canale utilizzando una chiave simmetrica, ovvero quando sia il client sia il server utilizzano la stessa chiave per la durata della conversazione e fino alla chiusura del dialogo.  
  
## Impostazione del tipo di credenziale client  
 Selezionare un tipo di credenziale client in base alle proprie esigenze.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Selezione di un tipo di credenziale](../../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md).Sono disponibili i tipi di credenziale client seguenti:  
  
-   `Windows`  
  
-   `Certificate`  
  
-   `Digest`  
  
-   `Basic`  
  
-   `UserName`  
  
-   `NTLM`  
  
-   `IssuedToken`  
  
 L'impostazione del tipo di credenziale dipende dalla modalità impostata.Se ad esempio è stata selezionata l'associazione `wsHttpBinding` e la modalità è stata impostata sulla sicurezza a livello di messaggio, l'attributo `clientCredentialType` dell'elemento Message può essere impostato su uno dei valori seguenti: `None`, `Windows`, `UserName`, `Certificate` e `IssuedToken`, come mostrato nell'esempio di configurazione seguente.  
  
```  
<system.serviceModel>  
<bindings>  
  <wsHttpBinding>  
    <binding name="myBinding">  
      <security mode="Message"/>  
      <message clientCredentialType="Windows"/>  
    </binding>  
</bindings>  
</system.serviceModel>  
```  
  
 Oppure nel codice:  
  
 [!code-csharp[c_WsHttpService#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wshttpservice/cs/source.cs#1)]
 [!code-vb[c_WsHttpService#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wshttpservice/vb/source.vb#1)]  
  
## Impostazione dei valori di credenziale del servizio  
 Dopo aver selezionato un tipo di credenziale client è necessario impostare le credenziali effettivamente utilizzate dal servizio e dal client.Nel servizio, le credenziali vengono impostate utilizzando la classe <xref:System.ServiceModel.Description.ServiceCredentials> e restituite tramite la proprietà <xref:System.ServiceModel.ServiceHostBase.Credentials%2A> della classe <xref:System.ServiceModel.ServiceHostBase>.L'associazione utilizzata determina il tipo di credenziale del servizio, la scelta della modalità di sicurezza e il tipo di credenziale client.Nel codice seguente un certificato viene impostato come credenziale di servizio.  
  
 [!code-csharp[c_tcpService#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_tcpservice/cs/source.cs#3)]
 [!code-vb[c_tcpService#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_tcpservice/vb/source.vb#3)]  
  
## Impostazione dei valori di credenziale del client  
 Nel client, i valori di credenziale vengono impostati utilizzando la classe <xref:System.ServiceModel.Description.ClientCredentials> e restituiti tramite la proprietà <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> della classe <xref:System.ServiceModel.ClientBase%601>.Nel codice seguente un certificato viene impostato come credenziale in un client che utilizza il protocollo TCP.  
  
 [!code-csharp[c_TcpClient#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_tcpclient/cs/source.cs#1)]
 [!code-vb[c_TcpClient#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_tcpclient/vb/source.vb#1)]  
  
## Vedere anche  
 [Programmazione WCF di base](../../../../docs/framework/wcf/basic-wcf-programming.md)   
 [Scenari di sicurezza comuni](../../../../docs/framework/wcf/feature-details/common-security-scenarios.md)