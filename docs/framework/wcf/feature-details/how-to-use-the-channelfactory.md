---
title: "Procedura: usare ChannelFactory | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: d48f01b5-582b-4c8b-b547-8adddae7e371
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Procedura: usare ChannelFactory
La classe generica <xref:System.ServiceModel.ChannelFactory%601> viene usata in scenari avanzati che richiedono la creazione di una channel factory utilizzabile per creare più di un canale.  
  
### Per creare e usare la classe ChannelFactory  
  
1.  Creare ed eseguire un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Progettazione e implementazione di servizi](../../../../docs/framework/wcf/designing-and-implementing-services.md), [Configurazione dei servizi](../../../../docs/framework/wcf/configuring-services.md) e [Servizi host](../../../../docs/framework/wcf/hosting-services.md).  
  
2.  Usare lo [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) per generare il contratto \(interfaccia\) per il client.  
  
3.  Nel codice client, usare la classe <xref:System.ServiceModel.ChannelFactory%601> per creare più listener endpoint.  
  
## Esempio  
 [!code-csharp[c_HowToUseChannelFactory#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtousechannelfactory/cs/source.cs#1)]
 [!code-vb[c_HowToUseChannelFactory#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtousechannelfactory/vb/source.vb#1)]