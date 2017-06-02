---
title: "Troubleshooting: Service Application Won&#39;t Install | Microsoft Docs"
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
  - "troubleshooting service applications"
  - "services, troubleshooting"
  - "services, debugging"
  - "Windows NT services, troubleshooting"
  - "troubleshooting NT services"
  - "Windows Service applications, troubleshooting"
ms.assetid: 45c48e2e-b97d-44bc-8896-14f328e0ce33
caps.latest.revision: 8
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 8
---
# Troubleshooting: Service Application Won&#39;t Install
Se l'applicazione di servizio non viene installata correttamente, assicurarsi che la proprietà <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> della classe di servizio sia impostata sullo stesso valore riportato nel programma di installazione del servizio specifico.  Per la corretta installazione del servizio, il valore deve essere identico in entrambe le istanze.  
  
> [!NOTE]
>  Per ottenere informazioni sul processo di installazione, è possibile consultare i log dell'installazione.  
  
 Verificare inoltre se è già stato installato un altro servizio con lo stesso nome.  Per una corretta installazione, i nomi dei servizi devono essere univoci.  
  
## Vedere anche  
 [Introduction to Windows Service Applications](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)