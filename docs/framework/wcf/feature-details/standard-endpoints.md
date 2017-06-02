---
title: "Endpoint standard | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3fcb4225-addc-44f2-935d-30e4943a8812
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Endpoint standard
Gli endpoint vengono definiti specificando un indirizzo, un un'associazione e un contratto.Altri parametri che è possibile impostare su un endpoint includono la configurazione di comportamento, le intestazioni e gli URI di ascolto.Per determinati tipi di endpoint tali valori non cambiano.Gli endpoint di scambio dei metadati utilizzano ad esempio sempre il contratto <xref:System.ServiceModel.Description.IMetadataExchange>.Altri endpoint, quali <xref:System.ServiceModel.Web.WebHttpEndpoint>, richiedono sempre un comportamento di endpoint specificato.L'usabilità di un endpoint può essere migliorata grazie a endpoint con valori predefiniti per le proprietà di endpoint di uso comune.Gli endpoint standard consentono a uno sviluppatore di definire un endpoint che dispone di valori predefiniti o in cui una o più proprietà di endpoint non cambiano.Questi endpoint consentono di utilizzare tale endpoint senza dovere specificare informazioni di natura statica.Gli endpoint standard possono essere utilizzati per endpoint infrastruttura ed endpoint applicazione.  
  
## Endpoint infrastruttura  
 Un servizio può esporre endpoint con alcune proprietà non implementate in modo esplicito dall'autore del servizio.L'endpoint di scambio dei metadati espone ad esempio il contratto <xref:System.ServiceModel.Description.IMetadataExchange>, ma l'autore del servizio non implementa l'interfaccia, poiché viene implementata da WCF.Tali endpoint infrastruttura dispongono di valori predefiniti per una o più proprietà di endpoint, alcune delle quali potrebbero non essere modificabili.La proprietà <xref:System.ServiceModel.Description.ServiceEndpoint.Contract%2A> dell'endpoint di scambio dei metadati deve essere <xref:System.ServiceModel.Description.IMetadataExchange>, mentre altre proprietà, tra cui l'associazione, possono essere fornite dallo sviluppatore.Gli endpoint infrastruttura vengono identificati impostando la proprietà <xref:System.ServiceModel.Description.ServiceEndpoint.IsSystemEndpoint%2A> su `true`.  
  
## Endpoint applicazione  
 Gli sviluppatori di applicazioni possono definire endpoint standard specifici che indicano valori predefiniti per l'indirizzo, l'associazione o il contratto.Un endpoint standard viene definito deducendo una classe da <xref:System.ServiceModel.Description.ServiceEndpoint> e impostando le proprietà di endpoint appropriate.È possibile fornire valori predefiniti per proprietà che possono essere modificate.Altre proprietà disporranno di valori statici che non sarà possibile modificare.Nell'esempio riportato di seguito viene illustrato come implementare un endpoint standard.  
  
```  
public class CustomEndpoint : ServiceEndpoint  
    {  
        public CustomEndpoint()  
            : this(string.Empty)  
        {  
        }  
  
        public CustomEndpoint(string address)  
            : this(address, ContractDescription.GetContract(typeof(ICalculator)))  
        {  
        }  
  
        // Create the custom endpoint with a fixed binding  
        public CustomEndpoint(string address, ContractDescription contract)  
            : base(contract)  
        {  
            this.Binding = new BasicHttpBinding();  
            this.IsSystemEndpoint = false;  
        }  
  
        // Definition of the additional property of this endpoint  
        public bool Property  
        {  
            get;  
            set;  
        }  
    }  
```  
  
 Per utilizzare un endpoint personalizzato definito dall'utente in un file di configurazione, è necessario dedurre una classe da <xref:System.ServiceModel.Configuration.StandardEndpointElement>, dedurre una classe da <xref:System.ServiceModel.Configuration.StandardEndpointCollectionElement> e registrare il nuovo endpoint standard nella sezione delle estensioni in app.config o machine.config.<xref:System.ServiceModel.Configuration.StandardEndpointElement> fornisce supporto ala configurazione per l'endpoint standard, come indicato nell'esempio seguente.  
  
```  
public class CustomEndpointElement : StandardEndpointElement  
    {  
        // Definition of the additional property for the standard endpoint element  
        public bool Property  
        {  
            get { return (bool)base["property"]; }  
            set { base["property"] = value; }  
        }  
  
        // The additional property needs to be added to the properties of the standard endpoint element  
        protected override ConfigurationPropertyCollection Properties  
        {  
            get  
            {  
                ConfigurationPropertyCollection properties = base.Properties;  
                properties.Add(new ConfigurationProperty("property", typeof(bool), false, ConfigurationPropertyOptions.None));  
                return properties;  
            }  
        }  
  
        // Return the type of this standard endpoint  
        protected override Type EndpointType  
        {  
            get { return typeof(CustomEndpoint); }  
        }  
  
        // Create the custom service endpoint  
        protected override ServiceEndpoint CreateServiceEndpoint(ContractDescription contract)  
        {  
            return new CustomEndpoint();  
        }  
  
        // Read the value given to the property in config and save it  
        protected override void OnApplyConfiguration(ServiceEndpoint endpoint, ServiceEndpointElement serviceEndpointElement)  
        {  
            CustomEndpoint customEndpoint = (CustomEndpoint)endpoint;  
            customEndpoint.Property = this.Property;  
        }  
  
        // Read the value given to the property in config and save it  
        protected override void OnApplyConfiguration(ServiceEndpoint endpoint, ChannelEndpointElement channelEndpointElement)  
        {  
            CustomEndpoint customEndpoint = (CustomEndpoint)endpoint;  
            customEndpoint.Property = this.Property;  
        }  
  
        // No validation in this sample  
        protected override void OnInitializeAndValidate(ServiceEndpointElement serviceEndpointElement)  
        {  
        }  
  
        // No validation in this sample  
        protected override void OnInitializeAndValidate(ChannelEndpointElement channelEndpointElement)  
        {  
        }  
    }  
  
```  
  
 <xref:System.ServiceModel.Configuration.StandardEndpointCollectionElement> fornisce il tipo di supporto per la raccolta visualizzata nella sezione \<`standardEndpoints`\> all'interno della configurazione per l'endpoint standard.Nell'esempio seguente viene illustrato come implementare la classe.  
  
