---
title: "Procedura: specificare un&#39;associazione al client in codice | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6bee5da4-adf7-42e6-8f78-63a9e5c6dbad
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Procedura: specificare un&#39;associazione al client in codice
Questo esempio illustra un client creato in modo da utilizzare un servizio di calcolatrice. Inoltre, l'associazione a tale client viene specificata in modo imperativo in codice.Il client accede al servizio `CalculatorService` che implementa l'interfaccia `ICalculator`. Sia il servizio sia il client utilizzano la classe <xref:System.ServiceModel.BasicHttpBinding>.  
  
 Questa procedura presuppone che il servizio di calcolatrice sia in esecuzione.Per informazioni sulla compilazione del servizio, vedere [Procedura: specificare un'associazione al servizio in configurazione](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md).Il servizio utilizza inoltre lo strumento [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) fornito da [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] per generare automaticamente i componenti client.Lo strumento genera il codice client di accesso al servizio.  
  
 Il client viene compilato in due parti.Lo strumento Svcutil.exe genera la classe `ClientCalculator` che implementa l'interfaccia `ICalculator`.Questa applicazione client viene quindi costruita creando un'istanza della classe `ClientCalculator` e specificando in codice l'associazione e l'indirizzo del servizio.  
  
 Per l'originale di questo esempio, vedere [BasicBinding](../../../docs/framework/wcf/samples/basicbinding.md).  
  
### Per specificare in codice un'associazione personalizzata  
  
1.  Utilizzare Svcutil.exe dalla riga di comando per generare il codice da metadati del servizio.  
  
    ```  
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>   
    ```  
  
2.  Il client generato contiene l'interfaccia `ICalculator` che definisce il contratto di servizio che l'implementazione del client deve soddisfare.  
  
     [!code-csharp[C_HowTo_CodeClientBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeclientbinding/cs/client.cs#1)]
     [!code-vb[C_HowTo_CodeClientBinding#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeclientbinding/vb/client.vb#1)]  
  
3.  Il client generato contiene inoltre l'implementazione della classe `ClientCalculator`.  
  
     [!code-csharp[C_HowTo_CodeClientBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeclientbinding/cs/client.cs#2)]
     [!code-vb[C_HowTo_CodeClientBinding#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeclientbinding/vb/client.vb#2)]  
  
4.  Creare un'istanza della classe `ClientCalculator` che utilizza la classe <xref:System.ServiceModel.BasicHttpBinding> in un'applicazione client e quindi chiamare le operazioni del servizio all'indirizzo specificato.  
  
     [!code-csharp[C_HowTo_CodeClientBinding#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeclientbinding/cs/client.cs#3)]
     [!code-vb[C_HowTo_CodeClientBinding#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeclientbinding/vb/client.vb#3)]  
  
5.  Compilare ed eseguire il client.  
  
## Vedere anche  
 [Uso di associazioni per configurare servizi e client](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)