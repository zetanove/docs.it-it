---
title: "Procedura: configurare un dominio applicazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "domini applicazione, configurazione"
  - "ApplicationBase (proprietà)"
ms.assetid: 07ea8438-7a34-49f0-a7e8-3d6ff7e4a482
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: configurare un dominio applicazione
La classe <xref:System.AppDomainSetup> consente di fornire a Common Language Runtime informazioni di configurazione per un nuovo dominio dell'applicazione.  Quando si creano domini dell'applicazione, la proprietà fondamentale è <xref:System.AppDomainSetup.ApplicationBase%2A>.  Le altre proprietà **AppDomainSetup** vengono utilizzate principalmente dagli host Common Language Runtime per configurare un particolare dominio applicazione.  
  
 La proprietà **ApplicationBase** consente di definire la directory radice dell'applicazione.  Quando riceve una richiesta di tipo, Common Language Runtime prova a individuare l'assembly contenente il tipo nella directory specificata nella proprietà **ApplicationBase**.  
  
> [!NOTE]
>  Un nuovo dominio applicazione eredita solo la proprietà **ApplicationBase** del creatore.  
  
 L'esempio seguente consente di creare un'istanza della classe **AppDomainSetup**, di utilizzare tale classe per creare un nuovo dominio applicazione, di scrivere le informazioni nella console, quindi di scaricare il dominio applicazione.  
  
## Esempio  
 [!code-cpp[ADApplicationBase#2](../../../samples/snippets/cpp/VS_Snippets_CLR/ADApplicationBase/CPP/source2.cpp#2)]
 [!code-csharp[ADApplicationBase#2](../../../samples/snippets/csharp/VS_Snippets_CLR/ADApplicationBase/CS/source2.cs#2)]
 [!code-vb[ADApplicationBase#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/ADApplicationBase/VB/source2.vb#2)]  
  
## Vedere anche  
 [Hosting Overview](http://msdn.microsoft.com/it-it/ea527626-99e3-4995-81c4-c8f3e60eb6d5)   
 [Programming with Application Domains](http://msdn.microsoft.com/it-it/bd36055b-56bd-43eb-b4d8-820c37172131)   
 [Uso dei domini dell'applicazione](../../../docs/framework/app-domains/use.md)