---
title: "Esempio di configurazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 75515b4a-8d70-44c8-99e0-7423df41380e
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Esempio di configurazione
Questo esempio illustra l'utilizzo di un file di configurazione per rendere individuabile un servizio.  
  
> [!NOTE]
>  L'esempio implementa l'individuazione nella configurazione.Per un esempio che implementa l'individuazione nel codice, vedere [Di base](../../../../docs/framework/wcf/samples/basic-sample.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Discovery\Configuration`  
  
## Configurazione del servizio  
 Il file di configurazione in questo esempio illustra due funzionalità:  
  
-   Rendere individuabile il servizio su un <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> standard.  
  
-   Modificare le informazioni correlate all'individuazione per l'endpoint dell'applicazione del servizio e modificare alcune delle impostazioni correlate all'individuazione nell'endpoint standard.  
  
 Per abilitare l'individuazione, è necessario effettuare alcune modifiche nel file di configurazione dell'applicazione per il servizio:  
  
-   È necessario aggiungere un endpoint di individuazione all'elemento `<service>`.Si tratta di un endpoint <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> standard.Si tratta di un endpoint del sistema che il runtime associa al servizio di individuazione.Il servizio di individuazione è in ascolto dei messaggi su tale endpoint.  
  
-   Un comportamento `<serviceDiscovery>` viene aggiunto alla sezione `<serviceBehaviors>`.Ciò consente al servizio di essere individuato in fase di runtime e l'endpoint di individuazione menzionato in precedenza viene utilizzato per rimanere in ascolto di messaggi `Probe` e `Resolve` di individuazione.Con queste due aggiunte, il servizio è individuabile in corrispondenza dell'endpoint di individuazione specificato.  
  
 Nel frammento di configurazione seguente viene illustrato un servizio con un endpoint dell'applicazione e un endpoint di individuazione definito:  
  
```vb  
<services>  
        <service name="Microsoft.Samples.Discovery.CalculatorService"  
                 behaviorConfiguration="calculatorServiceBehavior">  
          <endpoint address=""  
                    binding="wsHttpBinding"  
                    contract="Microsoft.Samples.Discovery.ICalculatorService"  
                    behaviorConfiguration="endpointBehaviorConfiguration" />  
          <endpoint name="udpDiscovery"   
                    kind="udpDiscoveryEndpoint"   
                endpointConfiguration="adhocDiscoveryEndpointConfiguration"/>        </service>  
      </services>  
  
```  
  
 Per sfruttare i vantaggi degli annunci, è necessario aggiungere un endpoint dell'annuncio.A tale scopo, modificare il file di configurazione come illustrato nel codice seguente.  
  
```  
  
<serviceDiscovery>  
            <announcementEndpoints>  
              <endpoint kind="udpAnnouncementEndpoint"/>  
            </announcementEndpoints>  
          </serviceDiscovery>  
  
```  
  
 L'aggiunta di un endpoint dell'annuncio al comportamento del servizio di individuazione crea un client dell'annuncio predefinito per il servizio.Ciò garantisce che il servizio invii un annuncio online oppure offline rispettivamente quando il servizio viene aperto e chiuso.  
  
 Il file di configurazione va oltre tali semplici passaggi modificando i comportamenti aggiuntivi.È possibile controllare le informazioni correlate all'individuazione tramite endpoint specifici.Ovvero, un utente può controllare se è possibile individuare un endpoint e può anche contrassegnare tale endpoint con <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior.Scopes%2A> e metadati XML personalizzati.A tale scopo, l'utente deve aggiungere una proprietà `behaviorConfiguration` all'endpoint dell'applicazione.In questo caso, la proprietà seguente viene aggiunta all'endpoint dell'applicazione.  
  
```  
behaviorConfiguration="endpointBehaviorConfiguration"  
```  
  
 Tramite l'elemento di configurazione del comportamento, è possibile controllare gli attributi correlati all'individuazione.In questo caso, due ambiti vengono aggiunti all'endpoint dell'applicazione.  
  
```xml  
<endpointBehaviors>  
          <behavior name="endpointBehaviorConfiguration">  
            <endpointDiscovery>  
              <scopes>  
                <add scope="http://www.example.com/calculator"/>  
                <add scope="ldap:///ou=engineering,o=examplecom,c=us"/>  
              </scopes>  
            </endpointDiscovery>  
  
          </behavior>            
        </endpointBehaviors>  
  
```  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] ambiti, vedere [Ricerca di individuazione e FindCriteria](../../../../docs/framework/wcf/feature-details/discovery-find-and-findcriteria.md).  
  
 È inoltre possibile controllare dettagli specifici dell'endpoint di individuazione.Questa operazione viene effettuata tramite <xref:System.ServiceModel.Configuration.StandardEndpointsSection>.In questo esempio, viene modificata la versione del protocollo utilizzata e viene aggiunto un attributo `maxResponseDelay`, come illustrato nell'esempio di codice seguente.  
  
