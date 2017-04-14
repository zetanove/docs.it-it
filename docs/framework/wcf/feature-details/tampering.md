---
title: "Manomissioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3bad93be-60bb-4f89-96ab-a1c3dc7c0fad
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Manomissioni
Il termine *manomissione* indica l'azione con cui si modifica un messaggio o il suo recapito e si utilizza il messaggio modificato a fini diversi da quelli per cui è stato creato.  
  
## Non disattivare WS\-Addressing  
 La specifica WS\-Addressing fornisce intestazioni di indirizzo in ogni messaggio, consentendo a un destinatario di verificare il mittente del messaggio.È possibile disattivare questa funzionalità impostando la proprietà <xref:System.ServiceModel.Channels.MessageVersion.Addressing%2A> su <xref:System.ServiceModel.Channels.AddressingVersion.None%2A>.  
  
 Quando la modalità di sicurezza è impostata su Message, e se WS\-Addressing è disattivato, l'autore di un attacco può prendere una richiesta da un client e inviarla a un altro servizio che non ha modo di rilevare se il messaggio proviene dal client originale.In effetti, il primo servizio può fingere di essere un client durante la comunicazione con il secondo servizio.  
  
 Per limitare questo problema, non impostare mai la proprietà <xref:System.ServiceModel.Channels.MessageVersion.Addressing%2A> su <xref:System.ServiceModel.Channels.AddressingVersion.None%2A> ed evitare l'utilizzo di <xref:System.ServiceModel.Channels.MessageVersion>, ad esempio la proprietà statica <xref:System.ServiceModel.Channels.MessageVersion.Soap12%2A>, che imposta la proprietà <xref:System.ServiceModel.Channels.MessageVersion.Addressing%2A> su <xref:System.ServiceModel.Channels.AddressingVersion.None%2A>.  
  
## Vedere anche  
 [Considerazioni sulla sicurezza](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)   
 [Diffusione di informazioni](../../../../docs/framework/wcf/feature-details/information-disclosure.md)   
 [Elevazione dei privilegi](../../../../docs/framework/wcf/feature-details/elevation-of-privilege.md)   
 [Denial of Service \(Negazione del servizio\)](../../../../docs/framework/wcf/feature-details/denial-of-service.md)   
 [Scenari non supportati](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)   
 [Attacchi di tipo replay](../../../../docs/framework/wcf/feature-details/replay-attacks.md)