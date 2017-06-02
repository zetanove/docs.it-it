---
title: "Procedura: configurare un&#39;associazione WS-Metadata Exchange personalizzata | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "scambio protetto metadati-WS [WCF]"
  - "scambio protetto metadati-WS [WCF], configurazione di un'associazione personalizzata"
ms.assetid: cdba4d73-da64-4805-bc56-9822becfd1e4
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Procedura: configurare un&#39;associazione WS-Metadata Exchange personalizzata
In questo argomento viene illustrato come configurare un'associazione WS\-Metadata Exchange personalizzata.  [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] include quattro associazioni di metadati definite dal sistema, ma è possibile pubblicare metadati usando qualsiasi associazione desiderata.  In questo argomento viene illustrato come pubblicare metadati usando `wsHttpBinding`.  Questa associazione offre la possibilità di esporre i metadati in modo sicuro.  Il codice riportato in questo articolo si basa su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md).  
  
### Uso di un file di configurazione  
  
1.  Nel file di configurazione del servizio aggiungere un comportamento del servizio che contenga il tag `serviceMetadata`:  
  
    ```  
    <behaviors>  
       <serviceBehaviors>  
         <behavior name="CalculatorServiceBehavior">  
           <serviceMetadata httpGetEnabled="True"/>  
         </behavior>  
       </serviceBehaviors>  
    </behaviors>  
    ```  
  
2.  Aggiungere un attributo `behaviorConfiguration` al tag del servizio che fa riferimento a questo nuovo comportamento:  
  
    ```  
    <service        name="Microsoft.ServiceModel.Samples.CalculatorService"  
    behaviorConfiguration="CalculatorServiceBehavior">   
    ```  
  
3.  Aggiungere un endpoint dei metadati specificando mex come indirizzo, `wsHttpBinding` come associazione e <xref:System.ServiceModel.Description.IMetadataExchange> come contratto:  
  
    ```  
    <endpoint address="mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange" />  
    ```  
  
4.  Per verificare che l'endpoint dello scambio di metadati stia funzionando correttamente, aggiungere un tag dell'endpoint nel file di configurazione client:  
  
    ```  
    <endpoint name="MyMexEndpoint"               address="http://localhost:8000/servicemodelsamples/service/mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange"/>  
    ```  
  
5.  Nel metodo Main\(\) del client creare una nuova istanza di <xref:System.ServiceModel.Description.MetadataExchangeClient>, impostare la proprietà <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> su `true`, chiamare <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> e quindi eseguire un'iterazione nella raccolta di metadati restituita:  
  
    ```  
    string mexAddress = "http://localhost:8000/servicemodelsamples/service/mex";  
  
    MetadataExchangeClient mexClient = new MetadataExchangeClient("MyMexEndpoint");  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet mdSet = mexClient.GetMetadata(new EndpointAddress(mexAddress));  
    foreach (MetadataSection section in mdSet.MetadataSections)  
    Console.WriteLine("Metadata section: " + section.Dialect.ToString());  
    ```  
  
### Configurazione mediante codice  
  
1.  Creare un'istanza dell'associazione <xref:System.ServiceModel.WsHttpBinding>:  
  
    ```  
    WSHttpBinding binding = new WSHttpBinding();  
    ```  
  
2.  Creare un'istanza di <xref:System.ServiceModel.ServiceHost>:  
  
    ```  
    ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService), baseAddress);  
    ```  
  
3.  Aggiungere un endpoint di servizio e un'istanza di <xref:System.ServiceModel.Description.ServiceMetadataBehavior>:  
  
    ```  
    serviceHost.AddServiceEndpoint(typeof(ICalculator), binding, baseAddress);  
    ServiceMetadataBehavior smb = new ServiceMetadataBehavior();  
    smb.HttpGetEnabled = true;  
    serviceHost.Description.Behaviors.Add(smb);  
    ```  
  
4.  Aggiungere un endpoint dello scambio di metadati, specificando la classe <xref:System.ServiceModel.WSHttpBinding> creata in precedenza:  
  
    ```  
    serviceHost.AddServiceEndpoint(typeof(IMetadataExchange), binding, mexAddress);  
    ```  
  
5.  Per verificare che l'endpoint dello scambio di metadati stia funzionando correttamente, aggiungere un tag dell'endpoint nel file di configurazione client:  
  
    ```  
    <endpoint name="MyMexEndpoint"               address="http://localhost:8000/servicemodelsamples/service/mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange"/>  
    ```  
  
6.  Nel metodo Main\(\) del client creare una nuova istanza di <xref:System.ServiceModel.Description.MetadataExchangeClient>, impostare la proprietà <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> su `true`, chiamare <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> e quindi eseguire un'iterazione nella raccolta di metadati restituita:  
  
    ```  
    string mexAddress = "http://localhost:8000/servicemodelsamples/service/mex";  
  
    MetadataExchangeClient mexClient = new MetadataExchangeClient("MyMexEndpoint");  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet mdSet = mexClient.GetMetadata(new EndpointAddress(mexAddress));  
    foreach (MetadataSection section in mdSet.MetadataSections)  
    Console.WriteLine("Metadata section: " + section.Dialect.ToString());  
  
    ```  
  
## Vedere anche  
 [Comportamento di pubblicazione dei metadati](../../../../docs/framework/wcf/samples/metadata-publishing-behavior.md)   
 [Recupero di metadati](../../../../docs/framework/wcf/samples/retrieve-metadata.md)   
 [Metadata](../../../../docs/framework/wcf/feature-details/metadata.md)   
 [Pubblicazione di metadati](../../../../docs/framework/wcf/feature-details/publishing-metadata.md)   
 [Pubblicazione di endpoint dei metadati](../../../../docs/framework/wcf/publishing-metadata-endpoints.md)