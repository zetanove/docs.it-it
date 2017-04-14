---
title: "&lt;ws2007FederationHttpBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9af4ec79-cdef-457e-9dca-09d5eb821594
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# &lt;ws2007FederationHttpBinding&gt;
Associazione protetta e interoperabile che deriva da [\<wsFederationHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md) e supporta la sicurezza federata.  
  
## Sintassi  
  
```  
  
<ws2007FederationHttpBinding>  
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
        textEncoding="UnicodeFffeTextEncoding/Utf16TextEncoding/Utf8TextEncoding"  
        transactionFlow="Boolean"  
        useDefaultWebProxy="Boolean">  
        <security mode="None/Message/TransportWithMessageCredential">  
           <message negotiateServiceCredential="Boolean"  
                algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
                issuedTokenType="string"  
                issuedKeyType="SymmetricKey/PublicKey"  
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
</ws2007FederationHttpBinding>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`bypassProxyOnLocal`|Valore che indica se ignorare il server proxy per indirizzi locali.  Il valore predefinito è `false`.|  
|`closeTimeout`|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di chiusura.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:01:00.|  
|`hostnameComparisonMode`|Specifica la modalità di confronto del nome host HTTP usata per analizzare gli URI.  L'attributo è di tipo <xref:System.ServiceModel.HostnameComparisonMode>, che indica se il nome host viene usato per raggiungere il servizio in caso di corrispondenza nell'URI.  Il valore predefinito è <xref:System.ServiceModel.HostnameComparisonMode.StrongWildcard>, che ignora il nome host nella corrispondenza.|  
|`maxBufferPoolSize`|Dimensione massima del pool di buffer dell'associazione.  Il valore predefinito è 524.288 byte \(512 \* 1024\).  Molte parti di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] usano buffer.  La creazione e l'eliminazione dei buffer a ogni relativo uso sono operazioni onerose, analogamente a quelle di Garbage Collection dei buffer.  Quando si usa un pool di buffer è possibile prelevare un buffer dal pool, usarlo e, al termine delle operazioni, riporlo nel pool.  In questo modo è possibile evitare il sovraccarico dovuto alla creazione e all'eliminazione dei buffer.|  
|`maxReceivedMessageSize`|Dimensione massima del messaggio, incluse le intestazioni, che può essere ricevuto in un canale configurato con questa associazione.  Il mittente di un messaggio che supera questo limite riceverà un errore SOAP.  Il destinatario elimina il messaggio e crea una voce dell'evento nel registro di traccia.  Il valore predefinito è 65536.|  
|`messageEncoding`|Definisce il codificatore usato per codificare il messaggio.  Di seguito vengono elencati i valori validi:<br /><br /> -   Text: usa un codificatore di messaggi di testo.<br />-   Mtom: usa un codificatore Message Transmission Organization Mechanism 1.0 \(MTOM\).<br /><br /> L'impostazione predefinita è Text.<br /><br /> L'attributo è di tipo <xref:System.ServiceModel.WSMessageEncoding>.|  
|`name`|Nome della configurazione dell'associazione.  Questo valore deve essere univoco perché viene usato per identificare l'associazione.  A partire da [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)], non è necessario che le associazioni e i comportamenti dispongano di un nome.  Per altre informazioni sulla configurazione predefinita e le associazioni e i comportamenti senza nome, vedere [Configurazione semplificata](../../../../../docs/framework/wcf/simplified-configuration.md) e [Configurazione semplificata per servizi WCF](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).|  
|`openTimeout`|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di apertura.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:01:00.|  
|`privactyNoticeAt`|URI presso cui si trova l'informativa sulla privacy.|  
|`privactyNoticeVersion`|Versione dell'informativa sulla privacy corrente.|  
|`proxyAddress`|URI che specifica l'indirizzo del proxy HTTP.  Se `useDefaultWebProxy` è `true`, questa impostazione deve essere `null`.  Il valore predefinito è `null`.|  
|`receiveTimeout`|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di ricezione.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:10:00.|  
|`sendTimeout`|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di invio.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:01:00.|  
|`textEncoding`|Imposta la codifica del set di caratteri da usare per l'emissione dei messaggi nell'associazione.  Di seguito vengono elencati i valori validi:<br /><br /> -   BigEndianUnicode: codifica Unicode BigEndian.<br />-   Unicode: codifica a 16 bit.<br />-   UTF8: codifica a 8 bit.<br /><br /> L'impostazione predefinita è UTF8.  L'attributo è di tipo <xref:System.Text.Encoding>.|  
|`transactionFlow`|Valore che specifica se l'associazione supporta il flusso di WS\-Transactions.  Il valore predefinito è `false`.|  
|`useDefaultWebProxy`|Valore che indica se viene usato il proxy HTTP di sistema configurato automaticamente.  L'indirizzo proxy deve essere `null`, ovvero non deve essere impostato, se l'attributo è `true`.  Il valore predefinito è `true`.|  
  
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
 La federazione è la possibilità di condividere le identità di autenticazione e di autorizzazione fra più aziende o domini trust.  Per il mapping della rappresentazione dell'identità da un dominio trust a un altro, viene usato il protocollo WS\-Trust.  L'associazione HTTP federata supporta la sicurezza SOAP nonché una sicurezza a modalità mista, ma non supporta la sicurezza del trasporto.  I servizi configurati con questa associazione devono usare il trasporto HTTP.  [!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)] [\<wsFederationHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md).  
  
## Esempio  
  
```  
<configuration>  
<system.ServiceModel>  
<bindings>  
<ws2007FederationHttpBinding>  
    <binding   
        bypassProxyOnLocal="false"  
        transactionFlow="false"  
        hostNameComparisonMode="WeakWildcard"  
        maxReceivedMessageSize="1000"  
        messageEncoding="Mtom"   
        proxyAddress="http://www.contoso.com"   
        textEncoding="Utf16TextEncoding"  
        useDefaultWebProxy="false">  
        <reliableSession ordered="false"  
            inactivityTimeout="00:02:00" enabled="true" />  
        <security mode="None">  
           <message negotiateServiceCredential="false"  
                algorithmSuite="Aes128"  
                issuedTokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1"   
                issuedKeyType="PublicKey">  
               <issuer address="http://localhost/Sts" />  
           </message>  
        </security>  
    </binding>  
</ws2007FederationBinding>  
</bindings>  
</system.ServiceModel>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.WS2007FederationHttpBinding>   
 <xref:System.ServiceModel.Configuration.WS2007FederationHttpBindingElement>   
 [\<wsFederationHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<associazione\>](../../../../../docs/framework/misc/binding.md)