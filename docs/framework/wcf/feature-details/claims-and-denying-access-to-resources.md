---
title: "Attestazioni e negazioni di accesso alle risorse | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "attestazioni [WCF], negazione di accesso alle risorse"
ms.assetid: 145ebb41-680e-4256-b14c-1efb4af1e982
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Attestazioni e negazioni di accesso alle risorse
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] supporta un meccanismo di autorizzazione basato su attestazioni.Così come consentono l'accesso alle risorse in base alla presenza di attestazioni, i sistemi spesso negano l'accesso alle risorse in base alla presenza di attestazioni.Tali sistemi devono esaminare la classe <xref:System.IdentityModel.Policy.AuthorizationContext> per rilevare la presenza di attestazioni che causano la negazione dell'accesso prima di ricercare le attestazioni che causano la concessione dell'accesso.  
  
 Ad esempio, un sistema potrebbe negare l'accesso a una risorsa a chiunque disponga di un'attestazione di tipo `Age`, un diritto <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A> e un valore di risorsa `Under 21` solo quando tale identità dispone anche di un'attestazione di tipo `Name`, un diritto <xref:System.IdentityModel.Claims.Rights.Identity%2A> e un valore di risorsa `Mallory`.In altri termini, il sistema nega l'accesso a chiunque abbia meno di 21 anni e lo concede quando il nome è Mallory.Per implementare correttamente questa semantica, è importante ricercare prima l'attestazione `Age` e determinare se l'età è inferiore ai 21 anni.In caso contrario, se Mallory ha meno di 21 anni, l'accesso alla risorsa potrebbe essere concesso unicamente sulla base dell'attestazione `Name`.  
  
## Vedere anche  
 [Gestione di attestazioni e autorizzazioni con il modello di identità](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)   
 [Attestazioni e token](../../../../docs/framework/wcf/feature-details/claims-and-tokens.md)