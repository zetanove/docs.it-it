---
title: "Procedura: creare un contratto unidirezionale | Microsoft Docs"
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
ms.assetid: 85084cd9-31cc-4e95-b667-42ef01336622
caps.latest.revision: 23
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 23
---
# Procedura: creare un contratto unidirezionale
In questo argomento vengono illustrati i passaggi di base per creare metodi che utilizzano un contratto unidirezionale.Tali metodi richiamano operazioni in un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] da un client senza però aspettarsi una risposta.Questo tipo di contratto può essere utilizzato, ad esempio, per pubblicare notifiche a numerosi sottoscrittori.È anche possibile utilizzare contratti unidirezionali durante la creazione di un contratto duplex \(bidirezionale\) che consente ai client e ai server di comunicare fra loro indipendentemente in modo che uno sia in grado di avviare chiamate all'altro.In particolare, questo può consentire al server di eseguire chiamate unidirezionali al client che vengono trattate da quest'ultimo come eventi.Per informazioni dettagliate sulla specifica di metodi bidirezionali, vedere la proprietà <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> e la classe <xref:System.ServiceModel.OperationContractAttribute>.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sulla creazione di un'applicazione client per un contratto duplex, vedere [Procedura: accedere a servizi con un contratto unidirezionale o request\/reply](../../../../docs/framework/wcf/feature-details/how-to-access-wcf-services-with-one-way-and-request-reply-contracts.md).Per un esempio funzionante, vedere [Unidirezionale](../../../../docs/framework/wcf/samples/one-way.md).  
  
### Per creare un contratto unidirezionale  
  
1.  Creare il contratto di servizio applicando la classe <xref:System.ServiceModel.ServiceContractAttribute> all'interfaccia e che definisce i metodi del servizio da implementare.  
  
2.  Indicare quali metodi nell'interfaccia possono essere chiamati da un client applicando loro la classe <xref:System.ServiceModel.OperationContractAttribute>.  
  
3.  Designare operazioni che non devono avere output \(nessun valore restituito e nessun parametro out o ref\) di tipo unidirezionale impostando la proprietà <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> su `true`.Notare che le operazioni che contengono la classe <xref:System.ServiceModel.OperationContractAttribute> soddisfano per impostazione predefinita un contratto request\/reply perché la proprietà <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> è `false` per impostazione predefinita.Pertanto, se si desidera un contratto unidirezionale per il metodo, è necessario specificare in modo esplicito il valore della proprietà dell'attributo in modo che sia `true`.  
  
## Esempio  
 Nell'esempio di codice seguente viene definito un contratto per un servizio che include alcuni metodi unidirezionali.Tutti i metodi contengono contratti unidirezionali eccetto `Equals` la cui impostazione predefinita è request\/reply e restituisce un risultato.  
  
 [!code-csharp[S_Service_Session#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_service_session/cs/service.cs#1)]
 [!code-vb[S_Service_Session#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_service_session/vb/service.vb#1)]  
  
## Vedere anche  
 <xref:System.ServiceModel.ServiceContractAttribute>   
 <xref:System.ServiceModel.OperationContractAttribute>   
 [Progettazione e implementazione di servizi](../../../../docs/framework/wcf/designing-and-implementing-services.md)   
 [Procedura: definire il contratto di servizio](../../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md)   
 [Sessione](../../../../docs/framework/wcf/samples/session.md)   
 [Procedura: creare un contratto duplex](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)