---
title: "Uso di NetHttpBinding | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fe134acf-ceca-49de-84a9-05a37e3841f1
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Uso di NetHttpBinding
<xref:System.ServiceModel.NetHttpBinding> è un'associazione progettata per usare i servizi HTTP o WebSocket e usa la codifica binaria per impostazione predefinita.  L'oggetto <xref:System.ServiceModel.NetHttpBinding> rileverà se viene usato con un contratto request\/reply o un contratto duplex e modificherà il comportamento di conseguenza. Utilizzerà HTTP per i contratti request\/reply e WebSockets per i contratti duplex.  È possibile eseguire l'override di questo comportamento usando l'impostazione <xref:System.ServiceModel.NetHttpBinding.WebSocketTransportUsage%2A>:  
  
1.  Always: forza l'uso di WebSockets anche per i contratti request\/reply.  
  
2.  Never: impedisce l'uso di WebSockets.  Il tentativo di utilizzo di un contratto duplex con questa impostazione genererà un'eccezione.  
  
3.  WhenDuplex: si tratta del valore predefinito e si comporta come descritto in precedenza.  
  
 <xref:System.ServiceModel.NetHttpBinding> supporta sessioni affidabili sia in modalità HTTP sia in modalità WebSocket.  Nella modalità WebSocket, le sessioni vengono fornite dal trasporto.  
  
> [!WARNING]
>  Quando si usa <xref:System.ServiceModel.NetHttpBinding> e l'elemento TransferMode dell'associazione è impostato su TransferMode.Streamed, i flussi di grandi dimensioni possono causare un deadlock e quindi il timeout della chiamata.  Per risolvere il problema inviare messaggi più piccoli o usare TransferMode.Buffered.  
  
## Configurazione dell'utilizzo di NetHttpBinding in un servizio  
 L'endpoint <xref:System.ServiceModel.NetHttpBinding> può essere configurato come qualsiasi altra associazione.  Nel frammento di configurazione seguente è illustrato come configurare un servizio WCF con <xref:System.ServiceModel.NetHttpBinding>.  
  
```xml  
<system.serviceModel>  
    <services>  
      <service name="WcfService1.Service1">  
        <endpoint address=""  
                  binding="netHttpBinding"  
                  contract="WcfService1.IService1"/>  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange"/>  
      </service>  
    </services>  
    <bindings>  
      <netHttpBinding>  
        <binding name="My_NetHttpBindingConfig">  
          <webSocketSettings transportUsage="WhenDuplex"/>  
        </binding>  
      </netHttpBinding>  
    </bindings>  
    <!- ... -->   
  </system.serviceModel>  
```  
  
 Nel frammento di codice seguente viene illustrato come aggiungere l'oggetto <xref:System.ServiceModel.NetHtttpBinding> nel codice.  
  
```csharp  
ServiceHost svchost = new ServiceHost(typeof(Service1), baseAddress);  
            NetHttpBinding binding = new NetHttpBinding();  
            svchost.AddServiceEndpoint(typeof(IService1), binding, address);   
        }  
```  
  
## Vedere anche  
 [Configurazione di associazioni per servizi](../../../../docs/framework/wcf/configuring-bindings-for-wcf-services.md)   
 [Associazioni](../../../../docs/framework/wcf/feature-details/bindings.md)   
 [Associazioni fornite dal sistema](../../../../docs/framework/wcf/system-provided-bindings.md)   
 [Servizi duplex](../../../../docs/framework/wcf/feature-details/duplex-services.md)