---
title: "Esempio di elemento di associazione di individuazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: af513015-85bf-417b-8729-1bdff77ff6d6
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Esempio di elemento di associazione di individuazione
In questo esempio viene illustrato come utilizzare l'elemento di associazione del client di individuazione per individuare un servizio.Questa funzionalità consente agli sviluppatori di aggiungere un canale client di individuazione allo stack dei canali del client esistente, rendendo il modello di programmazione estremamente intuitivo.Quando il canale associato viene aperto, l'indirizzo del servizio viene risolto utilizzando la funzionalità di individuazione.L'esempio è costituito dai progetti seguenti:  
  
-   **CalculatorService**: servizio di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] individuabile.  
  
-   **CalculatorClient**: applicazione client di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che utilizza il canale client di individuazione per cercare e chiamare CalculatorService.  
  
-   **DynamicCalculatorClient**: applicazione client di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che utilizza un endpoint dinamico per cercare e chiamare CalculatorService.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Discovery\DiscoveryBindingElement`  
  
## CalculatorService  
 Questo progetto contiene un servizio calcolatrice semplice che implementa il contratto `ICalculatorService`.  
  
 Il file App.config seguente viene utilizzato per aggiungere un comportamento `<serviceDiscovery>` nei comportamenti del servizio, nonché l'endpoint di individuazione.  
  
```  
<system.serviceModel>  
    <services>  
      <service behaviorConfiguration="CalculatorBehavior" name="Microsoft.Samples.Discovery.CalculatorService">  
        <endpoint name="udpDiscoveryEpt" kind="udpDiscoveryEndpoint" />  
      </service>  
    </services>  
    <behaviors>  
      <!--Enable discovery through configuration.-->  
      <serviceBehaviors>  
        <behavior name="CalculatorBehavior">  
          <serviceDiscovery>  
          </serviceDiscovery>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
```  
  
 Il servizio e gli endpoint corrispondenti vengono in tal modo resi individuabili.CalculatorService è un servizio indipendente che aggiunge un endpoint utilizzando l'associazione NetTcpBinding.Aggiunge inoltre `EndpointDiscoveryBehavior` all'endpoint e specifica un ambito, come illustrato nel codice seguente.  
  
```  
// Add a NET.TCP endpoint and add a scope to that endpoint.  
ServiceEndpoint netTcpEndpoint = serviceHost.AddServiceEndpoint(typeof(ICalculatorService), new NetTcpBinding(), netTcpAddress);  
EndpointDiscoveryBehavior netTctEndpointBehavior = new EndpointDiscoveryBehavior();  
netTctEndpointBehavior.Scopes.Add(new Uri("ldap:///ou=engineering,o=exampleorg,c=us"));  
netTcpEndpoint.Behaviors.Add(netTctEndpointBehavior);  
serviceHost.Open();  
```  
  
## CalculatorClient  
 Questo progetto contiene un'implementazione client che invia messaggi a CalculatorService.Questo programma utilizza il metodo `CreateCustomBindingWithDiscoveryElement()` per creare un'associazione personalizzata che utilizza il canale client di individuazione.  
  
```  
static CustomBinding CreateCustomBindingWithDiscoveryElement()  
 {  
      DiscoveryClientBindingElement discoveryBindingElement = new DiscoveryClientBindingElement();  
  
            // Provide the search criteria and the endpoint over which the probe is sent  
            discoveryBindingElement.FindCriteria = new FindCriteria(typeof(ICalculatorService));  
            discoveryBindingElement.DiscoveryEndpointProvider = new UdpDiscoveryEndpointProvider();  
  
            CustomBinding customBinding = new CustomBinding(new NetTcpBinding());  
            // Insert DiscoveryClientBindingElement at the top of the BindingElement stack.  
            // An exception is thrown if this binding element is not at the top  
            customBinding.Elements.Insert(0, discoveryBindingElement);  
  
            return customBinding; }  
```  
  
 Dopo aver creato un'istanza di <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>, lo sviluppatore specifica i criteri da utilizzare durante la ricerca di un servizio.In questo caso, il criterio di ricerca dell'individuazione è il tipo `ICalculatorService`.Lo sviluppatore specifica inoltre un oggetto <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider> che restituisce un oggetto <xref:System.ServiceModel.Discovery.DiscoveryEndpoint> che specifica la posizione in cui eseguire la ricerca dei servizi.<xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider> restituisce una nuova istanza di <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Utilizzo di un'associazione personalizzata con il canale client di individuazione](../../../../docs/framework/wcf/feature-details/using-a-custom-binding-with-the-discovery-client-channel.md).  
  
```  
// Extend DiscoveryEndpointProvider class to change the default DiscoveryEndpoint  
    // to the DiscoveryClientBindingElement. The Discovery ClientChannel   
    // uses this endpoint to send Probe message.  
    public class UdpDiscoveryEndpointProvider : DiscoveryEndpointProvider  
    {  
        public override DiscoveryEndpoint GetDiscoveryEndpoint()  
        {  
            return new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscoveryApril2005);  
        }  
    }  
```  
  
 In questo caso, il client utilizza il meccanismo UDP multicast definito dal protocollo di individuazione per la ricerca dei servizi nella subnet locale.La restante parte del metodo crea un'associazione personalizzata e inserisce l'elemento di associazione dell'individuazione in cima allo stack.  
  
> [!NOTE]
>  È necessario posizionare <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> in cima allo stack dell'associazione.È necessario che qualsiasi <xref:System.ServiceModel.Channels.BindingElement> posto in cima a <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> verifichi che la channel factory o il canale creato non utilizzi la proprietà `EndpointAddress` o `Via`, poiché l'indirizzo effettivo viene trovato solo in corrispondenza del canale client di individuazione.  
  
 È quindi possibile creare un'istanza di `CalculatorClient` attraverso il passaggio di questa associazione personalizzata e di un indirizzo dell'endpoint.  
  
```  
CalculatorServiceClient client = new CalculatorServiceClient(CreateCustomBindingWithDiscoveryElement(), DiscoveryClientBindingElement.DiscoveryEndpointAddress);  
```  
  
 Quando si utilizza il canale client di individuazione, viene passato l'indirizzo dell'endpoint costante specificato in precedenza.Quindi, in fase di esecuzione, il canale client di individuazione trova il servizio specificato dai criteri di ricerca e vi si connette.Affinché il servizio e il client stabiliscano una connessione, è inoltre necessario che dispongano dello stesso stack dell'associazione sottostante.  
  
#### Per utilizzare questo esempio  
  
1.  Aprire la soluzione in [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
2.  Compilare la soluzione.  
  
3.  Eseguire l'applicazione di servizio e ognuna delle applicazioni client.  
  
4.  Si osservi che il client è stato in grado di trovare il servizio senza conoscerne l'indirizzo.  
  
## Vedere anche