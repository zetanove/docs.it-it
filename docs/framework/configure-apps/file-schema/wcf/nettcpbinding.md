---
title: "&lt;netTcpBinding&gt; | Microsoft Docs"
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
helpviewer_keywords: 
  - "elemento netTcpBinding"
ms.assetid: 5c5104a7-8754-4335-8233-46a45322503e
caps.latest.revision: 33
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 33
---
# &lt;netTcpBinding&gt;
Specifica un'associazione protetta, affidabile e ottimizzata adatta per le comunicazioni fra computer.  Per impostazione predefinita, genera uno stack di comunicazione in fase di runtime con Windows per la sicurezza per garantire la sicurezza e l'autenticazione dei messaggi, TCP per il recapito dei messaggi e la codifica binaria dei messaggi.  
  
## Sintassi  
  
```  
  
<netTcpBinding>  
   <binding   
      closeTimeout="TimeSpan"  
      hostNameComparisonMode="StrongWildCard/Exact/WeakWildcard"  
      listenBacklog="Integer"  
      maxBufferPoolSize="integer"  
      maxBufferSize="Integer"  
      maxConnections="Integer"   
      maxReceivedMessageSize="Integer"  
      name="string"  
      openTimeout="TimeSpan"  
      portSharingEnabled="Boolean"  
      receiveTimeout="TimeSpan"  
      sendTimeout="TimeSpan"  
      transactionFlow="Boolean"   
      transactionProtocol="OleTransactions/WSAtomicTransactionOctober2004"   
            transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse"  
  
      <reliableSession ordered="Boolean"  
            inactivityTimeout="TimeSpan"  
            enabled="Boolean" />  
      <security mode="None/Transport/Message/Both">  
            <message clientCredentialType="None/Windows/UserName/Certificate/CardSpace"  
                defaultProtectionLevel="None/Sign/EncryptAndSign"   
algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15" />  
            <transport clientCredentialType="None/Windows/Certificate"  
                protectionLevel="None/Sign/EncryptAndSign" />  
      </security>  
       <readerQuotas   
            maxArrayLength="Integer"  
            maxBytesPerRead="Integer"  
            maxDepth="Integer"   
            maxNameTableCharCount="Integer"           
            maxStringContentLength="Integer" />  
   </binding>  
</netTcpBinding>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|closeTimeout|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di chiusura.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:01:00.|  
|hostnameComparisonMode|Specifica la modalità di confronto del nome host HTTP usata per analizzare gli URI.  L'attributo è di tipo <xref:System.ServiceModel.HostnameComparisonMode>, che indica se il nome host viene usato per raggiungere il servizio in caso di corrispondenza nell'URI.  Il valore predefinito è <xref:System.ServiceModel.HostnameComparisonMode.StrongWildcard>, che ignora il nome host nella corrispondenza.|  
|listenBacklog|Numero intero positivo che specifica il numero massimo di canali di attesa accettati nel listener.  Le connessioni in eccesso vengono messe in coda finché il numero di connessioni non risulta inferiore al limite consentito.  L'attributo `connectionTimeout` limita il tempo di attesa della connessione da parte del client prima che venga generata un'eccezione.  Il valore predefinito è 10.|  
|maxBufferPoolSize|Numero intero che specifica la dimensione del pool di buffer massima per questa associazione.  Il valore predefinito è 512 \* 1024 byte.  Molte parti di Windows Communication Foundation \(WCF\) usano buffer.  La creazione e l'eliminazione dei buffer a ogni relativo uso sono operazioni onerose, analogamente a quelle di Garbage Collection dei buffer.  Quando si usa un pool di buffer è possibile prelevare un buffer dal pool, usarlo e, al termine delle operazioni, riporlo nel pool.  In questo modo è possibile evitare il sovraccarico dovuto alla creazione e all'eliminazione dei buffer.|  
|maxBufferSize|Numero intero positivo che specifica la dimensione massima, in byte, del buffer usato per archiviare messaggi in memoria.<br /><br /> Se l'attributo `transferMode` è uguale a `Buffered`, questo attributo deve essere uguale al valore dell'attributo `maxReceivedMessageSize`.<br /><br /> Se l'attributo `transferMode` è uguale a `Streamed`, questo attributo non può essere superiore al valore dell'attributo `maxReceivedMessageSize` e deve essere uguale almeno alla dimensione delle intestazioni.<br /><br /> Il valore predefinito è 65536.  Per altre informazioni, vedere <xref:System.ServiceModel.Configuration.NetNamedPipeBindingElement.MaxBufferSize%2A>.|  
|maxConnections|Numero intero che specifica il numero massimo di connessioni in uscita e in ingresso che il servizio creerà e accetterà.  Le connessioni in ingresso e in uscita vengono conteggiate in base a un limite distinto specificato da questo attributo.<br /><br /> Le connessioni in ingresso eccedenti il limite vengono messe in coda finché non è disponibile uno spazio inferiore al limite.<br /><br /> Le connessioni in uscita eccedenti il limite vengono messe in coda finché non è disponibile uno spazio inferiore al limite.<br /><br /> Il valore predefinito è 10.|  
|maxReceivedMessageSize|Integer positivo che specifica la dimensione massima del messaggio, incluse le intestazioni, che è possibile ricevere su un canale configurato con questa associazione.  Il mittente di un messaggio che supera questo limite riceverà un errore SOAP.  Il destinatario elimina il messaggio e crea una voce dell'evento nel registro di traccia.  Il valore predefinito è 65536.|  
|name|Stringa che contiene il nome della configurazione dell'associazione.  Questo valore deve essere univoco perché viene usato per identificare l'associazione.  A partire da [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)], non è necessario che le associazioni e i comportamenti dispongano di un nome.  Per altre informazioni sulla configurazione predefinita e le associazioni e i comportamenti senza nome, vedere [Configurazione semplificata](../../../../../docs/framework/wcf/simplified-configuration.md) e [Configurazione semplificata per servizi WCF](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).|  
|openTimeout|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di apertura.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:01:00.|  
|portSharingEnabled|Valore booleano che specifica se è attivata la condivisione delle porte TCP per la connessione.  Se è `false`, ciascuna associazione usa la propria porta esclusiva.  Questa impostazione è appropriata solo per i servizi in quanto non ha effetto per i client.|  
|receiveTimeout|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di ricezione.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:10:00.|  
|sendTimeout|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo fornito per il completamento di un'operazione di invio.  Questo valore deve essere maggiore o uguale a <xref:System.TimeSpan.Zero>.  L'impostazione predefinita è 00:01:00.|  
|transactionFlow|Valore booleano che specifica se l'associazione supporta la propagazione di WS\-Transactions.  Il valore predefinito è `false`.|  
|transactionProtocol|Specifica il protocollo di transazione da usare con questa associazione.  I valori validi sono:<br /><br /> -   OleTransactions<br />-   WSAtomicTransactionOctober2004<br /><br /> L'impostazione predefinita è OleTransactions.  L'attributo è di tipo <xref:System.ServiceModel.TransactionProtocol>.|  
|transferMode|Valore <xref:System.ServiceModel.TransferMode> che specifica se i messaggi vengono memorizzati nel buffer o inviati nel flusso o sono una richiesta o una risposta.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-nettcpbinding.md)|Definisce le impostazioni di sicurezza per l'associazione.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.NetTcpSecurityElement>.|  
|[\<quoteReader\>](../Topic/%3CreaderQuotas%3E.md)|Definisce i vincoli sulla complessità dei messaggi SOAP che possono essere elaborati dagli endpoint configurati con questa associazione.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>.|  
|[reliableSession](http://msdn.microsoft.com/it-it/9c93818a-7dfa-43d5-b3a1-1aafccf3a00b)|Specifica se vengono stabilite sessioni affidabili tra endpoint del canale.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<associazioni\>](../../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)|Questo elemento contiene una raccolta di associazioni standard e personalizzate.|  
  
## Note  
 Per impostazione predefinita, questa associazione genera uno stack di comunicazione runtime che, oltre a implementare la codifica binaria dei messaggi, usa la sicurezza del trasporto e il protocollo TCP per il recapito dei messaggi.  Questa associazione rappresenta una scelta fornita dal sistema [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] appropriata per la comunicazione su una rete Intranet.  
  
 La configurazione predefinita per `netTcpBinding` è più veloce rispetto a quella fornita da `wsHttpBinding`, ma è destinata solo alle comunicazioni tra [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] e [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)].  Il comportamento di sicurezza può essere configurato usando l'attributo `securityMode` facoltativo.  L'utilizzo del protocollo WS\-ReliableMessaging può essere configurato usando l'attributo facoltativo `reliableSessionEnabled`.  La messaggistica affidabile è tuttavia disattivata per impostazione predefinita.  Più in generale, le associazioni HTTP fornite dal sistema, ad esempio `wsHttpBinding` e `basicHttpBinding`, sono configurate in modo da attivare modalità di supporto per impostazione predefinita, mentre l'associazione `netTcpBinding` le disattiva per impostazione predefinita e pertanto è necessario fornire un consenso esplicito per ottenere il supporto, ad esempio, per una delle specifiche WS\-\*.  Ciò significa che la configurazione predefinita per le associazioni TCP è più veloce nello scambio dei messaggi tra endpoint rispetto a quelle predefinite per le associazioni HTTP.  
  
## Esempio  
 L'associazione è specificata nei file di configurazione per il client e il servizio.  Il tipo di associazione è specificato nell'attributo `binding` dell'elemento `<endpoint>`.  Se si desidera configurare l'associazione netTcpBinding e modificare alcune delle relative impostazioni, è necessario definire una configurazione di associazione.  L'endpoint deve fare riferimento alla configurazione di associazione con un attributo `bindingConfiguration`.  Nell'esempio seguente viene modificata una configurazione di associazione.  
  
```  
<services>  
  <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
           behaviorConfiguration="CalculatorServiceBehavior">  
    ...  
    <endpoint address=""  
              binding="netTcpBinding"  
              contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    ...  
  </service>  
</services>  
  
<bindings>  
  <netTcpBinding>  
    <binding   
             closeTimeout="00:01:00"  
             openTimeout="00:01:00"   
             receiveTimeout="00:10:00"   
             sendTimeout="00:01:00"  
             transactionFlow="false"   
             transferMode="Buffered"   
             transactionProtocol="OleTransactions"  
             hostNameComparisonMode="StrongWildcard"   
             listenBacklog="10"  
             maxBufferPoolSize="524288"   
             maxBufferSize="65536"   
             maxConnections="10"  
             maxReceivedMessageSize="65536">  
      <readerQuotas maxDepth="32"   
                    maxStringContentLength="8192"   
                    maxArrayLength="16384"  
                    maxBytesPerRead="4096"   
                    maxNameTableCharCount="16384" />  
      <reliableSession ordered="true"   
                       inactivityTimeout="00:10:00"  
                       enabled="false" />  
      <security mode="Transport">  
        <transport clientCredentialType="Windows" protectionLevel="EncryptAndSign" />  
      </security>  
    </binding>  
  </netTcpBinding>  
</bindings>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.NetTcpBinding>   
 <xref:System.ServiceModel.Configuration.NetTcpBindingElement>   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<associazione\>](../../../../../docs/framework/misc/binding.md)