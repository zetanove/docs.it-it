---
title: "Procedura: consentire richieste di metadati durante l&#39;autorizzazione | Microsoft Docs"
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
  - "consenso alle richieste di metadati durante l'autorizzazione [WCF]"
ms.assetid: 90cec34f-b619-452b-a056-8b1c0de49d05
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Procedura: consentire richieste di metadati durante l&#39;autorizzazione
Durante l'autorizzazione personalizzata potrebbe essere necessario consentire l'elaborazione di una richiesta di metadati.Nell'argomento seguente vengono dettagliati i passaggi necessari per convalidare tale richiesta.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] sull'autorizzazione, vedere [Autorizzazione](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md).  
  
### Per consentire richieste di metadati durante l'autorizzazione  
  
1.  Creare un'estensione della classe <xref:System.ServiceModel.ServiceAuthorizationManager>.  
  
2.  Eseguire l'override del metodo <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A>.Il metodo restituisce `true` o `false` rispettivamente se l'autorizzazione è consentita o meno.Le informazioni sulla procedura corrente sono reperibili in <xref:System.ServiceModel.OperationContext> passato come parametro al metodo.  
  
3.  Durante l'override controllare il nome del contratto, lo spazio dei nomi e l'azione, come indicato nell'esempio seguente.Se le condizioni sono valide, restituire `true.`.  
  
4.  Utilizzare il punto di estendibilità per utilizzare la classe.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Procedura: creare un gestore autorizzazioni personalizzato per un servizio](../../../../docs/framework/wcf/extending/how-to-create-a-custom-authorization-manager-for-a-service.md).  
  
## Esempio  
 Nell'esempio seguente viene illustrato un override del metodo <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A>.  
  
 [!code-csharp[C_HowtoCheckForMexRequestsInAuthorization#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtocheckformexrequestsinauthorization/cs/source.cs#1)]
 [!code-vb[C_HowtoCheckForMexRequestsInAuthorization#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtocheckformexrequestsinauthorization/vb/source.vb#1)]  
  
## Vedere anche  
 <xref:System.ServiceModel.ServiceAuthorizationManager>   
 [Autorizzazione](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)   
 [Gestione di attestazioni e autorizzazioni con il modello di identità](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)