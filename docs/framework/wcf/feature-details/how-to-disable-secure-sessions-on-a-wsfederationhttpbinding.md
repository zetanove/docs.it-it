---
title: "Procedura: disattivare sessioni protette in un&#39;associazione WSFederationHttpBinding | Microsoft Docs"
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
  - "federazione"
  - "WCF, federazione"
ms.assetid: 675fa143-6a4e-4be3-8afc-673334ab55ec
caps.latest.revision: 16
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 16
---
# Procedura: disattivare sessioni protette in un&#39;associazione WSFederationHttpBinding
Alcuni servizi possono richiedere credenziali federate senza tuttavia supportare le sessioni protette.In questo caso occorre disattivare la funzionalità di sessione protetta.A differenza della classe <xref:System.ServiceModel.WsHttpBinding>, la classe <xref:System.ServiceModel.WSFederationHttpBinding> non fornisce alcuna modalità di disattivazione delle sessioni protette quando si comunica con un servizio.È invece necessario creare un'associazione personalizzata che sostituisce le impostazioni della sessione protetta con un bootstrap.  
  
 Questo argomento illustra come modificare gli elementi di un'associazione <xref:System.ServiceModel.WSFederationHttpBinding> per creare un'associazione personalizzata.Il risultato è un'associazione <xref:System.ServiceModel.WSFederationHttpBinding> uguale all'originale in cui tuttavia non vengono utilizzate sessioni protette.  
  
### Per creare un'associazione federata personalizzata senza sessioni protette  
  
1.  Creare un'istanza della classe <xref:System.ServiceModel.WSFederationHttpBinding> o in modo imperativo nel codice oppure caricando un'associazione di questo tipo dal file di configurazione.  
  
2.  Duplicare l'associazione <xref:System.ServiceModel.WSFederationHttpBinding> in un'associazione <xref:System.ServiceModel.Channels.CustomBinding>.  
  
3.  Individuare l'elemento <xref:System.ServiceModel.Channels.SecurityBindingElement> all'interno dell'associazione <xref:System.ServiceModel.Channels.CustomBinding>.  
  
4.  Individuare l'elemento <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters> all'interno dell'associazione <xref:System.ServiceModel.Channels.SecurityBindingElement>.  
  
5.  Sostituire l'elemento <xref:System.ServiceModel.Channels.SecurityBindingElement> originale con l'elemento di associazione di sicurezza bootstrap ottenuto dai parametri <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters>.  
  
## Esempio  
 Nell'esempio seguente viene creata un'associazione federata personalizzata senza sessioni protette.  
  
 [!code-csharp[c_CustomFederationBinding#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customfederationbinding/cs/c_customfederationbinding.cs#0)]
 [!code-vb[c_CustomFederationBinding#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customfederationbinding/vb/c_customfederationbinding.vb#0)]  
  
## Compilazione del codice  
  
-   Per compilare l'esempio di codice, creare un progetto che fa riferimento all'assembly System.ServiceModel.dll.  
  
## Vedere anche  
 [Associazioni e protezione](../../../../docs/framework/wcf/feature-details/bindings-and-security.md)