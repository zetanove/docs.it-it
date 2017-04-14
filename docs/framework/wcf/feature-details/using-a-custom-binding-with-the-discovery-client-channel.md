---
title: "Utilizzo di un&#39;associazione personalizzata con il canale client di individuazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 36f95e75-04f7-44f3-a995-a0d623624d7f
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Utilizzo di un&#39;associazione personalizzata con il canale client di individuazione
In caso di utilizzo di un'associazione personalizzata con <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>, è necessario definire un elemento <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider> che crea istanze <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>.  
  
## Creazione di un elemento DiscoveryEndpointProvider  
 L'elemento <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider> è responsabile della creazione di [T:System:ServiceModel.Discovery.DiscoveryEndpoints](assetId:///T:System:ServiceModel.Discovery.DiscoveryEndpoints?qualifyHint=False&amp;autoUpgrade=True) su richiesta.Per definire un provider di endpoint di individuazione, derivare una classe da <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider> ed eseguire l'override del metodo <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider.GetDiscoveryEndpoint%2A>, quindi restituire un nuovo endpoint di individuazione.Nell'esempio seguente viene mostrato come creare un provider di endpoint di individuazione.  
  
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
  
 Una volta definito il provider di endpoint di individuazione, è possibile creare un'associazione personalizzata e aggiungere <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>, che fa riferimento al provider di endpoint di individuazione, come indicato nell'esempio seguente.  
  
```  
DiscoveryClientBindingElement discoveryBindingElement = new DiscoveryClientBindingElement();  
  
// Provide the search criteria and the endpoint over which the probe is sent.  
discoveryBindingElement.FindCriteria = new FindCriteria(typeof(ICalculatorService));  
discoveryBindingElement.DiscoveryEndpointProvider = new UdpDiscoveryEndpointProvider();  
  
CustomBinding customBinding = new CustomBinding(new NetTcpBinding());  
// Insert DiscoveryClientBindingElement at the top of the BindingElement stack.  
// An exception is thrown if this binding element is not at the top.  
customBinding.Elements.Insert(0, discoveryBindingElement);  
```  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] come utilizzare il canale client di individuazione, vedere [Utilizzo del canale client di individuazione](../../../../docs/framework/wcf/feature-details/using-the-discovery-client-channel.md).Per un esempio di codice completo, vedere [Esempio di elemento di associazione di individuazione](../../../../docs/framework/wcf/samples/discovery-binding-element-sample.md).  
  
## Vedere anche  
 [Panoramica di WCF Discovery](../../../../docs/framework/wcf/feature-details/wcf-discovery-overview.md)   
 [Utilizzo del canale client di individuazione](../../../../docs/framework/wcf/feature-details/using-the-discovery-client-channel.md)   
 [Esempio di elemento di associazione di individuazione](../../../../docs/framework/wcf/samples/discovery-binding-element-sample.md)