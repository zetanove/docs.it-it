---
title: "Crittografia di firme digitali | Microsoft Docs"
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
  - "firme digitali [WCF]"
  - "firme digitali [WCF], crittografia"
  - "crittografia di firme digitali [WCF]"
ms.assetid: 0868866d-40b4-4341-8e42-eee3b7f15b69
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Crittografia di firme digitali
Per impostazione predefinita, un messaggio viene firmato e crittografato e la firma viene crittografata digitalmente.È possibile controllare questo comportamento creando un'associazione personalizzata con un'istanza della classe <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> o <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> e quindi impostando la proprietà `MessageProtectionOrder` della classe su un valore dell'enumerazione <xref:System.ServiceModel.Security.MessageProtectionOrder>.Il valore predefinito è <xref:System.ServiceModel.Security.MessageProtectionOrder>.Questo processo richiede un tempo superiore dal 10 al 40 percento rispetto alla semplice firma e crittografia.La disattivazione della crittografia della firma può tuttavia consentire all'autore di un attacco di individuare il contenuto del messaggio,poiché l'elemento di firma contiene il codice hash del testo normale di ogni parte firmata del messaggio.Ad esempio, anche se il corpo del messaggio è crittografato per impostazione predefinita, la firma non crittografata contiene il codice hash del corpo del messaggio.Se il messaggio è di piccole dimensioni, l'autore dell'attacco potrebbe essere in grado di dedurre il contenuto.Con la crittografia della firma si riduce o si elimina questa possibilità.  
  
 Disattivare pertanto la crittografia della firma solo quando il valore del contenuto è basso e il miglioramento delle prestazioni sarà significativo, ad esempio in caso di invio di file binari di grandi dimensioni senza implicazioni di sicurezza.  
  
### Per disattivare la firma digitale  
  
1.  Creare una classe <xref:System.ServiceModel.Channels.CustomBinding>.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Procedura: creare un'associazione personalizzata utilizzando SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md).  
  
2.  Aggiungere un elemento <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> o <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> alla raccolta di associazioni.  
  
3.  Impostare la proprietà <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement.MessageProtectionOrder%2A?displayProperty=fullName> su <xref:System.ServiceModel.Security.MessageProtectionOrder> oppure impostare la proprietà <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.MessageProtectionOrder%2A?displayProperty=fullName> su <xref:System.ServiceModel.Security.MessageProtectionOrder>.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] creazione di associazioni personalizzate, vedere [Creazione di associazioni definite dall'utente](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] creazione di un'associazione personalizzata per una modalità di autenticazione specifica, vedere [Procedura: creare un elemento SecurityBindingElement per una modalità di autenticazione specificata](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md).  
  
## Vedere anche  
 <xref:System.ServiceModel.Security.MessageProtectionOrder>   
 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>   
 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>   
 [Procedura: creare un'associazione personalizzata utilizzando SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)   
 [Creazione di associazioni definite dall'utente](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md)   
 [Procedura: creare un elemento SecurityBindingElement per una modalità di autenticazione specificata](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)