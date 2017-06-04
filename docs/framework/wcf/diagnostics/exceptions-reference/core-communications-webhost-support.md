---
title: "Comunicazioni principali: supporto Webhost | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 034c501f-96f9-4ef7-9602-3ac21788fd3e
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Comunicazioni principali: supporto Webhost
In questo argomento vengono elencate tutte le eccezioni generate dal supporto Webhost.  
  
## Elenco delle eccezioni  
  
|Codice sorgente|Stringa di risorsa|  
|---------------------|------------------------|  
|Hosting\_CompatibilityServiceNotHosted|Il servizio richiede la compatibilità ASP.NET.Deve inoltre essere ospitato in IIS.Ospitare il servizio in IIS con la compatibilità ASP.NET abilitata in Web.config o impostare la proprietà AspNetCompatibilityRequirementsAttribute.AspNetCompatibilityRequirementsMode su un valore diverso da Required.|  
|Hosting\_ListenerNotFoundForActivationInRecycling|Nessun canale è attualmente in ascolto all'indirizzo specificato.Se un'applicazione è in fase di riciclo, il servizio viene chiuso.|  
|Hosting\_NonHTTPInCompatibilityMode|Gli unici protocolli supportati nella compatibilità ASP.NET sono HTTP e HTTPS.Rimuovere l'endpoint specificato o disabilitare la compatibilità ASP.NET per l'applicazione.|  
|Hosting\_ProcessNotExecutingUnderHostedContext|Non è possibile richiamare il processo di hosting specificato all'interno dell'ambiente host corrente.L'API richiede che l'applicazione chiamante sia ospitata in Internet Information Services o nel servizio di attivazione dei processi di Windows.|  
|Hosting\_ServiceCompatibilityRequire|Non è possibile attivare il servizio perché richiede la compatibilità ASP.NET.La compatibilità ASP.NET non è abilitata per questa applicazione.Abilitare la compatibilità ASP.NET nel file Web.config o impostare AspNetCompatibilityRequirementsAttribute.AspNetCompatibility.|