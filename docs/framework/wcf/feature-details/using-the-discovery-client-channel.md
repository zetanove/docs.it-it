---
title: "Utilizzo del canale client di individuazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1494242a-1d64-4035-8ecd-eb4f06c8d2ba
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Utilizzo del canale client di individuazione
In fase di scrittura di un'applicazione client WCF è necessario conoscere l'indirizzo endpoint del servizio che si sta chiamando.In molti casi l'indirizzo endpoint di un servizio non è noto in anticipo o l'indirizzo del servizio cambia con il tempo.Il canale client di individuazione consente di scrivere un'applicazione client WCF, descrivere il servizio che si desidera chiamare e il canale client invia automaticamente una richiesta del probe.Quando un servizio risponde, il canale client di individuazione recupera l'indirizzo endpoint per il servizio dalla risposta del probe e lo utilizza per chiamare il servizio.  
  
## Utilizzo del canale client di individuazione  
 Per utilizzare il canale client di individuazione, aggiungere un'istanza di <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> allo stack del canale client.È in alternativa possibile utilizzare <xref:System.ServiceModel.Discovery.DynamicEndpoint> e un <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> verrà aggiunto in modo automatico all'associazione, se non è già presente.  
  
> [!CAUTION]
>  È consigliabile rendere <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> l'elemento in primo piano sullo stack del canale client.Qualsiasi elemento di associazione aggiunto in cima a <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> deve verificare che <xref:System.ServiceModel.ChannelFactory> o il canale creato non utilizzi l'indirizzo endpoint o `Via` \(passato al metodo `CreateChannel`\), poiché potrebbero non contenere l'indirizzo corretto.  
  
 La classe <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> contiene due proprietà pubbliche:  
  
1.  <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement.FindCriteria%2A>, utilizzata per descrivere il servizio che si desidera chiamare.  
  
2.  <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement.DiscoveryEndpoint%2A>, che specifica l'endpoint di individuazione a cui inviare i messaggi di individuazione.  
  
 La proprietà <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement.FindCriteria%2A> consente di specificare il contratto di servizio cercato, qualsiasi URI di ambito obbligatorio e il numero massimo di tentativi di aprire il canale.Il tipo di contratto viene specificato chiamando il costruttore <xref:System.ServiceModel.Discovery.FindCriteria%2A>.È possibile aggiungere gli URI di ambito alla proprietà <xref:System.ServiceModel.Discovery.FindCriteria.Scopes%2A>.La proprietà <xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> consente di specificare il numero massimo di risultati a cui il client tenta di connettersi.Se viene ricevuta una risposta del probe, il client tenta di aprire il canale utilizzando l'indirizzo endpoint dalla risposta del probe.Se si verifica un'eccezione, il client passa alla risposta del probe successivo, in attesa di ricezione di più risposte, se necessario.Questo schema continua finché il canale non viene aperto o viene raggiunto il numero massimo di risultati.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] queste impostazioni, vedere <xref:System.ServiceModel.Discovery.FindCriteria%2A>.  
  
 La proprietà <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement.DiscoveryEndpoint%2A> consente di specificare l'endpoint di individuazione da utilizzare.In genere si tratta di un <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>, ma può essere rappresentato da qualsiasi endpoint valido.  
  
 In fase di creazione dell'associazione da utilizzare per comunicare con il servizio, è necessario utilizzare la stessa associazione del servizio.L'unica differenza consiste nel fatto che l'associazione client dispone di un <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> in cima allo stack.Se il servizio utilizza una delle associazioni fornite dal sistema, creare un nuovo elemento <xref:System.ServiceModel.Channels.CustomBinding> e passare all'associazione fornita dal sistema al costruttore <xref:System.ServiceModel.CustomBinding.CustomBinding%2A>.Sarà quindi possibile aggiungere <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> chiamando `Insert` sulla proprietà <xref:System.ServiceModel.Channels.Binding.Elements%2A>.  
  
 Una volta aggiunto l'elemento <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> all'associazione e dopo averne eseguito la configurazione, è possibile creare un'istanza della classe client WCF, aprirla e chiamare i relativi metodi.Nell'esempio seguente viene utilizzato il canale client di individuazione per individuare un servizio WCF che implementa la classe `ICalculator` \(utilizzata nell'esercitazione WCF della Guida introduttiva\) e chiama il relativo metodo `Add`.  
  
```  
// Create the DiscoveryClientBindingElement  
DiscoveryClientBindingElement bindingElement = new DiscoveryClientBindingElement();  
// Search for a service that implements the ICalculator interface, attempting to open  
// the channel a maximum of 2 times  
bindingElement.FindCriteria = new FindCriteria(typeof(ICalculator)) { MaxResults = 2 };  
// Use the UdpDiscoveryEndpoint  
bindingElement.DiscoveryEndpoint = new UdpDiscoveryEndpoint();  
  
// The service uses the BasicHttpBinding, so use that and insert the DiscoveryClientBindingElement at the   
// top of the stack  
CustomBinding binding = new CustomBinding(new BasicHttpBinding());  
binding.Elements.Insert(0,bindingElement);  
  
try  
{  
    // Create the WCF client and call a method  
    CalculatorClient client = new CalculatorClient(binding, new EndpointAddress("http://schemas.microsoft.com/dynamic"));  
    client.Open();  
    client.Add(1, 1);  
}  
catch (EndpointNotFoundException ex)  
{  
    Console.WriteLine("An exception occurred: " + ex.Message);  
}  
```  
  
## Sicurezza e canale client di individuazione  
 In caso di utilizzo del canale client di individuazione, vengono specificati due endpoint.Uno viene utilizzato per messaggi di individuazione, in genere <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>, e l'altro è l'endpoint dell'applicazione.In caso di implementazione di un servizio sicuro, è necessario proteggere entrambi gli endpoint.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] sicurezza, vedere [Protezione di servizi e client](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md).