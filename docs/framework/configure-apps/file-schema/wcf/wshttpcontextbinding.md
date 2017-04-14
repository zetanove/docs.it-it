---
title: "&lt;wsHttpContextBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1e40b5c9-0df2-4d66-afc5-a99d0e4ae7a4
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# &lt;wsHttpContextBinding&gt;
Fornisce un contesto per l'associazione <xref:System.ServiceModel.WsHttpBinding> che richiede che il livello di protezione sia Sign.  
  
## Sintassi  
  
```  
  
<wsHttpContextBinding>  
    <binding   
        allowCookies="Boolean"  
        bypassProxyOnLocal="Boolean"  
        closeTimeout="TimeSpan"  
          contextProtectionLevel="EncryptAndSign/None/Sign"  
        hostNameComparisonMode="StrongWildCard/Exact/WeakWildcard"  
        maxBufferPoolSize="integer"  
        maxReceivedMessageSize="Integer"  
        messageEncoding="Text/Mtom"   
                name="string"  
        openTimeout="TimeSpan"   
        proxyAddress="URI"  
        receiveTimeout="TimeSpan"  
        sendTimeout="TimeSpan"  
  
textEncoding="UnicodeFffeTextEncoding/Utf16TextEncoding/Utf8TextEncoding"  
        transactionFlow="Boolean"  
        useDefaultWebProxy="Boolean">  
        <reliableSession ordered="Boolean"  
           inactivityTimeout="TimeSpan"  
           enabled="Boolean" />  
        <security mode="Message/None/Transport/TransportWithCredential">  
           <transport clientCredentialType="Basic/Certificate/Digest/None/Ntlm/Windows"  
                proxyCredentialType="Basic/Digest/None/Ntlm/Windows"  
                realm="string"   
                defaultClientCredentialType="Basic/Certificate/Digest/None/Ntlm/Windows"  
                defaultProxyCredentialType="Basic/Digest/None/Ntlm/Windows"  
                defaultRealm="string" />  
          <message clientCredentialType="Certificate/IssuedToken/None/UserName/Windows"  
                      algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
           establishSecurityContext="Boolean"   
           negotiateServiceCredential="Boolean"/>  
        </security>  
       <readerQuotas   
            maxArrayLength="Integer"  
            maxBytesPerRead="Integer"  
            maxDepth="Integer"   
            maxNameTableCharCount="Integer"           
            maxStringContentLength="Integer" />  
    </binding>  
</wsHttpContextBinding>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti attributi, elementi figlio ed elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|allowCookies|Valore booleano che indica se il client accetta cookie e li propaga alle richieste future.  Il valore predefinito è `false`.<br /><br /> Quando l'attributo `allowCookies` è impostato su `true`, contextChannel usa httpCookies come modalità di scambio del contesto.  Quando questo attributo è impostato su `false`, il contesto viene scambiato come intestazioni SOAP.<br /><br /> Il valore predefinito è `false`.<br /><br /> È possibile usare questa proprietà quando si interagisce con servizi Web ASMX che usano cookie.  In questo modo i cookie restituiti dal server vengono copiati automaticamente in tutte le richieste client future per quel servizio.|  
|bypassProxyOnLocal|Valore booleano che indica se ignorare il server proxy per indirizzi locali.  Il valore predefinito è `false`.|  
|closeTimeout|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di chiusura.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:01:00.|  
|contextProtectionLevel|Valore valido dell'elemento <xref:System.Net.Security.ProtectionLevel> che specifica il livello di protezione desiderato dell'intestazione SOAP usata per propagare le informazioni sul contesto.  Il valore predefinito è `Sign`.|  
|hostnameComparisonMode|Specifica la modalità di confronto del nome host HTTP usata per analizzare gli URI.  L'attributo è di tipo <xref:System.ServiceModel.HostnameComparisonMode>, che indica se il nome host viene usato per raggiungere il servizio in caso di corrispondenza nell'URI.  Il valore predefinito è <xref:System.ServiceModel.HostnameComparisonMode.StrongWildcard>, che ignora il nome host nella corrispondenza.|  
|maxBufferPoolSize|Numero intero che specifica la dimensione del pool di buffer massima per questa associazione.  Il valore predefinito è 524.288 byte \(512 \* 1024\).  Molte parti di Windows Communication Foundation \(WCF\) usano buffer.  La creazione e l'eliminazione dei buffer a ogni relativo uso sono operazioni onerose, analogamente a quelle di Garbage Collection dei buffer.  Quando si usa un pool di buffer è possibile prelevare un buffer dal pool, usarlo e, al termine delle operazioni, riporlo nel pool.  In questo modo è possibile evitare il sovraccarico dovuto alla creazione e all'eliminazione dei buffer.|  
|maxReceivedMessageSize|Integer positivo che specifica la dimensione massima del messaggio, incluse le intestazioni, che è possibile ricevere su un canale configurato con questa associazione.  Il mittente di un messaggio che supera questo limite riceverà un errore SOAP.  Il destinatario elimina il messaggio e crea una voce dell'evento nel registro di traccia.  Il valore predefinito è 65536.|  
|messageEncoding|Definisce il codificatore usato per codificare il messaggio.  Di seguito vengono elencati i valori validi:<br /><br /> -   Text: usa un codificatore di messaggi di testo.<br />-   Mtom: usa un codificatore Message Transmission Organization Mechanism 1.0 \(MTOM\).<br />-   L'impostazione predefinita è Text.<br /><br /> L'attributo è di tipo <xref:System.ServiceModel.WSMessageEncoding>.|  
|name|Stringa che contiene il nome della configurazione dell'associazione.  Questo valore deve essere univoco perché viene usato per identificare l'associazione.  A partire da [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)], non è necessario che le associazioni e i comportamenti dispongano di un nome.  Per altre informazioni sulla configurazione predefinita e le associazioni e i comportamenti senza nome, vedere [Configurazione semplificata](../../../../../docs/framework/wcf/simplified-configuration.md) e [Configurazione semplificata per servizi WCF](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).|  
|openTimeout|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di apertura.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:01:00.|  
|proxyAddress|URI che specifica l'indirizzo del proxy HTTP.  Se `useSystemWebProxy` è `true`, questa impostazione deve essere `null`.  Il valore predefinito è `null`.|  
|receiveTimeout|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di ricezione.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:01:00.|  
|sendTimeout|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di invio.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:01:00.|  
|textEncoding|Specifica la codifica del set di caratteri da usare per l'emissione dei messaggi dell'associazione.  Di seguito vengono elencati i valori validi:<br /><br /> -   UnicodeFffeTextEncoding: codifica Unicode BigEndian.<br />-   Utf16TextEncoding: codifica a 16 bit.<br />-   Utf8TextEncoding: codifica a 8 bit.<br /><br /> L'impostazione predefinita è Utf8TextEncoding.<br /><br /> L'attributo è di tipo <xref:System.Text.Encoding>.|  
|transactionFlow|Valore booleano che specifica se l'associazione supporta la propagazione di WS\-Transactions.  Il valore predefinito è `false`.|  
|useDefaultWebProxy|Valore booleano che specifica se viene usato il proxy HTTP di sistema configurato automaticamente.  Il valore predefinito è `true`.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md)|Definisce le impostazioni di sicurezza per l'associazione.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.WSHttpSecurityElement>.|  
|[\<quoteReader\>](../Topic/%3CreaderQuotas%3E.md)|Definisce i vincoli sulla complessità dei messaggi SOAP che possono essere elaborati dagli endpoint configurati con questa associazione.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>.|  
|[reliableSession](http://msdn.microsoft.com/it-it/9c93818a-7dfa-43d5-b3a1-1aafccf3a00b)|Specifica se vengono stabilite sessioni affidabili tra endpoint del canale.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<associazioni\>](../../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)|Questo elemento contiene una raccolta di associazioni standard e personalizzate.|  
  
## Vedere anche  
 <xref:System.ServiceModel.WSHttpBinding>   
 <xref:System.ServiceModel.WSHttpContextBinding>   
 <xref:System.ServiceModel.Configuration.wsHttpContextBindingElement>   
 <xref:System.ServiceModel.Channels.ContextBindingElement>   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<associazione\>](../../../../../docs/framework/misc/binding.md)   
 [\<wsHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)