```  
<standardEndpoints>  
   <udpDiscoveryEndpoint>  
      <standardEndpoint name="adhocDiscoveryEndpointConfiguration" discoveryVersion="WSDiscovery11" maxResponseDelay="00:00:00.600" />    
   </udpDiscoveryEndpoint>  
</standardEndpoints>  
  
```  
  
 Di seguito è riportato il file di configurazione completo utilizzato in questo esempio:  
  
```  
<configuration>  
    <system.serviceModel>  
  
      <services>  
        <service name="Microsoft.Samples.Discovery.CalculatorService"  
                 behaviorConfiguration="calculatorServiceBehavior">  
          <endpoint address=""  
                    binding="wsHttpBinding"  
                    contract="Microsoft.Samples.Discovery.ICalculatorService"  
                    behaviorConfiguration="endpointBehaviorConfiguration" />  
         <!-- Define the discovery endpoint -->            
<endpoint name="udpDiscovery" kind="udpDiscoveryEndpoint" endpointConfiguration="adhocDiscoveryEndpointConfiguration"/>        </service>  
      </services>  
  
      <behaviors>  
  
        <serviceBehaviors>  
          <behavior name="calculatorServiceBehavior">  
  
            <!-- Add an announcement endpoint -->  
            <serviceDiscovery>  
              <announcementEndpoints>  
                <endpoint kind="udpAnnouncementEndpoint"/>  
              </announcementEndpoints>  
            </serviceDiscovery>  
          </behavior>  
        </serviceBehaviors>  
  
        <endpointBehaviors>  
          <behavior name="endpointBehaviorConfiguration">  
            <!-- Add scopes used to identify the service -->  
            <endpointDiscovery>  
              <scopes>  
                <add scope="http://www.example.com/calculator"/>  
                <add scope="ldap:///ou=engineering,o=examplecom,c=us"/>  
              </scopes>  
            </endpointDiscovery>  
  
          </behavior>            
        </endpointBehaviors>  
  
      </behaviors>  
  
      <standardEndpoints>  
        <udpDiscoveryEndpoint>  
         <!-- Configure the UDP discovery endpoint -->  
          <standardEndpoint name="adhocDiscoveryEndpointConfiguration" discoveryVersion="WSDiscovery11" maxResponseDelay="00:00:00.600" />    
        </udpDiscoveryEndpoint>  
      </standardEndpoints>  
  
    </system.serviceModel>  
</configuration>  
  
```  
  
## Configurazione del client  
 Nel file di configurazione dell'applicazione per il client, un oggetto `standardEndpoint` di tipo `dynamicEndpoint` viene impiegato per utilizzare l'individuazione come illustrato nel frammento di codice seguente.  
  
```xml  
<client>  
   <!--  Create an endpoint, make kind="dynamicEndpoint" and use the endpointConfiguration to change settings of DynamicEndpoint -->  
   <endpoint name="calculatorEndpoint"  
             binding="wsHttpBinding"  
             contract="ICalculatorService"  
             kind ="dynamicEndpoint"  
             endpointConfiguration="dynamicEndpointConfiguration">  
   </endpoint>  
</client>  
  
```  
  
 Quando un client sta utilizzando un `dynamicEndpoint`, il runtime esegue automaticamente l'individuazione.Durante l'individuazione vengono utilizzate varie impostazioni, ad esempio quelle definite nella sezione `discoveryClientSettings`, in cui viene specificato il tipo di endpoint di individuazione da utilizzare:  
  
```xml  
<endpoint kind="udpDiscoveryEndpoint" endpointConfiguration="adhocDiscoveryEndpointConfiguration" />  
  
```  
  
 Criteri di ricerca utilizzati per cercare i servizi:  
  
