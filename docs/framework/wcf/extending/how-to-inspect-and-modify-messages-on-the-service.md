---
title: "Procedura: ispezionare e modificare i messaggi sul servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9c5b1cc7-84f3-45f8-9226-d59c278e8c42
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Procedura: ispezionare e modificare i messaggi sul servizio
È possibile ispezionare o modificare i messaggi in ingresso o in uscita su un [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] client implementando un <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=fullName> e inserendola nel runtime del servizio. Per ulteriori informazioni, vedere [estensione dispatcher](../../../../docs/framework/wcf/extending/extending-dispatchers.md). La funzionalità equivalente nel servizio è il <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=fullName>.  
  
### <a name="to-inspect-or-modify-messages"></a>Per ispezionare o modificare i messaggi  
  
1.  Implementare il <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=fullName> interfaccia.  
  
2.  Implementare un <xref:System.ServiceModel.Description.IServiceBehavior?displayProperty=fullName>, <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=fullName>, o <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=fullName> interfaccia in base all'ambito in cui si desidera inserire facilmente il controllo dei messaggi del servizio.  
  
3.  Inserire il comportamento prima di chiamare il <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=fullName> metodo il <xref:System.ServiceModel.ServiceHost?displayProperty=fullName>. Per informazioni dettagliate, vedere [configurazione ed estensione del Runtime con comportamenti](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md).  
  
## <a name="example"></a>Esempio  
 Negli esempi di codice seguenti vengono illustrati, nell'ordine:  
  
-   Un'implementazione del controllo del servizio.  
  
-   Un comportamento del servizio che inserisce il controllo.  
  
-   Un file di configurazione che carica ed esegue il comportamento in un'applicazione del servizio.  
  
 [!code-csharp[Interceptors#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/interceptors.cs#7)]
 [!code-vb[Interceptors#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/interceptors.vb#7)]  
  
 [!code-csharp[Interceptors#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/insertingbehaviors.cs#8)]
 [!code-vb[Interceptors#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/insertingbehaviors.vb#8)]  
  
 <!-- TODO: review snippet reference [!code[Interceptors#9](../../../../samples/snippets/common/VS_Snippets_CFX/interceptors/common/hostapplication.exe.config#9)]  -->
 <!-- TODO: review snippet reference [!code-csharp[Interceptors#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/hostapplication.exe.config#9)]  -->
 <!-- TODO: review snippet reference [!code-vb[Interceptors#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/hostapplication.exe.config#9)]  -->  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=fullName>   
 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=fullName>   
 [Configurazione ed estensione del Runtime con comportamenti](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)