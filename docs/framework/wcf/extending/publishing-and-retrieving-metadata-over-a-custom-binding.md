---
title: "Pubblicazione e recupero di metadati su un&#39;associazione personalizzata | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 904e11b4-d90e-45c6-9ee5-c3472c90008c
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Pubblicazione e recupero di metadati su un&#39;associazione personalizzata
La classe <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> fornisce supporto per l'aggiunta di endpoint dei metadati a un servizio.Tali endpoint dei metadati possono rispondere a richieste GET HTTP a un URL che presenta un querystring `?wsdl` e a richieste GET WS\-Transfer come definito nella specifica WS\-MetadataExchange \(MEX\).Gli endpoint MEX implementano il contratto <xref:System.ServiceModel.Description.IMetadataExchange?displayProperty=fullName>.  
  
## Pubblicazione di metadati su un'associazione personalizzata  
 Gli endpoint di metadati GET di HTTP e di HTTPS vengono attivati impostando le proprietà <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A?displayProperty=fullName> o <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A?displayProperty=fullName> su `true`.Non è possibile configurare le associazioni per questi endpoint.  
  
 Il contratto <xref:System.ServiceModel.Description.IMetadataExchange>, tuttavia, può essere utilizzato con qualsiasi endpoint, compresi gli endpoint che utilizzano associazioni personalizzate, poiché gli endpoint <xref:System.ServiceModel.Description.IMetadataExchange> sono identici a qualsiasi altro endpoint del servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Se si sa come modificare la configurazione di un'associazione fornita dal sistema o come configurare un elemento <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName>, è possibile configurare un'associazione da utilizzare con un endpoint <xref:System.ServiceModel.Description.IMetadataExchange>.  
  
## Recupero di metadati su un'associazione personalizzata  
 I metadati possono essere recuperati da endpoint di metadati Get HTTP e Get HTTPS utilizzando richieste GET HTTP o HTTPS standard.  
  
 Per recuperare metadati da un endpoint di metadati MEX è generalmente possibile utilizzare una delle associazioni MEX standard supportate in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]<xref:System.ServiceModel.Description.MetadataExchangeBindings?displayProperty=fullName>.Il tipo <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=fullName> e lo strumento Svcutil.exe consentono di selezionare automaticamente una di queste associazioni MEX standard in base all'indirizzo dell'endpoint dei metadati specificato.  
  
 Se un endpoint di metadati MEX utilizza un'associazione diversa dalle associazioni MEX standard, è possibile configurare l'associazione utilizzata da <xref:System.ServiceModel.Description.MetadataExchangeClient> mediante codice o fornendo una configurazione dell'endpoint del client <xref:System.ServiceModel.Description.IMetadataExchange>.Lo strumento Svcutil.exe carica automaticamente dal file di configurazione una configurazione dell'endpoint del client <xref:System.ServiceModel.Description.IMetadataExchange> che ha lo stesso nome dello schema URI per l'indirizzo dell'endpoint dei metadati.  
  
## Protezione  
 Quando si pubblicano metadati su un'associazione personalizzata, accertarsi che l'associazione fornisca il supporto di sicurezza necessario per i metadati.Per impedire la diffusione di informazioni, ad esempio, e fare in modo che il client sia autorizzato a ottenere i metadati, è possibile rendere più protetti i metadati e l'applicazione configurando l'endpoint <xref:System.ServiceModel.Description.IMetadataExchange> perché richieda l'autenticazione e la crittografia.Nell'esempio [Endpoint di metadati protetto personalizzato](../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md) viene illustrato questo scenario.  
  
## Vedere anche  
 [Protezione dei servizi](../../../../docs/framework/wcf/securing-services.md)   
 [Associazioni WS\-MetadataExchange](../../../../docs/framework/wcf/extending/ws-metadataexchange-bindings.md)   
 [Procedura: configurare un'associazione WS\-Metadata Exchange personalizzata](../../../../docs/framework/wcf/extending/how-to-configure-a-custom-ws-metadata-exchange-binding.md)   
 [Procedura: recuperare metadati attraverso un'associazione non MEX](../../../../docs/framework/wcf/extending/how-to-retrieve-metadata-over-a-non-mex-binding.md)