---
title: "Negoziazione di sicurezza e timeout | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 02a428f1-84e5-4d28-a11f-53ce31d63196
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# Negoziazione di sicurezza e timeout
Quando viene eseguita l'autenticazione di client e servizi, in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] è supportata una modalità in base alla quale la credenziale del servizio viene negoziata nell'ambito dell'autenticazione.In scenari di questo tipo, può verificarsi uno scambio di autenticazione multifase tra il client e il servizio al fine di propagare la credenziale del servizio al client.La proprietà <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.NegotiationTimeout%2A> controlla il tempo di completamento richiesto per tale scambio multifase.Questo timeout viene tuttavia applicato solo se lo scambio impiega effettivamente più tempo di una singola richiesta\-risposta.Nel caso in cui la negoziazione venga completata in un singolo round trip, il timeout non viene applicato.  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>   
 [Procedura: impostare lo sfasamento massimo dei segnali di clock](../../../../docs/framework/wcf/feature-details/how-to-set-a-max-clock-skew.md)