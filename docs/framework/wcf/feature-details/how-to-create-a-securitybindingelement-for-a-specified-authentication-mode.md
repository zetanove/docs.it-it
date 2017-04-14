---
title: "Procedura: creare un elemento SecurityBindingElement per una modalit&#224; di autenticazione specificata | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a7c7747a-5b8c-463f-8493-7266dac75066
caps.latest.revision: 9
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 9
---
# Procedura: creare un elemento SecurityBindingElement per una modalit&#224; di autenticazione specificata
In [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] sono disponibili varie modalità per l'autenticazione reciproca di client e servizi.È possibile creare elementi di associazione di sicurezza per tali modalità di autenticazione utilizzando metodi statici sulla classe <xref:System.ServiceModel.Channels.SecurityBindingElement> o tramite configurazione, come spiegato nell'esempio seguente.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sulle 18 modalità di autenticazione, vedere [Modalità di autenticazione di SecurityBindingElement](../../../../docs/framework/wcf/feature-details/securitybindingelement-authentication-modes.md).  
  
## Esempio  
 Nell'esempio di codice seguente sono illustrati i metodi per la creazione di associazioni per le varie modalità di autenticazione.  
  
> [!NOTE]
>  Dopo la creazione di un'istanza dell'oggetto <xref:System.ServiceModel.Channels.SecurityBindingElement>, diverse proprietà sono immutabili, ad esempio <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters.KeyType%2A> e <xref:System.ServiceModel.Channels.SecurityBindingElement.MessageSecurityVersion%2A>.Non cambiano neppure chiamando `set` su di esse.  
  
 [!code-csharp[c_CustomBindingsAuthMode#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombindingsauthmode/cs/source.cs#2)]
 [!code-vb[c_CustomBindingsAuthMode#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_custombindingsauthmode/vb/source.vb#2)]  
  
## Vedere anche  
 [Modalità di autenticazione di SecurityBindingElement](../../../../docs/framework/wcf/feature-details/securitybindingelement-authentication-modes.md)   
 [Procedura: creare un'associazione personalizzata utilizzando SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)