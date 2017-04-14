---
title: "Procedura: utilizzare la classe MetadataResolver per ottenere dinamicamente i metadati di associazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 56ffcb99-fff0-4479-aca0-e3909009f605
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Procedura: utilizzare la classe MetadataResolver per ottenere dinamicamente i metadati di associazione
In questo argomento viene illustrato come utilizzare la classe <xref:System.ServiceModel.Description.MetadataResolver> per ottenere dinamicamente i metadati di associazione.  
  
### Per ottenere dinamicamente i metadati di associazione  
  
1.  Creare un oggetto <xref:System.ServiceModel.EndpointAddress> con l'indirizzo dell'endpoint dei metadati.  
  
    ```  
    EndpointAddress metaAddress  
      = new EndpointAddress(new   Uri("http://localhost:8080/SampleService/mex"));  
    ```  
  
2.  Chiamare il metodo <xref:System.ServiceModel.Description.MetadataResolver.Resolve%28System.Type%2CSystem.ServiceModel.EndpointAddress%29>, che accetta come parametro il tipo di servizio e l'indirizzo dell'endpoint dei metadati.Questa chiamata restituisce una raccolta di endpoint che implementano il contratto specificato.Dai metadati vengono importate solo le informazioni di associazione. Le informazioni relative al contratto non vengono importate.Al loro posto vengono invece utilizzate le informazioni relative al contratto fornito.  
  
    ```  
    ServiceEndpointCollection endpoints = MetadataResolver.Resolve(typeof(SampleServiceClient),metaAddress);  
    ```  
  
3.  È quindi possibile scorrere la raccolta di endpoint del servizio per estrarre le informazioni di associazione desiderate.Il codice seguente scorre gli endpoint, crea un oggetto client del servizio che passa l'associazione e l'indirizzo relativi all'endpoint corrente e quindi chiama un metodo del servizio.  
  
    ```  
    foreach (ServiceEndpoint point in endpoints)  
    {  
       if (point != null)  
       {  
          // Create a new wcfClient using retrieved endpoints.  
          using (wcfClient = new SampleServiceClient(point.Binding, point.Address))  
          {  
             Console.WriteLine(  
               wcfClient.SampleMethod("Client used the "  
               + point.Address.ToString() + " address."));  
          }  
      }  
    }  
    ```  
  
## Vedere anche  
 [Metadata](../../../../docs/framework/wcf/feature-details/metadata.md)