---
title: "Sicurezza dei comportamenti | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 19710ae3-f197-4d28-ba9d-52e465006819
caps.latest.revision: 5
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 5
---
# Sicurezza dei comportamenti
Contenuto della sezione sono contenuti esempi che illustrano la sicurezza della configurazione per i comportamenti del servizio.  
  
## In questa sezione  
 [Comportamento di controllo dei servizi](../../../../docs/framework/wcf/samples/service-auditing-behavior.md)  
 Questo esempio illustra come usare <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> per abilitare il controllo degli eventi di sicurezza durante le operazioni del servizio.  
  
 [Provider di appartenenza e di ruoli](../../../../docs/framework/wcf/samples/membership-and-role-provider.md)  
 In questo esempio viene illustrato in che modo un servizio può usare i provider di appartenenza e di ruoli [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] per autenticare e autorizzare i client.  
  
 [Autorizzazione dell'accesso alle operazioni del servizio](../../../../docs/framework/wcf/samples/authorizing-access-to-service-operations.md)  
 In questo esempio viene illustrato come usare l'[\<autorizzazioneServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md) e abilitare l'uso dell'attributo <xref:System.Security.Permissions.PrincipalPermissionAttribute> per autorizzare l'accesso alle operazioni del servizio.  
  
 [Rappresentazione di client](../../../../docs/framework/wcf/samples/impersonating-the-client.md)  
 In questo esempio viene illustrato come rappresentare l'applicazione del chiamante nel servizio in modo che quest'ultimo possa accedere alle risorse di sistema per conto del chiamante.