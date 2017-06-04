---
title: "&lt;customBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 9da4f960-f64e-4d8a-894d-2b09eba5ce4b
caps.latest.revision: 24
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# &lt;customBinding&gt;
Fornisce il controllo completo dello stack di messaggistica per l'utente.  
  
## Sintassi  
  
```  
  
<customBinding>  
    <binding name="string"  
        closeTimeout="TimeSpan"  
        openTimeout="TimeSpan"   
        receiveTimeout="TimeSpan"  
        sendTimeout="TimeSpan"  
       <compositeDuplex clientBaseAddress="Uri"/>  
       <reliableSession acknowledgementInterval="TimeSpan"  
           advancedFlowControl="Boolean"   
           bufferedMessagesQuota="Integer"  
           inactivityTimeout="TimeSpan"  
           maxPendingChannels="Integer"  
           maxRetryCount="Integer"   
           ordered="Boolean" />  
       <pnrpPeerResolver />  
       <windowsStreamSecurity protectionLevel="None/Sign/EncryptAndSign"/>  
       <sslStreamSecurity requireClientCertificate="Boolean" />  
              <transactionFlow transactionProtocol="OleTransactions/WSAtomicTransactionOctober2004"/>  
       <security   
          defaultAlgorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
           authenticationMode="UserNameForAnonymous"  
           contextMode="Cookie"   
           defaultProtectionLevel="Sign"  
           enableKeyDerivation="false"  
           keyEntropyMode="ClientEntropy"   
                  messageProtectionOrder="SignBeforeEncryptAndEncryptSignature"   
           securityVersion="WSSecurityXXX2005">  
           <localClientSettings cacheCookies="false"  
               detectReplays="false"  
               maxCookieCachingTime="00:07:24" />  
           <localServiceSettings replayCacheSize="9"  
               maxClockSkew="00:00:03"   
               replayWindow="00:07:22.2190000" />  
       </security>  
       <binaryMessageEncoding maxReadPoolSize="Integer"  
           maxWritePoolSize="Integer"  
           maxSessionSize="Integer" />  
       <httpsTransport manualAddressing="Boolean"  
           maxMessageSize="Integer"  
           authenticationScheme="Negotiate"   
           bypassProxyOnLocal="Boolean"  
           hostNameComparisonMode="Exact"   
           mapAddressingHeadersToHttpHeaders="Boolean"   
           proxyaddress="Uri"  
           realm="String"   
           requireClientCertificate="Boolean" />  
       <peerTransport manualAddressing="false"  
          maxMessageSize="20002"  
          listenIPAddress="202.10.1.9"   
          messageAuthentication="false"  
          peerNodeAuthenticationMode="None"  
          port="1000" />  
  
<security   
      defaultAlgorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
   authenticationMode="UserNameForAnonymous"  
   bootstrapBindingConfiguration="String"  
   bootstrapBindingSectionName="String"  
   defaultProtectionLevel="None/Sign/EncryptAndSign"  
      requireDerivedKeys="Boolean"  
   securityHeaderLayout="Strict/Lax/LaxTimestampFirst/LaxTimestampLast"  
   includeTimestamp="Boolean"  
   keyEntropyMode="ClientEntropy/ServerEntropy/CombinedEntropy"   
   messageProtectionOrder="SignBeforeEncrypt/SignBeforeEncryptAndEncryptSignature/EncryptBeforeSign"   
   protectTokens="Boolean"  
   requireSecurityContextCancellation="Boolean"  
   securityVersion=" WSSecurityJan2004/WSSecurityXXX2005"  
   requireSignatureConfirmation="Boolean" >  
   <localClientSettings cacheCookies="Boolean"  
      detectReplays="Boolean"  
      replayCacheSize="Integer"  
      maxClockSkew="TimeSpan"  
      maxCookieCachingTime="TimeSpan"  
      replayWindow="TimeSpan"  
      sessionKeyRenewalInterval="TimeSpan"  
      sessionKeyRolloverInterval="TimeSpan"  
      reconnectOnTransportFailure="Boolean"  
      timestampValidityDuration="TimeSpan"  
      cookieRenewalThresholdPercentage="Integer" />  
   <localServiceSettings detectReplays="Boolean"  
      issuedCookieLifeTime="TimeSpan"  
      maxStatefulNegotiations="Integer"  
            replayCacheSize="Integer"  
      maxClockSkew="TimeSpan"   
      negotiationTimeout="TimeSpan"  
      replayWindow="TimeSpan"  
      inactivityTimeout="TimeSpan"  
      sessionKeyRenewalInterval="TimeSpan"  
      sessionKeyRolloverInterval="TimeSpan"  
      reconnectOnTransportFailure="Boolean"  
      maxConcurrentSessions="Integer"  
      timestampValidityDuration="TimeSpan" />  
   <federationParameters trustVersion="WSTrustApr2004/WSTrustFeb2005" />  
<security   
   defaultAlgorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/ Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
   authenticationMode="UserNameForAnonymous"  
   bootstrapBindingConfiguration="String"  
   bootstrapBindingSectionName="String"  
   defaultProtectionLevel="None/Sign/EncryptAndSign"  
      requireDerivedKeys="Boolean"  
   securityHeaderLayout="Strict/Lax/LaxTimestampFirst/LaxTimestampLast"  
   includeTimestamp="Boolean"  
   keyEntropyMode="ClientEntropy/ServerEntropy/CombinedEntropy"   
   messageProtectionOrder="SignBeforeEncrypt/SignBeforeEncryptAndEncryptSignature/EncryptBeforeSign"   
   protectTokens="Boolean"  
   requireSecurityContextCancellation="Boolean"  
   securityVersion=" WSSecurityJan2004/WSSecurityXXX2005"  
   requireSignatureConfirmation="Boolean" >  
   <localClientSettings cacheCookies="Boolean"  
      detectReplays="Boolean"  
      replayCacheSize="Integer"  
      maxClockSkew="TimeSpan"  
      maxCookieCachingTime="TimeSpan"  
      replayWindow="TimeSpan"  
      sessionKeyRenewalInterval="TimeSpan"  
      sessionKeyRolloverInterval="TimeSpan"  
      reconnectOnTransportFailure="Boolean"  
      timestampValidityDuration="TimeSpan"  
      cookieRenewalThresholdPercentage="Integer" />  
   <localServiceSettings detectReplays="Boolean"  
      issuedCookieLifeTime="TimeSpan"  
      maxStatefulNegotiations="Integer"  
            replayCacheSize="Integer"  
      maxClockSkew="TimeSpan"   
      negotiationTimeout="TimeSpan"  
      replayWindow="TimeSpan"  
      inactivityTimeout="TimeSpan"  
      sessionKeyRenewalInterval="TimeSpan"  
      sessionKeyRolloverInterval="TimeSpan"  
      reconnectOnTransportFailure="Boolean"  
      maxConcurrentSessions="Integer"  
      timestampValidityDuration="TimeSpan" />  
   <federationParameters trustVersion="WSTrustApr2004/WSTrustFeb2005" />  
   <GenericIssuedTokenParameters>   
      <LocalIssuerIssuedTokenParameters keyType=" SymmeticKey/PublicKey"  
        keySize="Integer"  
        tokenType="String" />  
     <IssuedTokenParametersEndpointAddress address="URI"  
        bindingConfiguration="String"  
        binding="String" />  
     <IssuedTokenClient localIssuerChannelBehaviors="String"  
        cacheIssuedTokens="Boolean"  
        maxIssuedTokenCachingTime="TimeSpan"  
        keyEntropyMode="ClientEntropy/ServerEntropy/CombinedEntropy" />  
     <IssuedTokenClientBehavior issuerAddress="String"  
        behaviorConfiguration="String" />  
     <IssuedTokenClientBehavior address="URI"  
        bindingConfiguration="String"  
        binding="String" />  
   </GenericIssuedTokenParameters>   
</security>  
</binding>  
</customBinding>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti attributi, elementi figlio ed elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|closeTimeout|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di chiusura.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:01:00.|  
|name|Stringa che contiene il nome della configurazione dell'associazione.  Questo valore è una stringa definita dall'utente che deve essere univoca in quanto funge da stringa di identificazione dell'associazione personalizzata.  A partire da [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)], non è necessario che le associazioni e i comportamenti dispongano di un nome.  Per altre informazioni sulla configurazione predefinita e le associazioni e i comportamenti senza nome, vedere [Configurazione semplificata](../../../../../docs/framework/wcf/simplified-configuration.md) e [Configurazione semplificata per servizi WCF](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).|  
|openTimeout|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di apertura.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:01:00.|  
|receiveTimeout|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di ricezione.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:01:00.|  
|sendTimeout|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di invio.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:01:00.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\< compositeDuplex \>](../../../../../docs/framework/configure-apps/file-schema/wcf/compositeduplex.md)|Specifica la messaggistica bidirezionale sull'associazione personalizzata.  Viene usato con trasporti che non consentono comunicazioni duplex a livello nativo, ad esempio, HTTP.  TCP, al contrario, consente comunicazioni duplex a livello nativo e non richiede l'uso di questo elemento di associazione affinché il servizio invii messaggi a un client.<br /><br /> Il client deve esporre un indirizzo affinché il servizio crei un contatto e stabilisca una connessione.  Questo indirizzo client è fornito dall'attributo `ClientBaseAddress`.<br /><br /> L'elemento è di tipo <xref:System.ServiceModel.Configuration.CompositeDuplexElement>.|  
|[\<resolverPeerPnrp\>](../../../../../docs/framework/configure-apps/file-schema/wcf/pnrppeerresolver.md)|Specifica un resolver dei nomi peer PNRP \(Peer Name Resolution Protocol\).  L'elemento è di tipo <xref:System.ServiceModel.Configuration.PnrpPeerResolverElement>.|  
|[\<sessioneAttendibile\>](../../../../../docs/framework/configure-apps/file-schema/wcf/reliablesession.md)|Specifica l'impostazione per WS\-Reliable Messaging.  Quando questo elemento viene aggiunto a un'associazione personalizzata, il canale risultante può supportare assicurazioni di recapito una volta esatta.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.ReliableSessionElement>.|  
|[\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)|Specifica le opzioni di sicurezza per l'associazione personalizzata.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.SecurityElement>.|  
|[\<sslStreamSecurity\>](../../../../../docs/framework/configure-apps/file-schema/wcf/sslstreamsecurity.md)|Specifica le impostazioni di sicurezza per l'associazione del flusso SSL.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.SslStreamSecurityElement>.|  
|[\<transactionFlow\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transactionflow.md)|Specifica che l'associazione supporta il flusso delle transazioni e il protocollo che deve essere usato dall'attributo `transactionProtocol`.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.TransactionFlowElement>.|  
|[\<sicurezzaFlussoWindows\>](../../../../../docs/framework/configure-apps/file-schema/wcf/windowsstreamsecurity.md)|Specifica le opzioni di sicurezza del flusso per un'associazione personalizzata.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.WindowsStreamSecurityElement>.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|associazioni|Contiene tutte le associazioni per le applicazioni Windows Communication Foundation \(WCF\).|  
  
## Note  
 Le associazioni personalizzate forniscono il controllo completo dello stack dei messaggi WCF.  È possibile creare associazioni speciali su misura aggiungendo gli elementi di configurazione per le entità specifiche.  Ad esempio, l'utente può combinare la sezione `httpsTransport`, la sezione `reliableSession` e la sezione `security` per creare un'associazione affidabile e protetto basata su HTTPS.  
  
 Un'associazione singola definisce lo stack dei messaggi specificando gli elementi di configurazione per gli elementi dello stack nell'ordine in cui vengono visualizzati nello stack.  Ogni elemento definisce e configura un elemento dello stack.  Deve esistere un solo elemento di trasporto in ogni associazione personalizzata.  Senza questo elemento, lo stack dei messaggi è incompleto.  
  
 L'ordine in cui gli elementi vengono visualizzati nello stack è importante, perché è l'ordine in cui le operazioni vengono applicate al messaggio.  L'ordine consigliato per gli elementi dello stack è il seguente:  
  
1.  Transazioni \(facoltativo\)  
  
2.  Messaggistica affidabile \(facoltativo\)  
  
3.  Sicurezza \(facoltativo\)  
  
4.  Trasporto  
  
5.  Codificatore \(facoltativo\)  
  
 Usare un'associazione personalizzata quando una delle associazioni fornite dal sistema non soddisfa i requisiti del servizio.  Un'associazione personalizzata potrebbe essere usata, ad esempio, per abilitare l'uso di un nuovo trasporto o di un nuovo codificatore a un endpoint del servizio.  
  
 Un'associazione personalizzata viene costruita usando uno dei <xref:System.ServiceModel.Channels.CustomBinding.%23ctor%2A> da una raccolta di elementi di associazione in uno stack in un ordine specifico:  
  
-   All'inizio si trova una classe <xref:System.ServiceModel.Channels.TransactionFlowBindingElement> facoltativa che consente la propagazione delle transazioni.  
  
-   Quindi una classe <xref:System.ServiceModel.Channels.ReliableSessionBindingElement> facoltativa che fornisce una sessione e un meccanismo di ordinamento come definito nella specifica WS\-ReliableMessaging.  Questa nozione di sessione può attraversare SOAP e può trasportare intermediari.  
  
-   Segue un elemento di associazione di sicurezza facoltativo che fornisce funzionalità di sicurezza quali, ad esempio, autorizzazione, autenticazione, protezione e riservatezza.  Gli elementi di associazione di sicurezza seguenti sono forniti da [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)]:  
  
    -   <xref:System.ServiceModel.Channels.SecurityBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>  
  
-   Seguono i modelli di messaggio facoltativi specificati dagli elementi di associazione:  
  
-   <xref:System.ServiceModel.Channels.CompositeDuplexBindingElement>  
  
-   Quindi gli elementi di associazione di trasporto facoltativi di aggiornamenti\/helper:  
  
    -   <xref:System.ServiceModel.Channels.PnrpPeerResolverBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>  
  
-   Segue quindi un elemento di associazione obbligatorio di codifica dei messaggi.  È possibile usare un trasporto proprio o una delle associazioni di codifica del messaggio seguenti:  
  
    -   <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>  
  
-   Segue infine un elemento di trasporto obbligatorio.  È possibile usare un trasporto proprio o uno degli elementi di associazione di trasporto forniti da [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)]:  
  
    -   <xref:System.ServiceModel.Channels.TcpTransportBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.HttpTransportBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.MsmqTransportBindingElement>  
  
    -   <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBindingElement>  
  
    -   <xref:System.ServiceModel.Channels.PeerTransportBindingElement>  
  
 Nella tabella seguente viene fornito un riepilogo delle opzioni per ogni livello.  
  
|Livello|Opzioni|Obbligatorio|  
|-------------|-------------|------------------|  
|Flusso transazioni|<xref:System.ServiceModel.Channels.TransactionFlowBindingElement>|No|  
|Affidabilità|<xref:System.ServiceModel.Channels.ReliableSessionBindingElement>|No|  
|Sicurezza|Simmetrico, asimmetrico, livello di trasporto|No|  
|Cambio di forma|<xref:System.ServiceModel.Channels.CompositeDuplexBindingElement>|No|  
|Aggiornamenti del trasporto|Flusso SSL, flusso di Windows, resolver Peer|No|  
|Codifica|Testo, binario, MTOM, personalizzata|Sì|  
|Trasporto|TCP, named pipe, HTTP, HTTPS, versioni di MSMQ, personalizzato|Sì|  
  
 È inoltre possibile definire elementi di associazione personalizzati e inserirli tra i livelli appena elencati.  
  
 Per una discussione sull'utilizzo di un'associazione personalizzata per modificare un'associazione fornita dal sistema, vedere [Procedura: personalizzare un'associazione fornita dal sistema](../../../../../docs/framework/wcf/extending/how-to-customize-a-system-provided-binding.md).  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.Binding>   
 <xref:System.ServiceModel.Channels.BindingElement>   
 <xref:System.ServiceModel.Configuration.BindingsSection>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [\<associazione\>](../../../../../docs/framework/misc/binding.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [customBinding Element](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)