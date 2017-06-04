---
title: "Procedura: creare un contratto Windows Communication Foundation con una classe | Microsoft Docs"
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
ms.assetid: 1ad69393-3915-4e7f-9b91-b6fc59c6f5ba
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# Procedura: creare un contratto Windows Communication Foundation con una classe
La modalità preferita per creare un contratto [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] è tramite un'interfaccia.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Procedura: definire il contratto di servizio](../../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md).Un'alternativa, illustrata qui, consiste nel creare una classe e quindi nell'applicare l'attributo <xref:System.ServiceModel.ServiceContractAttribute> direttamente alla classe e l'attributo <xref:System.ServiceModel.OperationContractAttribute> a ognuno dei metodi nella classe che fanno parte del contratto.  
  
> [!WARNING]
>  `[ServiceContract]` e `[ServiceContractAttribute]` eseguono la stessa operazione.La stessa situazione è valida per `[OperationContract]` e `[OperationContractAttribute]`.In ogni caso il primo è l'abbreviazione del secondo.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sui contratti di servizio, vedere [Progettazione dei contratti di servizio](../../../../docs/framework/wcf/designing-service-contracts.md).  
  
### Creazione di un contratto Windows Communication Foundation con una classe  
  
1.  Creare una nuova classe utilizzando [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)], C\# o qualsiasi altro linguaggio Common Language Runtime.  
  
2.  Applicare la classe <xref:System.ServiceModel.ServiceContractAttribute> alla classe.  
  
3.  Creare metodi nella classe.  
  
4.  Applicare la classe <xref:System.ServiceModel.OperationContractAttribute> a ogni metodo che deve essere esposto come parte del contratto [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] pubblico.  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrata una classe che definisce un contratto di servizio.  
  
 [!code-csharp[c_HowTo_CreateContractWithClass#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createcontractwithclass/cs/source.cs#1)]
 [!code-vb[c_HowTo_CreateContractWithClass#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_createcontractwithclass/vb/source.vb#1)]  
  
 I metodi a cui è applicata la classe <xref:System.ServiceModel.OperationContractAttribute> utilizzano per impostazione predefinita un modello di messaggio request\/reply.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] questo modello di messaggio, vedere [Procedura: creare un contratto request\/reply](../../../../docs/framework/wcf/feature-details/how-to-create-a-request-reply-contract.md).È anche possibile creare e utilizzare altri modelli di messaggio impostando proprietà dell'attributo.Per ulteriori esempi, vedere [Procedura: creare un contratto unidirezionale](../../../../docs/framework/wcf/feature-details/how-to-create-a-one-way-contract.md) e [Procedura: creare un contratto duplex](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md).  
  
## Vedere anche  
 <xref:System.ServiceModel.ServiceContractAttribute>   
 <xref:System.ServiceModel.OperationContractAttribute>