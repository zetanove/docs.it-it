---
title: "&lt;wsFederationHttpBinding&gt; | Microsoft Docs"
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
  - "elemento wsFederationBinding"
ms.assetid: 9c3312b4-2137-4e71-bf3f-de1cf8e9be79
caps.latest.revision: 28
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# &lt;wsFederationHttpBinding&gt;
Definisce un'associazione che supporta WS\-Federation.  
  
## Sintassi  
  
```  
  
<wsFederationHttpBinding>  
    <binding   
        bypassProxyOnLocal="Boolean"  
        closeTimeout="TimeSpan"   
        hostNameComparisonMode="StrongWildcard/Exact/WeakWildcard"  
        maxBufferPoolSize="integer"  
        maxReceivedMessageSize="integer"  
        messageEncoding="Text/Mtom"   
                name="string"  
        openTimeout="TimeSpan"   
        privacyNoticeAt="Uri"  
        privacyNoticeVersion="Integer"  
        proxyAddress="Uri"   
        receiveTimeout="TimeSpan"  
        sendTimeout="TimeSpan"  
        textEncoding="UnicodeFffeTextEncoding/Utf16TextEncoding/ Utf8TextEncoding"  
        transactionFlow="Boolean"  
        useDefaultWebProxy="Boolean">  
        <security mode="None/Message/TransportWithMessageCredential">  
         <message   
            algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
            issuedTokenType="string"   
            issuedKeyType="SymmetricKey/PublicKey"  
            negotiateServiceCredential="Boolean" >  
            <claimTypeRequirements>  
               <add claimType="URI"  
                    isOptional="Boolean" />  
            </claimTypeRequirements>  
                        <issuer address="Uri" >  
               <headers>  
                  <add name="String"  
                       namespace="String" />  
                          </headers>  
                              <identity>  
                                 <certificate encodedValue="String"/>  
                                <certificateReference findValue="String"   
                                 isChainIncluded="Boolean"  
                            storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"  
                                  storeLocation="LocalMachine/CurrentUser"  
                                   X509FindType=System.Security.Cryptography.X509certificates.X509findtype/>  
                                   <dns value="String"/>  
                                <rsa value="String"/>  
                                <servicePrincipalName value="String"/>  
                                <usePrincipalName value="String"/>  
                              </identity>  
                        </issuer>  
                        <issuerMetadata address=String" >  
               <headers>  
                  <add name="String"  
                       namespace="String" />  
               </headers>  
               <identity>  
                  <certificate encodedValue="String"/>  
                  <certificateReference findValue="String"   
                     isChainIncluded="Boolean"  
                     storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"  
                     storeLocation="LocalMachine/CurrentUser"  
                     x509FindType=System.Security.Cryptography.X509certificates.X509findtype/>  
                  <dns value="String"/>  
                  <rsa value="String"/>  
                  <servicePrincipalName value="String"/>  
                  <usePrincipalName value="String"/>  
               </identity>  
                        </issuerMetadata>  
            <tokenRequestParameters>  
               <xmlElement>  
               </xmlElement>  
            </tokenRequestParameters>  
           </message>  
        </security>  
        <reliableSession ordered="Boolean"  
           inactivityTimeout="TimeSpan"  
           enabled="Boolean" />  
       <readerQuotas   
            maxArrayLength="Integer"  
            maxBytesPerRead="Integer"  
            maxDepth="Integer"   
            maxNameTableCharCount="Integer"           
            maxStringContentLength="Integer" />  
    </binding>  
</wsFederationBinding>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|bypassProxyOnLocal|Valore booleano che indica se ignorare il server proxy per indirizzi locali.  Il valore predefinito è `false`.|  
|closeTimeout|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di chiusura.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:01:00.|  
|hostnameComparisonMode|Specifica la modalità di confronto del nome host HTTP usata per analizzare gli URI.  L'attributo è di tipo <xref:System.ServiceModel.HostnameComparisonMode>, che indica se il nome host viene usato per raggiungere il servizio in caso di corrispondenza nell'URI.  Il valore predefinito è <xref:System.ServiceModel.HostnameComparisonMode.StrongWildcard>, che ignora il nome host nella corrispondenza.|  
|maxBufferPoolSize|Numero intero che specifica la dimensione del pool di buffer massima per questa associazione.  Il valore predefinito è 524.288 byte \(512 \* 1024\).  Molte parti di Windows Communication Foundation \(WCF\) usano buffer.  La creazione e l'eliminazione dei buffer a ogni relativo uso sono operazioni onerose, analogamente a quelle di Garbage Collection dei buffer.  Quando si usa un pool di buffer è possibile prelevare un buffer dal pool, usarlo e, al termine delle operazioni, riporlo nel pool.  In questo modo è possibile evitare il sovraccarico dovuto alla creazione e all'eliminazione dei buffer.|  
|maxReceivedMessageSize|Integer positivo che specifica la dimensione massima del messaggio, incluse le intestazioni, che è possibile ricevere su un canale configurato con questa associazione.  Il mittente di un messaggio che supera questo limite riceverà un errore SOAP.  Il destinatario elimina il messaggio e crea una voce dell'evento nel registro di traccia.  Il valore predefinito è 65536.|  
|messageEncoding|Definisce il codificatore usato per codificare il messaggio.  Di seguito vengono elencati i valori validi:<br /><br /> -   Text: usa un codificatore di messaggi di testo.<br />-   Mtom: usa un codificatore Message Transmission Organization Mechanism 1.0 \(MTOM\).<br /><br /> L'impostazione predefinita è Text.<br /><br /> L'attributo è di tipo <xref:System.ServiceModel.WSMessageEncoding>.|  
|name|Stringa che contiene il nome della configurazione dell'associazione.  Questo valore deve essere univoco perché viene usato per identificare l'associazione.  A partire da [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)], non è necessario che le associazioni e i comportamenti dispongano di un nome.  Per altre informazioni sulla configurazione predefinita e le associazioni e i comportamenti senza nome, vedere [Configurazione semplificata](../../../../../docs/framework/wcf/simplified-configuration.md) e [Configurazione semplificata per servizi WCF](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).|  
|openTimeout|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di apertura.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:01:00.|  
|privactyNoticeAt|Stringa che specifica l'URI presso cui è disponibile l'informativa sulla privacy.|  
|privactyNoticeVersion|Numero intero che specifica la versione dell'informativa sulla privacy corrente.|  
|proxyAddress|URI che specifica l'indirizzo del proxy HTTP.  Se `useDefaultWebProxy` è `true`, questa impostazione deve essere `null`.  Il valore predefinito è `null`.|  
|receiveTimeout|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di ricezione.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:10:00.|  
|sendTimeout|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di invio.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:01:00.|  
|textEncoding|Imposta la codifica del set di caratteri da usare per l'emissione dei messaggi nell'associazione.  Di seguito vengono elencati i valori validi:<br /><br /> -   BigEndianUnicode: codifica Unicode BigEndian.<br />-   Unicode: codifica a 16 bit.<br />-   UTF8: codifica a 8 bit<br /><br /> L'impostazione predefinita è UTF8.  L'attributo è di tipo <xref:System.Text.Encoding>.|  
|transactionFlow|Valore booleano che specifica se l'associazione supporta la propagazione di WS\-Transactions.  Il valore predefinito è `false`.|  
|useDefaultWebProxy|Valore booleano che indica se viene usato il proxy HTTP di sistema configurato automaticamente.  L'indirizzo proxy deve essere `null`, ovvero non deve essere impostato, se l'attributo è `true`.  Il valore predefinito è `true`.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wsfederationhttpbinding.md)|Definisce le impostazioni di sicurezza per il messaggio.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.WSFederationHttpSecurityElement>.|  
|[\<quoteReader\>](../Topic/%3CreaderQuotas%3E.md)|Definisce i vincoli sulla complessità dei messaggi SOAP che possono essere elaborati dagli endpoint configurati con questa associazione.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>.|  
|[reliableSession](http://msdn.microsoft.com/it-it/9c93818a-7dfa-43d5-b3a1-1aafccf3a00b)|Specifica se vengono stabilite sessioni affidabili tra endpoint del canale.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<associazioni\>](../../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)|Questo elemento contiene una raccolta di associazioni standard e personalizzate.|  
  
## Note  
 La federazione è la possibilità di condividere le identità di autenticazione e di autorizzazione fra più sistemi.  Queste identità possono fare riferimento agli utenti o ai computer.  Il protocollo HTTP federato supporta la sicurezza SOAP e una sicurezza a modalità mista, ma non supporta l'uso esclusivo della sicurezza del trasporto.  Questa associazione consente al sistema [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] di supportare il protocollo WS\-Federation.  I servizi configurati con questa associazione devono usare il trasporto HTTP.  
  
 Le associazioni sono costituite da uno stack di elementi di associazione.  Lo stack di elementi di associazione in  
  
 `wsFederationHttpBinding` è uguale a quello contenuto in `wsHttpBinding`  
  
 quando l'impostazione di [\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wsfederationhttpbinding.md) corrisponde al valore predefinito di <xref:System.ServiceModel.WSFederationHttpSecurityMode>.  
  
 `wsFederationHttpBinding` controlla i dettagli delle impostazioni di sicurezza dei messaggi in [\<message\>](../../../../../docs/framework/configure-apps/file-schema/wcf/message-element-of-wsfederationhttpbinding.md).  Poiché la sicurezza usata dall'associazione non può più essere modificata dopo la creazione dell'associazione, l'elemento [\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wsfederationhttpbinding.md) fornisce soltanto l'autorizzazione di accesso.  
  
 `wsFederationHttpBinding` fornisce inoltre un attributo privactyNoticeAt per impostare e recuperare l'URI in corrispondenza del quale si trova l'informativa sulla privacy.  
  
 La sicurezza del criterio è particolarmente importante negli scenari della federazione.  Il consiglio è usare qualche forma di sicurezza, ad esempio HTTPS, per proteggere il criterio dagli utenti malintenzionati.  
  
 In scenari della federazione che usano questa associazione, il criterio del servizio contiene potenzialmente importanti informazioni quali la chiave da usare per crittografare il token emesso \(SAML\), il tipo di attestazioni in cui inserire il token e così via.  Se questo criterio viene manomesso, un pirata informatico potrebbe individuare la chiave del token emesso per eseguire ulteriori manomissioni, divulgare informazioni e altri comportamenti dannosi.  Per aiutare a impedire questa possibilità, il criterio deve essere ottenuto in modo protetto dal servizio, ad esempio usando HTTPS.  
  
 Per altre informazioni su questa associazione, vedere [Procedura: creare una classe WSFederationHttpBinding](../../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md).  
  
## Esempio  
  
```  
<configuration>  
<system.ServiceModel>  
<bindings>  
<wsFederationHttpBinding>  
    <binding   
        bypassProxyOnLocal="false"  
        transactionFlow="false"  
        hostNameComparisonMode="WeakWildcard"  
        maxReceivedMessageSize="1000"  
        messageEncoding="Mtom"   
        proxyAddress="http://foo/bar"   
        textEncoding="Utf16TextEncoding"  
        useDefaultWebProxy="false">  
        <reliableSession ordered="false"  
            inactivityTimeout="00:02:00" enabled="true" />  
        <security mode="None">  
           <message negotiateServiceCredential="false"  
                algorithmSuite="Aes128"  
                issuedTokenType="saml"   
                issuedKeyType="PublicKey">  
               <issuer address="http://localhost/Sts" />  
           </message>  
        </security>  
    </binding>  
</wsFederationBinding>  
</bindings>  
</system.ServiceModel>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.WSFederationHttpBinding>   
 <xref:System.ServiceModel.Configuration.WSFederationHttpBindingElement>   
 [Procedura: creare una classe WSFederationHttpBinding](../../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<associazione\>](../../../../../docs/framework/misc/binding.md)