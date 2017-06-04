---
title: "Procedura: esportare asserzioni di criteri personalizzate | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 99030386-43b0-4f7b-866d-17ea307f5cbd
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Procedura: esportare asserzioni di criteri personalizzate
Le asserzioni di criteri descrivono le funzionalità e i requisiti di un endpoint del servizio.Le applicazioni del servizio possono utilizzare asserzioni di criteri personalizzate nei metadati del servizio per comunicare informazioni sulla personalizzazione di endpoint, associazione e contratto all'applicazione client.È possibile utilizzare [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per esportare asserzioni in espressioni di criteri collegate alle associazioni WSDL nell'endpoint, nell'operazione o negli oggetti del messaggio, a seconda delle funzionalità o dei requisiti da comunicare.  
  
 Le asserzioni di criteri personalizzate vengono esportate mediante l'implementazione dell'interfaccia <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=fullName> in un elemento <xref:System.ServiceModel.Channels.BindingElement?displayProperty=fullName>, inserendo l'elemento dell'associazione direttamente nell'associazione dell'endpoint del servizio o registrando l'elemento dell'associazione nel file di configurazione dell'applicazione.È necessario che l'implementazione dell'esportazione del criterio aggiunga l'asserzione di criteri personalizzata come istanza <xref:System.Xml.XmlElement?displayProperty=fullName> all'elemento <xref:System.ServiceModel.Description.PolicyAssertionCollection?displayProperty=fullName> appropriato nell'elemento <xref:System.ServiceModel.Description.PolicyConversionContext?displayProperty=fullName> passato al metodo <xref:System.ServiceModel.Description.IPolicyExportExtension.ExportPolicy%2A>.  
  
 È inoltre necessario controllare la proprietà <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> della classe <xref:System.ServiceModel.Description.WsdlExporter> ed esportare espressioni del criterio annidate e attributi dello schema dei criteri nello spazio dei nomi corretto in base alla versione del criterio specificata.  
  
 Per importare asserzioni di criteri personalizzate, vedere <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=fullName> e [Procedura: importare asserzioni di criteri personalizzati](../../../../docs/framework/wcf/extending/how-to-import-custom-policy-assertions.md).  
  
### Per esportare asserzioni di criteri personalizzate  
  
1.  Implementare l'interfaccia <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=fullName> in una classe <xref:System.ServiceModel.Channels.BindingElement?displayProperty=fullName>.Nell'esempio di codice seguente viene illustrata l'implementazione di un'asserzione di criteri personalizzata a livello di associazione.  
  
     [!code-csharp[CustomPolicySample#14](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/policyexporter.cs#14)]
     [!code-vb[CustomPolicySample#14](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/custompolicysample/vb/policyexporter.vb#14)]  
  
2.  Inserire l'elemento di associazione nell'associazione dell'endpoint a livello di programmazione o utilizzando un file di configurazione dell'applicazione.Vedere le procedure seguenti.  
  
### Per inserire un elemento di associazione utilizzando un file di configurazione dell'applicazione  
  
1.  Implementare <xref:System.ServiceModel.Configuration.BindingElementExtensionElement?displayProperty=fullName> per l'elemento di associazione dell'asserzione di criteri personalizzata.  
  
2.  Aggiungere l'estensione dell'elemento di associazione al file di configurazione utilizzando l'elemento [\<bindingElementExtensions\>](../../../../docs/framework/configure-apps/file-schema/wcf/bindingelementextensions.md).  
  
3.  Compilare un'associazione personalizzata utilizzando <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName>.  
  
### Per inserire un elemento di associazione a livello di programmazione  
  
1.  Creare un nuovo elemento <xref:System.ServiceModel.Channels.BindingElement?displayProperty=fullName> e aggiungerlo a <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName>.  
  
2.  Aggiungere l'associazione personalizzata di cui al passaggio 1a un endpoint nuovo e aggiungere tale nuovo endpoint del servizio all'oggetto <xref:System.ServiceModel.ServiceHost?displayProperty=fullName> chiamando il metodo <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A>.  
  
3.  Aprire l'elemento <xref:System.ServiceModel.ServiceHost>.Nell'esempio di codice seguente sono mostrati la creazione di un'associazione personalizzata e l'inserimento degli elementi dell'associazione a livello di programmazione.  
  
     [!code-csharp[s_imperative#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_imperative/cs/service.cs#1)]
     [!code-vb[s_imperative#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_imperative/vb/service.vb#1)]  
  
## Vedere anche  
 <xref:System.ServiceModel.Description.IPolicyImportExtension>   
 <xref:System.ServiceModel.Description.IPolicyExportExtension>   
 [Procedura: importare asserzioni di criteri personalizzati](../../../../docs/framework/wcf/extending/how-to-import-custom-policy-assertions.md)