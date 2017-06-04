---
title: "Sessioni affidabili | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Windows Communication Foundation, sessions and instances"
  - "WCF, sessions and instances"
  - "sessions and instances [WCF]"
helpviewer_keywords: 
  - "istanze [WCF]"
  - "sessioni [WCF]"
ms.assetid: 143951b3-3aa0-4540-b4b7-d33e77e874a1
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Sessioni affidabili
In questa sezione viene illustrato il significato di una sessione affidabile [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], per cosa è utilizzata, come e quando utilizzarla, quali sono le configurazioni di associazione che la supportano. Vengono inoltre definite le pratiche consigliate.Nella tabella seguente sono riepilogati i dettagli sui punti essenziali e gli argomenti correlati in questa sezione.  
  
 Una sessione affidabile fornita da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] assicura che i messaggi inviati tra gli endpoint vengano trasferiti attraverso SOAP o intermediari di trasporto e che vengano recapitati solo una volta e, facoltativamente, nello stesso ordine nel quale sono stati inviati.  
  
 Per utilizzare una sessione affidabile con un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], utilizzare una delle associazioni fornite dal sistema in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che supporta una sessione affidabile per impostazione predefinita o come opzione, oppure creare un'associazione personalizzata che supporti la sessione.  
  
## In questa sezione  
 [Panoramica delle sessioni affidabili](../../../../docs/framework/wcf/feature-details/reliable-sessions-overview.md)  
 Descrive le sessioni affidabili, quando utilizzarle, le diverse associazioni che supportano sessioni affidabili e come funzionano.  
  
 [Procedura: scambiare messaggi in una sessione affidabile](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-within-a-reliable-session.md)  
 Descrive come creare una sessione affidabile su HTTP utilizzando un'associazione personalizzata specificata nella configurazione.  
  
 [Procedura: proteggere i messaggi in sessioni affidabili](../../../../docs/framework/wcf/feature-details/how-to-secure-messages-within-reliable-sessions.md)  
 Descrive come proteggere una sessione affidabile.  
  
 [Procedura: creare un'associazione di sessione affidabile personalizzata con HTTPS](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-reliable-session-binding-with-https.md)  
 Descrive come creare una sessione affidabile su HTTPS.  
  
 [Procedure consigliate per le sessioni affidabili](../../../../docs/framework/wcf/feature-details/best-practices-for-reliable-sessions.md)  
 Descrive alcune delle procedure consigliate associate all'utilizzo di una sessione affidabile.  
  
## Riferimenti  
 <xref:System.ServiceModel.ReliableSession>  
  
## Vedere anche  
 [Code e sessioni affidabili](../../../../docs/framework/wcf/feature-details/queues-and-reliable-sessions.md)   
 [Sessioni, istanze e concorrenza](../../../../docs/framework/wcf/feature-details/sessions-instancing-and-concurrency.md)