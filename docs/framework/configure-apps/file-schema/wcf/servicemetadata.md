---
title: "&lt;serviceMetadata&gt; | Microsoft Docs"
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
ms.assetid: 2b4c3b4c-31d4-4908-a9b7-5bb411c221f2
caps.latest.revision: 28
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# &lt;serviceMetadata&gt;
Specifica la pubblicazione dei metadati del servizio e delle informazioni associate.  
  
## Sintassi  
  
```  
  
<serviceMetadata   
    externalMetadataLocation="String"  
    httpGetBinding=”String”  
    httpGetBindingConfiguration=”String”  
    httpGetEnabled="Boolean"   
    httpGetUrl="String"  
    httpsGetBinding=”String”  
    httpsGetBindingConfiguration=”String”  
    httpsGetEnabled="Boolean"   
    httpsGetUrl="String"  
    policyVersion="Policy12/Policy15"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|externalMetadataLocation|URI contenente il percorso di un file WSDL. Tale file viene restituito all'utente in risposta a richieste WSDL e MEX al posto del file WSDL generato automaticamente.  Se questo attributo non viene impostato, viene restituito il file WSDL predefinito.  Il valore predefinito è una stringa vuota.|  
|httpGetBinding|Stringa che specifica il tipo dell'associazione che verrà usata per il recupero di metadati tramite HTTP GET.  Questa impostazione è facoltativa.  Se non viene specificata, verranno usate le associazioni predefinite.<br /><br /> Verranno supportate sole le associazioni con elementi di associazione interni che supportano <xref:System.ServiceModel.Channels.IReplyChannel>.  La proprietà <xref:System.ServiceModel.Channels.MessageVersion%2A> dell'associazione deve inoltre essere <xref:System.ServiceModel.Channels.MessageVersion.None%2A>.|  
|httpGetBindingConfiguration|Stringa che imposta il nome dell'associazione specificata nell'attributo `httpGetBinding` che fa riferimento alle informazioni di configurazione aggiuntive di questa associazione.  Lo stesso nome deve essere definito nella sezione `<bindings>`.|  
|httpGetEnabled|Valore booleano che specifica se pubblicare metadati di servizio per il recupero usando una richiesta HTTP GET.  Il valore predefinito è `false`.<br /><br /> Se l'attributo httpGetUrl non viene specificato, l'indirizzo di pubblicazione dei metadati è l'indirizzo del servizio seguito da "?wsdl".  Ad esempio, se l'indirizzo del servizio è "http:\/\/localhost:8080\/CalculatorService", l'indirizzo di pubblicazione dei metadati tramite una richiesta HTTP GET è "http:\/\/localhost:8080\/CalculatorService?wsdl".<br /><br /> Se questa proprietà è `false` o se l'indirizzo del servizio non è basato su HTTP o HTTPS, l'elemento "?wsdl" viene ignorato.|  
|httpGetUrl|URI che specifica l'indirizzo di pubblicazione dei metadati per il recupero usando una richiesta HTTP GET.  Se è specificato un URI relativo, verrà considerato come relativo all'indirizzo di base del servizio.|  
|httpsGetBinding|Stringa che specifica il tipo dell'associazione che verrà usata per il recupero di metadati tramite HTTPS GET.  Questa impostazione è facoltativa.  Se non viene specificata, verranno usate le associazioni predefinite.<br /><br /> Verranno supportate sole le associazioni con elementi di associazione interni che supportano <xref:System.ServiceModel.Channels.IReplyChannel>.  La proprietà <xref:System.ServiceModel.Channels.MessageVersion%2A> dell'associazione deve inoltre essere <xref:System.ServiceModel.Channels.MessageVersion.None%2A>.|  
|httpsGetBindingConfiguration|Stringa che imposta il nome dell'associazione specificata nell'attributo `httpsGetBinding` che fa riferimento alle informazioni di configurazione aggiuntive di questa associazione.  Lo stesso nome deve essere definito nella sezione `<bindings>`.|  
|httpsGetEnabled|Valore booleano che specifica se pubblicare metadati di servizio per il recupero usando una richiesta HTTPS GET.  Il valore predefinito è `false`.<br /><br /> Se l'attributo httpsGetUrl non viene specificato, l'indirizzo di pubblicazione dei metadati è l'indirizzo del servizio seguito da "?wsdl".  Ad esempio, se l'indirizzo del servizio è "https:\/\/localhost:8080\/CalculatorService", l'indirizzo di pubblicazione dei metadati tramite una richiesta HTTPS GET è "https:\/\/localhost:8080\/CalculatorService?wsdl".<br /><br /> Se questa proprietà è `false` o se l'indirizzo del servizio non è basato su HTTP o HTTPS, l'elemento "?wsdl" viene ignorato.|  
|httpsGetUrl|URI che specifica l'indirizzo di pubblicazione dei metadati per il recupero usando una richiesta HTTPS GET.|  
|policyVersion|Stringa che indica la versione della specifica WS\-Policy usata.  L'attributo è di tipo <xref:System.ServiceModel.Description.PolicyVersion>.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<comportamento\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Specifica un elemento di comportamento.|  
  
## Note  
 Questo elemento di configurazione consente di controllare le funzionalità di pubblicazione dei metadati di un servizio.  Per impedire la rivelazione non intenzionale di metadati del servizio potenzialmente riservati, la configurazione predefinita per i servizi [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] disabilita la pubblicazione dei metadati.  Questo comportamento è protetto per impostazione predefinita, ma significa inoltre che non è possibile usare uno strumento di importazione di metadati \(ad esempio Svcutil.exe\) per generare il codice client necessario per chiamare il servizio, a meno che il comportamento del servizio di pubblicazione dei metadati non venga abilitato in modo esplicito in fase di configurazione.  Tale elemento di configurazione consente di abilitare questo comportamento di pubblicazione per il servizio.  
  
 Per un esempio dettagliato del codice di configurazione di questo comportamento, vedere [Comportamento di pubblicazione dei metadati](../../../../../docs/framework/wcf/samples/metadata-publishing-behavior.md).  
  
 Gli attributi `httpGetBinding` e `httpsGetBinding` facoltativi consentono di configurare le associazioni usate per il recupero di metadati tramite HTTP GET \(o HTTPS GET\).  Se non vengono specificati, per il recupero dei metadati verranno usate le associazioni predefinite \(`HttpTransportBindingElement` per HTTP e `HttpsTransportBindingElement` per HTTPS\) a seconda dei casi.  Si noti che non è possibile usare questi attributi con le associazioni WCF incorporate.  Verranno supportate sole le associazioni con elementi di associazione interni che supportano <xref:System.ServiceModel.Channels.IReplyChannel>.  La proprietà <xref:System.ServiceModel.Channels.MessageVersion%2A> dell'associazione deve inoltre essere <xref:System.ServiceModel.Channels.MessageVersion.None%2A>.  
  
 Per ridurre l'esposizione di un servizio agli utenti malintenzionati, questo trasferimento può essere protetto mediante il meccanismo HTTPS \(ovvero SSL su HTTP\).  A tale scopo, è anzitutto necessario associare un certificato X.509 adatto a una porta specifica del computer che ospita il servizio.  \([!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)] [Utilizzo dei certificati](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)\). Aggiungere quindi questo elemento alla configurazione del servizio e impostare l'attributo `httpsGetEnabled` su `true`.  Impostare infine l'attributo `httpsGetUrl` sull'URL dell'endpoint dei metadati del servizio, come illustrato nell'esempio seguente.  
  
```  
<behaviors>  
 <serviceBehaviors>  
  <behavior name="NewBehavior">  
    <serviceMetadata httpsGetEnabled="true"   
     httpsGetUrl="https://myComputerName/myEndpoint" />  
  </behavior>  
 </serviceBehaviors>  
