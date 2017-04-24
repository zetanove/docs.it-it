---
title: "Procedura: controllare o modificare i parametri | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ab6c0ac7-aac4-45ba-93d6-a0e9afd1756f
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Procedura: controllare o modificare i parametri
È possibile ispezionare o modificare i messaggi in ingresso o in uscita per una singola operazione su un [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] oggetto client o un [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] servizio implementando il <xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=fullName> interfaccia e inserendola nel runtime del client o servizio. In genere, viene utilizzato un comportamento dell'operazione per aggiungere controlli del parametro per una singola operazione; è tuttavia possibile utilizzare altri comportamenti per fornire facile accesso al runtime per un ambito più vasto. Per ulteriori informazioni, vedere [estensione client](../../../../docs/framework/wcf/extending/extending-clients.md) e [estensione dispatcher](../../../../docs/framework/wcf/extending/extending-dispatchers.md).  
  
### <a name="inspecting-or-modifying-parameters"></a>Controllo o modifica di parametri  
  
1.  Implementare il <xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=fullName> interfaccia.  
  
2.  Implementare un <xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=fullName>, <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=fullName>, <xref:System.ServiceModel.Description.IServiceBehavior?displayProperty=fullName> o <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=fullName> (a seconda dell'ambito richiesto) per aggiungere il controllo del parametro a uno di <xref:System.ServiceModel.Dispatcher.ClientOperation.ParameterInspectors%2A?displayProperty=fullName> o <xref:System.ServiceModel.Dispatcher.DispatchOperation.ParameterInspectors%2A?displayProperty=fullName> proprietà.  
  
3.  Inserire il comportamento prima di chiamare <xref:System.ServiceModel.ClientBase%601.Open%2A?displayProperty=fullName> o <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=fullName> metodo il <xref:System.ServiceModel.ChannelFactory%601?displayProperty=fullName>. Per informazioni dettagliate, vedere [configurazione ed estensione del Runtime con comportamenti](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md).  
  
## <a name="example"></a>Esempio  
 Negli esempi di codice seguenti vengono illustrati, nell'ordine:  
  
-   L'implementazione di un controllo del parametro.  
  
-   L'implementazione del comportamento che inserisce il controllo del parametro mediante un <xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=fullName>, <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=fullName>e un <xref:System.ServiceModel.Description.IServiceBehavior?displayProperty=fullName>.  
  
-   Un file di configurazione che carica ed esegue il comportamento dell'endpoint in un'applicazione client per inserire il controllo del parametro sul client.  
  
 [!code-csharp[Interceptors#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/interceptors.cs#4)]
 [!code-vb[Interceptors#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/interceptors.vb#4)]  
  
 [!code-csharp[Interceptors#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/insertingbehaviors.cs#5)]
 [!code-vb[Interceptors#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/insertingbehaviors.vb#5)]  
  
 <!-- TODO: review snippet reference [!code[Interceptors#3](../../../../samples/snippets/common/VS_Snippets_CFX/interceptors/common/client.exe.config#3)]  -->
 <!-- TODO: review snippet reference [!code-csharp[Interceptors#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/client.exe.config#3)]  -->
 <!-- TODO: review snippet reference [!code-vb[Interceptors#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/client.exe.config#3)]  -->  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione ed estensione del Runtime con comportamenti](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)