```xml  
<!-- Add Scopes, ScopeMatchBy, Extensions and termination criteria in FindCriteria -->  
<findCriteria scopeMatchBy="http://schemas.microsoft.com/ws/2008/06/discovery/rfc" duration="00:00:10" maxResults="1">  
   <scopes>  
      <add scope="http://www.microsoft.com/building42/floor1"/>  
   </scopes>  
   <!-- These extensions are sent from the client to the service as part of the probe message -->  
   <extensions>  
      <CustomMetadata>This is custom metadata that is sent to the service along with the client's find request.</CustomMetadata>  
   </extensions>  
</findCriteria>  
  
```  
  
 L'esempio estende tale funzionalità e modifica i <xref:System.ServiceModel.Discovery.FindCriteria> utilizzati dal client e alcune proprietà dell'`updDiscoveryEndpoint` standard utilizzate per l'individuazione.I <xref:System.ServiceModel.Discovery.FindCriteria> vengono modificati per utilizzare un ambito e un algoritmo `scopeMatchBy` specifico, oltre a criteri di chiusura personalizzati.Inoltre, l'esempio mostra anche come un client è in grado di inviare elementi XML utilizzando messaggi `Probe`.Infine, alcune modifiche vengono apportate a <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>, ad esempio la versione del protocollo utilizzata e impostazioni specifiche dell'UDP, come mostrato nel file di configurazione seguente.  
  
```xml  
<udpDiscoveryEndpoint>    
        <!-- Specify the discovery protocol version and UDP transport settings. -->   
        <standardEndpoint name="adhocDiscoveryEndpointConfiguration" discoveryVersion="WSDiscovery11">  
          <transportSettings duplicateMessageHistoryLength="2048"  
                             maxPendingMessageCount="5"  
                             maxReceivedMessageSize="8192"  
                             maxBufferPoolSize="262144"/>  
        </standardEndpoint>        
      </udpDiscoveryEndpoint>  
  
```  
  
 Di seguito è riportata la configurazione client completa utilizzata nell'esempio:  
  
```  
<configuration>  
  <system.serviceModel>  
  
    <client>  
      <!--  Create an endpoint, make kind="dynamicEndpoint" and use the endpointConfiguration to change settings of DynamicEndpoint -->  
      <endpoint name="calculatorEndpoint"  
                binding="wsHttpBinding"  
                contract="ICalculatorService"  
                kind ="dynamicEndpoint"  
                endpointConfiguration="dynamicEndpointConfiguration">  
      </endpoint>  
    </client>  
  
    <standardEndpoints>  
  
      <dynamicEndpoint>        
        <standardEndpoint name="dynamicEndpointConfiguration">  
          <discoveryClientSettings>  
            <!-- Controls where the discovery happens. In this case, Probe message is sent over UdpDiscoveryEndpoint. -->  
            <endpoint kind="udpDiscoveryEndpoint" endpointConfiguration="adhocDiscoveryEndpointConfiguration" />  
  
            <!-- Add Scopes, ScopeMatchBy, Extensions and termination criteria in FindCriteria -->  
            <findCriteria scopeMatchBy="http://schemas.microsoft.com/ws/2008/06/discovery/rfc" duration="00:00:10" maxResults="1">  
              <scopes>  
                <add scope="http://www.microsoft.com/building42/floor1"/>  
              </scopes>  
              <!-- These extensions are sent from the client to the service as part of the probe message -->  
              <extensions>  
                <CustomMetadata>This is custom metadata that is sent to the service along with the client's find request.</CustomMetadata>  
              </extensions>  
            </findCriteria>  
          </discoveryClientSettings>  
        </standardEndpoint>     
      </dynamicEndpoint>  
  
      <udpDiscoveryEndpoint>    
        <!-- Specify the discovery protocol version and UDP transport settings. -->   
        <standardEndpoint name="adhocDiscoveryEndpointConfiguration" discoveryVersion="WSDiscovery11">  
          <transportSettings duplicateMessageHistoryLength="2048"  
                             maxPendingMessageCount="5"  
                             maxReceivedMessageSize="8192"  
                             maxBufferPoolSize="262144"/>  
        </standardEndpoint>        
      </udpDiscoveryEndpoint>  
  
    </standardEndpoints>  
  
  </system.serviceModel>  
  
```  
  
#### Per utilizzare questo esempio  
  
1.  Questo esempio utilizza endpoint HTTP e per eseguirlo è necessario aggiungere gli elenchi di controllo di accesso \(ACL\) agli URL appropriati. Per ulteriori informazioni, vedere [Configurazione di HTTP e HTTPS](http://go.microsoft.com/fwlink/?LinkId=70353).L'esecuzione del comando seguente con privilegi elevati consente di aggiungere gli elenchi di controllo di accesso appropriati.È possibile sostituire dominio e nome utente per gli argomenti seguenti se il comando non funziona in modo corretto.`netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%`  
  
2.  Compilare la soluzione.  
  
3.  Eseguire il servizio eseguibile dalla directory di compilazione.  
  
4.  Eseguire il file eseguibile del client.Il client è in grado di individuare il servizio.  
  
## Vedere anche