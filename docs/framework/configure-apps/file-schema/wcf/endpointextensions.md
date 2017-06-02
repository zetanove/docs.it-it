---
title: "&lt;endpointExtensions&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 33396e0a-1fae-4616-b822-923584eebfd1
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;endpointExtensions&gt;
Contenuto della sezione viene registrato un nuovo endpoint standard nella sezione delle estensioni di un file di configurazione di un computer o di un'applicazione.  È possibile aggiungere un endpoint standard a questa raccolta usando la parola chiave `add` e impostando l'attributo `type` dell'elemento sul tipo di endpoint, nonché l'attributo `name` sul nome dell'endpoint standard.  
  
 Nell'esempio seguente viene usato l'elemento `add` e l'attributo `name` per aggiungere un endpoint standard alla sezione `<endpointExtensions>` del file di configurazione.  
  
```  
<system.serviceModel>  
    <extensions>  
        <endpointExtensions>  
           <add name="udpDiscoveryEndpoint"  
                type="System.Discovery.UdpEndpointCollectionElement, System.Discovery.dll, Version=1.0.0.0, Culture=neutral, PublicKeyToken=ffffffffffffffff"/>  
        </endpointExtensions>   
    </extensions>  
</system.serviceModel>  
```  
  
 Dopo aver registrato l'endpoint standard, sarà possibile usarlo come illustrato nell'esempio seguente.  Nel'elemento [\<endpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-element.md) l'attributo `kind` specifica il tipo di endpoint standard che è stato registrato nella sezione `<endpointExtensions>`.  L'attributo `endpointConfiguration` sarà identico all'attributo `name` dell'elemento di configurazione dell'endpoint standard nella sezione `<standardEndpoints>`.  
  
```  
  
<system.serviceModel>  
    <services>  
      <service name="Service1">  
        <endpoint kind="udpDiscoveryEndpoint"  
                  endpointConfiguration="udpConfig" />  
      </service>  
    </services>  
    <standardEndpoints>  
      <udpDiscoveryEndpoint>  
        <standardEndpoint  
                  name="udpConfig"  
                  multicastAddress="soap.udp://239.255.255.250:3703"  
                  ... />  
      </udpDiscoveryEndpoint>  
    </standardEndpoints>  
  </system.serviceModel>  
  
```