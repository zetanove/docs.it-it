---
title: "Procedura: creare un servizio con un&#39;interfaccia di contratto | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7b6803f6-d6f9-4cc2-9f1b-6f4c920475d5
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Procedura: creare un servizio con un&#39;interfaccia di contratto
La modalità preferita per creare un contratto [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] è tramite un'interfaccia.Questo contratto specifica la raccolta e la struttura dei messaggi necessari per accedere alle operazioni offerte dal servizio.Questa interfaccia definisce i tipi di input e output applicando la classe <xref:System.ServiceModel.ServiceContractAttribute> all'interfaccia e la classe <xref:System.ServiceModel.OperationContractAttribute> ai metodi che si desidera esporre.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sui contratti di servizio, vedere [Progettazione dei contratti di servizio](../../../../docs/framework/wcf/designing-service-contracts.md).  
  
### Creazione di un contratto WCF con un'interfaccia  
  
1.  Creare una nuova interfaccia utilizzando [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)], C\# o qualsiasi altro linguaggio Common Language Runtime.  
  
2.  Applicare la classe <xref:System.ServiceModel.ServiceContractAttribute> all'interfaccia.  
  
3.  Definire i metodi nell'interfaccia.  
  
4.  Applicare la classe <xref:System.ServiceModel.OperationContractAttribute> a ogni metodo che deve essere esposto come parte del contratto [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] pubblico.  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrata un'interfaccia che definisce un contratto di servizio.  
  
 [!code-csharp[c_HowTo_CreateContractWithInterface#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createcontractwithinterface/cs/source.cs#1)]
 [!code-vb[c_HowTo_CreateContractWithInterface#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_createcontractwithinterface/vb/source.vb#1)]  
  
 I metodi a cui è applicata la classe <xref:System.ServiceModel.OperationContractAttribute> utilizzano per impostazione predefinita un modello di messaggio request\/reply.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] questo modello di messaggio, vedere [Procedura: creare un contratto request\/reply](../../../../docs/framework/wcf/feature-details/how-to-create-a-request-reply-contract.md).È anche possibile creare e utilizzare altri modelli di messaggio impostando proprietà dell'attributo.Per ulteriori esempi, vedere [Procedura: creare un contratto unidirezionale](../../../../docs/framework/wcf/feature-details/how-to-create-a-one-way-contract.md) e [Procedura: creare un contratto duplex](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md).  
  
## Vedere anche  
 <xref:System.ServiceModel.ServiceContractAttribute>   
 <xref:System.ServiceModel.OperationContractAttribute>