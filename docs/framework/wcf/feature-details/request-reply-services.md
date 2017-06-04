---
title: "Servizi request/reply | Microsoft Docs"
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
  - "contratti [WCF], servizi request/reply"
  - "contratti request/reply [WCF]"
  - "WCF [WCF], servizi request/reply"
  - "Windows Communication Foundation [WCF], servizi request/reply"
ms.assetid: 2fa710f1-47f4-4598-b063-3ab3bd22ebba
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Servizi request/reply
I servizi request\/reply sono il tipo predefinito di contratto dell'operazione in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].I client effettuano chiamate alle operazioni del servizio e attendono una risposta dal servizio.È possibile effettuare chiamate a un'operazione del servizio in modo sincrono o asincrono. Nel primo caso, il client si blocca finché non riceve una risposta dal servizio o la chiamata scade, mentre nel secondo caso il client esegue una chiamata all'operazione del servizio, continua a funzionare e riceve la risposta dal servizio su un altro thread.  
  
 Per creare un contratto di servizio request\/reply, definirlo e applicare la classe <xref:System.ServiceModel.OperationContractAttribute> a ogni operazione, come illustrato nel codice di esempio seguente.  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IRequestReplyCalculator  
{  
    [OperationContract]  
    double Add(double n1, double n2);  
}  
  
```  
  
 Non è necessario impostare la proprietà <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> su `false` perché questo è il comportamento predefinito.  
  
## Vedere anche  
 [Servizi unidirezionali](../../../../docs/framework/wcf/feature-details/one-way-services.md)   
 [Servizi duplex](../../../../docs/framework/wcf/feature-details/duplex-services.md)