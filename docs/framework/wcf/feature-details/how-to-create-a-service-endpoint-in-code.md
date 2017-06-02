---
title: "Procedura: creare un endpoint del servizio nel codice | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3fbb22fa-2930-48b8-b437-def1de87c6a0
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Procedura: creare un endpoint del servizio nel codice
In questo esempio viene definito un contratto `ICalculator` per un servizio di calcolatrice. Il servizio viene implementato nella classe `CalculatorService` e il relativo endpoint viene quindi definito in codice, dove si specifica che il servizio deve utilizzare la classe <xref:System.ServiceModel.BasicHttpBinding>.  
  
 La procedura in genere consigliata consiste nello specificare le informazioni su associazione e indirizzo nella configurazione in modo dichiarativo anziché in modo imperativo nel codice.La definizione di endpoint nel codice non è generalmente pratica perché le associazioni e gli indirizzi per un servizio distribuito sono solitamente diversi da quelli utilizzati durante lo sviluppo del servizio.Più in generale, se l'associazione e le informazioni di indirizzo vengono tenute all'esterno del codice, possono cambiare senza che sia necessario ricompilare o ridistribuire l'applicazione.  
  
#### Per creare un endpoint del servizio nel codice  
  
1.  Creare l'interfaccia che definisce il contratto di servizio.  
  
     [!code-csharp[c_HowTo_CodeServiceBinding#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#1)]
     [!code-vb[c_HowTo_CodeServiceBinding#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#1)]  
  
2.  Implementare il contratto di servizio definito nel passaggio 1.  
  
     [!code-csharp[c_HowTo_CodeServiceBinding#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#2)]
     [!code-vb[c_HowTo_CodeServiceBinding#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#2)]  
  
3.  Nell'applicazione host, creare l'indirizzo di base del servizio e l'associazione da utilizzare con il servizio.  
  
     [!code-csharp[c_HowTo_CodeServiceBinding#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#3)]
     [!code-vb[c_HowTo_CodeServiceBinding#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#3)]  
  
4.  Creare l'host e chiamare <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%28System.Type%2CSystem.ServiceModel.Channels.Binding%2CSystem.String%29> o uno degli altri overload per aggiungere l'endpoint del servizio per l'host.  
  
     [!code-csharp[c_HowTo_CodeServiceBinding#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#6)]
     [!code-vb[c_HowTo_CodeServiceBinding#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#6)]  
  
     Per specificare l'associazione nel codice senza utilizzare gli endpoint predefiniti forniti dal runtime, passare l'indirizzo di base al costruttore durante la creazione di <xref:System.ServiceModel.ServiceHost> e non chiamare <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A>.  
  
     [!code-csharp[c_HowTo_CodeServiceBinding#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#7)]
     [!code-vb[c_HowTo_CodeServiceBinding#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#7)]  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)] endpoint predefiniti, vedere [Configurazione semplificata](../../../../docs/framework/wcf/simplified-configuration.md) e [Configurazione semplificata per servizi WCF](../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
## Vedere anche  
 [Procedura: specificare un'associazione al servizio in codice](../../../../docs/framework/wcf/how-to-specify-a-service-binding-in-code.md)