```  
public class CustomEndpointCollectionElement : StandardEndpointCollectionElement<CustomEndpoint, CustomEndpointElement>  
    {  
         // ...  
  
    }  
```  
  
 Nell'esempio seguente viene mostrato come registrare un endpoint standard nella sezione delle estensioni.  
  
```  
<extensions>  
      <standardEndpointExtensions>  
        <add  
          name="customStandardEndpoint"  
          type="CustomEndpointCollectionElement, Example.dll,  
                Version=1.0.0.0, Culture=neutral, PublicKeyToken=ffffffffffffffff"/>  
  
```  
  
## Configurazione di un endpoint standard  
 È possibile aggiungere endpoint standard al codice o alla configurazione.Per aggiungere un endpoint standard al codice, è sufficiente creare un'istanza del tipo di endpoint standard appropriato e aggiungerla all'host del servizio, come indicato nell'esempio seguente:  
  
```csharp  
serviceHost.AddServiceEndpoint(new CustomEndpoint());  
```  
  
 Per aggiungere un endpoint standard alla configurazione, aggiungere un elemento \<`endpoint`\> all'elemento \<`service`\> ed eventuali impostazioni di configurazione necessarie all'elemento \<`standardEndpoints`\>.Nell'esempio seguente viene mostrato come aggiungere un oggetto <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>, uno degli endpoint standard disponibili in [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)].  
  
```xml  
<services>  
  <service>  
    <endpoint isSystemEndpoint=”true” kind=”udpDiscoveryEndpoint” />  
  </service>  
</services>  
<standardEndpoints>    
  <udpDiscoveryEndpoint>  
     <standardEndpoint multicastAddress="soap.udp://239.255.255.250:3702" />   
  </udpDiscoveryEndpoint>  
</ standardEndpoints >  
```  
  
 Il tipo di endpoint standard viene specificato mediante l'attributo kind nell'elemento \<`endpoint`\>.L'endpoint viene configurato all'interno dell'elemento \<`standardEndpoints`\>.Nell'esempio precedente viene aggiunto e configurato un endpoint <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>.L'elemento \<`udpDiscoveryEndpoint`\> contiene un elemento \<`standardEndpoint`\> che imposta la proprietà <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint.MulticastAddress%2A> di <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>.  
  
## Endpoint standard forniti con .NET Framework  
 Nella tabella seguente sono elencati gli endpoint standard forniti con [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)].  
  
 `Mex Endpoint`  
 Endpoint standard utilizzato per esporre metadati del servizio.  
  
 <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>  
 Endpoint standard utilizzato dai servizi per inviare messaggi di annuncio.  
  
 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>  
 Endpoint standard utilizzato dai servizi per inviare messaggi di individuazione.  
  
 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>  
 Endpoint standard preconfigurato per le operazioni di individuazione su un'associazione multicast UDP.  
  
 <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>  
 Endpoint standard utilizzato dai servizi per inviare messaggi di annuncio su un'associazione UDP.  
  
 <xref:System.ServiceModel.Discovery.DynamicEndpoint>  
 Endpoint standard che utilizza WS\-Discovery per cercare l'indirizzo endpoint in modo dinamico al runtime.  
  
 <xref:System.ServiceModel.Description.ServiceMetadataEndpoint>  
 Endpoint standard per lo scambio dei metadati.  
  
 <xref:System.ServiceModel.Description.WebHttpEndpoint>  
 Endpoint standard con un'associazione <xref:System.ServiceModel.WebHttpBinding> che aggiunge in modo automatico il comportamento <xref:System.ServiceModel.Description.WebHttpBehavior>.  
  
 <xref:System.ServiceModel.Description.WebScriptEndpoint>  
 Endpoint standard con un'associazione <xref:System.ServiceModel.WebHttpBinding> che aggiunge in modo automatico il comportamento <xref:System.ServiceModel.Description.WebScriptEnablingBehavior>.  
  
 <xref:System.ServiceModel.Description.WebServiceEndpoint>  
 Endpoint standard con un'associazione <xref:System.ServiceModel.WebHttpBinding>.  
  
 <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>  
 Endpoint standard che consente di chiamare operazioni di controllo sulle istanze del flusso di lavoro.  
  
 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint>  
 Endpoint standard che supporta la creazione del flusso di lavoro e la ripresa dei segnalibri.