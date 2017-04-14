---
title: "Troubleshooting: Debugging Windows Services | Microsoft Docs"
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
  - "debugging Windows Service applications"
  - "debugging [Visual Studio], Windows services"
  - "troubleshooting service applications"
  - "services, troubleshooting"
  - "troubleshooting debugging, Windows Services"
  - "Windows Service applications, debugging"
  - "services, debugging"
  - "Windows Service applications, troubleshooting"
ms.assetid: cf859d4c-f04c-4cb7-81e3-bc7de8bea190
caps.latest.revision: 8
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 8
---
# Troubleshooting: Debugging Windows Services
Quando si esegue il debug di un'applicazione di servizio Windows, il servizio interagisce con il gestore del servizio Windows.  Per avviare il servizio, il gestore del servizio Windows effettua una chiamata al metodo <xref:System.ServiceProcess.ServiceBase.OnStart%2A>, quindi attende 30 secondi la risposta del metodo <xref:System.ServiceProcess.ServiceBase.OnStart%2A>.  Se il metodo non risponde in questo intervallo di tempo, il gestore segnala che è impossibile avviare il servizio.  
  
 Quando si esegue il debug del metodo <xref:System.ServiceProcess.ServiceBase.OnStart%2A>, come descritto nell'argomento [How to: Debug Windows Service Applications](../../../docs/framework/windows-services/how-to-debug-windows-service-applications.md), è necessario considerare questo intervallo di trenta secondi.  Se un eventuale punto di interruzione inserito nel metodo <xref:System.ServiceProcess.ServiceBase.OnStart%2A> non viene superato entro 30 secondi, il servizio non verrà avviato.  
  
## Vedere anche  
 [How to: Debug Windows Service Applications](../../../docs/framework/windows-services/how-to-debug-windows-service-applications.md)   
 [Introduction to Windows Service Applications](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)