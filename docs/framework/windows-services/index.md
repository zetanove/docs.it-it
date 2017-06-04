---
title: "Developing Windows Service Applications | Microsoft Docs"
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
  - "ServiceInstaller class, Windows Service applications"
  - "Service class, Windows Service applications"
  - "Windows Service applications"
  - "Windows NT services"
  - "ServiceProcessInstaller class, Windows Service applications"
  - "services"
  - ".NET applications, Windows applications"
ms.assetid: ba72d648-9553-4849-b829-069ad5ea014b
caps.latest.revision: 18
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 18
---
# Developing Windows Service Applications
Mediante Microsoft [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] o Microsoft [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK è possibile creare servizi in modo semplice tramite la creazione di un'applicazione che viene installata come servizio.  Questo tipo di applicazione è chiamata servizio Windows.  Con le funzionalità del framework, è possibile creare servizi, installarli, avviarli, interromperli e controllarne in altro modo il funzionamento.  
  
> [!WARNING]
>  Il modello servizio Windows per C\+\+ non è stato incluso in Visual Studio 2010.  Per creare un servizio Windows, è possibile creare un servizio nel codice gestito in visual C\# o Visual Basic, in grado di interagire con il codice C\+\+ esistente se necessario, oppure creare un servizio Windows in C\+\+ nativo utilizzando [Creazione guidata progetto ATL](../Topic/ATL%20Project%20Wizard.md).  
  
## In questa sezione  
 [Introduction to Windows Service Applications](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)  
 Viene fornita una panoramica delle applicazioni di servizio Windows, la durata di un servizio e differenza tra le applicazioni di servizio e altri tipi comuni di progetto.  
  
 [Walkthrough: Creating a Windows Service Application in the Component Designer](../../../docs/framework/windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer.md)  
 Viene fornito un esempio di creazione di un servizio in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] e Visual C\#.  
  
 [Service Application Programming Architecture](../../../docs/framework/windows-services/service-application-programming-architecture.md)  
 Vengono illustrati gli elementi del linguaggio utilizzati nella programmazione dei servizi.  
  
 [How to: Create Windows Services](../../../docs/framework/windows-services/how-to-create-windows-services.md)  
 Viene descritto il processo di creazione e configurazione dei servizi Windows utilizzando il modello di progetto di servizio Windows.  
  
## Sezioni correlate  
 <xref:System.ServiceProcess.ServiceBase>  
 Vengono descritte le funzionalità principali della classe <xref:System.ServiceProcess.ServiceBase>, utilizzata per creare servizi.  
  
 <xref:System.ServiceProcess.ServiceProcessInstaller>  
 Vengono descritte le funzionalità della classe <xref:System.ServiceProcess.ServiceProcessInstaller>, utilizzata con la classe <xref:System.ServiceProcess.ServiceInstaller> per installare e disinstallare servizi.  
  
 <xref:System.ServiceProcess.ServiceInstaller>  
 Vengono descritte le funzionalità della classe <xref:System.ServiceProcess.ServiceInstaller>, utilizzata con la classe <xref:System.ServiceProcess.ServiceProcessInstaller> per installare e disinstallare servizi.  
  
 [Creazione di progetti da modelli](http://msdn.microsoft.com/it-it/7c36d86a-6b79-4480-8228-0f925f1204b2)  
 Vengono descritti i tipi di progetto utilizzati in questo capitolo e viene illustrato come scegliere tra questi.