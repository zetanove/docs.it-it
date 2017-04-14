---
title: "&lt;endpointDiscovery&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 70812717-888a-4748-9640-0df6715ff029
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# &lt;endpointDiscovery&gt;
Specifica le varie impostazioni di individuazione per un endpoint, quali l'individuazione, gli ambiti e le eventuali estensioni personalizzate ai relativi metadati.  
  
## Sintassi  
  
```  
  
<behaviors>  
  <endpointBehaviors>  
    <behavior name="String">  
      <endpointDiscovery enabled="Boolean">  
        <scopes>  
          <add scope="URI"/>  
        </scopes>  
        <extensions>  
        </extensions>  
      </endpointDiscovery>  
    </behavior>  
  </endpointBehaviors>  
</behaviors>  
  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|enabled|Valore booleano che specifica se è abilitata l'individuazione dell'endpoint.  Il valore predefinito è `false`.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<scopes\>](../../../../../docs/framework/configure-apps/file-schema/wcf/scopes.md)|Raccolta di URI di ambito per l'endpoint.  A un singolo endpoint è possibile associare più URI di ambito.|  
|[\<estensioni\>](../../../../../docs/framework/configure-apps/file-schema/wcf/extensions.md) \[di \<endpointDiscovery\>\]|Raccolta di elementi XML che consente di specificare metadati personalizzati da pubblicare per un endpoint.|  
|\<types\>|Raccolta di interfacce da cercare.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<comportamento\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Specifica un elemento di comportamento.|  
|||  
  
## Note  
 L'aggiunta di questo elemento di configurazione alla configurazione di comportamento dell'endpoint con l'attributo `enabled` impostato su `true` ne determina l'abilitazione dell'individuazione.  È inoltre possibile usare l'elemento figlio [\<scopes\>](../../../../../docs/framework/configure-apps/file-schema/wcf/scopes.md) per specificare gli URI di ambito personalizzati che è possibile usare per filtrare gli endpoint di servizio durante l'esecuzione di query, nonché l'elemento figlio [\<estensioni\>](../../../../../docs/framework/configure-apps/file-schema/wcf/extensions.md) per specificare metadati personalizzati da pubblicare insieme ai metadati individuabili standard \(EPR, ContractTypeName, BindingName, Ambito e ListenURI\).  
  
 Questo elemento di configurazione dipende dall'elemento [\<serviceDiscovery\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicediscovery.md) che fornisce il controllo del livello di servizio dell'individuazione.  Questo comporta che le impostazioni dell'elemento vengono ignorate se [\<serviceDiscovery\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicediscovery.md) non è presente nella configurazione.  
  
## Esempio  
 Nell'esempio di configurazione seguente vengono specificati ambiti di filtro e metadati di estensione da pubblicare per un endpoint.  
  
```  
  
<services>  
  <service name="CalculatorService"  
           behaviorConfiguration="CalculatorServiceBehavior">  
     <endpoint binding="basicHttpBinding"  
              address="calculator"  
              contract="ICalculatorService"  
              behaviorConfiguration="calculatorEndpointBehavior" />  
  </service>  
</services>  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="CalculatorServiceBehavior">  
      <serviceDiscovery />  
    </behavior>  
  </serviceBehaviors>  
  <endpointBehaviors>  
    <behavior name="calculatorEndpointBehavior">  
      <endpointDiscovery enabled="true">  
        <scopes>  
          <add scope="http://contoso/test1"/>  
          <add scope="http://contoso/test2"/>  
        </scopes>  
        <extensions>  
          <e:Publisher xmlns:e="http://example.org">  
            <e:Name>The Example Organization</e:Name>  
            <e:Address>One Example Way, ExampleTown, EX 12345</e:Address>  
            <e:Contact>support@example.org</e:Contact>  
          </e:Publisher>  
          <AnotherCustomMetadata>Custom Metadata</AnotherCustomMetadata>  
        </extensions>  
      </endpointDiscovery>  
    </behavior>  
  </endpointBehaviors>  
</behaviors>  
  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior>