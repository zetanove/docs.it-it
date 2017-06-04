---
title: "Recupero dei metadati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "metadati [WCF], recupero"
ms.assetid: 18d8ba4c-af0f-4827-a50b-4202d767bacc
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Recupero dei metadati
Il recupero dei metadati è il processo di richiesta e di recupero dei metadati da un endpoint di metadati, ad esempio un endpoint di metadati WS\-MetadataExchange \(MEX\) o un endpoint di metadati HTTP\/GET.  
  
## Recupero dei metadati dalla riga di comando utilizzando Svcutil.exe  
 È possibile recuperare i metadati del servizio utilizzando richieste WS\-MetadataExchange o HTTP\/GET mediante lo strumento [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) passando l'opzione `/target:metadata` e un indirizzo.Svcutil.exe scarica i metadati all'indirizzo specificato e salva il file su disco.Lo strumento utilizza internamente un'istanza <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> e carica dalla configurazione la configurazione dell'endpoint <xref:System.ServiceModel.Description.IMetadataExchange> il cui nome corrisponde allo schema dell'indirizzo passato a Svcutil.exe come input.  
  
## Recupero dei metadati a livello di codice utilizzando MetadataExchangeClient  
 In[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] è possibile recuperare i metadati del servizio utilizzando protocolli standard, ad esempio richieste WS\-MetadataExchange e HTTP\/GET.Entrambi questi protocolli sono supportati dal tipo <xref:System.ServiceModel.Description.MetadataExchangeClient>.Per recuperare i metadati del servizio, utilizzare il tipo <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> fornendo un indirizzo per l'endpoint dei metadati e un'associazione facoltativa.L'associazione utilizzata da un'istanza <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> può essere una delle associazioni predefinite della classe statica <xref:System.ServiceModel.Description.MetadataExchangeBindings>, un'associazione fornita dall'utente o un'associazione caricata dalla configurazione dell'endpoint per il contratto `IMetadataExchange`.<xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> può inoltre risolvere i riferimenti dell'URL HTTP ai metadati utilizzando il tipo <xref:System.Net.HttpWebRequest>.  
  
 Per impostazione predefinita, un'istanza <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> è collegata a una sola istanza <xref:System.ServiceModel.ChannelFactory>.È possibile modificare o sostituire l'istanza <xref:System.ServiceModel.ChannelFactory?displayProperty=fullName> utilizzata da <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> eseguendo l'override del metodo virtuale <xref:System.ServiceModel.Description.MetadataExchangeClient.GetChannelFactory%2A>.Analogamente, è possibile modificare o sostituire l'istanza <xref:System.Net.HttpWebRequest> utilizzata da <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> per le richieste HTTP\/GET eseguendo l'override del metodo virtuale <xref:System.ServiceModel.Description.MetadataExchangeClient.GetWebRequest%2A?displayProperty=fullName>.  
  
## Argomenti della sezione  
 [Procedura: utilizzare Svcutil.exe per scaricare documenti di metadati](../../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-download-metadata-documents.md)  
 Viene illustrato come utilizzare Svcutil.exe per scaricare documenti di metadati  
  
 [Procedura: utilizzare la classe MetadataResolver per ottenere dinamicamente i metadati di associazione](../../../../docs/framework/wcf/feature-details/how-to-use-metadataresolver-to-obtain-binding-metadata-dynamically.md)  
 Viene illustrato come utilizzare <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=fullName> per ottenere dinamicamente i metadati di associazione a runtime.  
  
 [Procedura: utilizzare MetadataExchangeClient per il recupero di metadati](../../../../docs/framework/wcf/feature-details/how-to-use-metadataexchangeclient-to-retrieve-metadata.md)  
 Viene illustrato come utilizzare la classe <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> per scaricare file di metadati in un oggetto <xref:System.ServiceModel.Description.MetadataSet?displayProperty=fullName> contenente oggetti <xref:System.ServiceModel.Description.MetadataSection?displayProperty=fullName> per la scrittura nei file o per altri utilizzi.  
  
## Vedere anche  
 <xref:System.ServiceModel.Description.MetadataExchangeClient>