</behaviors>  
```  
  
## Esempio  
 L'esempio seguente configura un servizio per esporre metadati tramite l'elemento \<serviceMetadata\>.  Viene inoltre configurato un endpoint per esporre il contratto `IMetadataExchange` come un'implementazione di un protocollo WS\-MetadataExchange \(MEX\).  Nell'esempio viene usata l'associazione `mexHttpBinding`, ovvero un'utile associazione standard equivalente all'associazione `wsHttpBinding` con la modalità di sicurezza impostata su `None`.  Nell'endpoint viene usato un indirizzo relativo "mex" che, quando risolto rispetto all'indirizzo di base dei servizi, produce l'indirizzo di endpoint "http:\/\/localhost\/servicemodelsamples\/service.svc\/mex".  
  
```  
<configuration>  
<system.serviceModel>  
  <services>  
    <service   
        name="Microsoft.ServiceModel.Samples.CalculatorService"  
        behaviorConfiguration="CalculatorServiceBehavior">  
      <!-- This endpoint is exposed at the base address provided by the host: http://localhost/servicemodelsamples/service.svc  -->  
      <endpoint address=""  
                binding="wsHttpBinding"  
                contract="Microsoft.ServiceModel.Samples.ICalculator" />  
      <!-- the mex endpoint is exposed at http://localhost/servicemodelsamples/service.svc/mex   
           To expose the IMetadataExchange contract, you   
           must enable the serviceMetadata behavior as demonstrated below -->  
      <endpoint address="mex"  
                binding="mexHttpBinding"  
                contract="IMetadataExchange" />  
    </service>  
  </services>  
  
  <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
  <behaviors>  
    <serviceBehaviors>  
      <behavior name="CalculatorServiceBehavior">  
        <!-- The serviceMetadata behavior publishes metadata through   
             the IMetadataExchange contract. When this behavior is   
             present, you can expose this contract through an endpoint   
             as shown above. Setting httpGetEnabled to true publishes   
             the service's WSDL at the <baseaddress>?wsdl  
             eg. http://localhost/servicemodelsamples/service.svc?wsdl -->  
        <serviceMetadata httpGetEnabled="True"/>  
        <serviceDebug includeExceptionDetailInFaults="False" />  
      </behavior>  
    </serviceBehaviors>  
  </behaviors>  
  
</system.serviceModel>  
  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ServiceMetadataPublishingElement>   
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>   
 [Comportamenti di sicurezza](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [Comportamento di pubblicazione dei metadati](../../../../../docs/framework/wcf/samples/metadata-publishing-behavior.md)