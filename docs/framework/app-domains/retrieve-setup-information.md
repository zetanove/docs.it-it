---
title: "Recupero di informazioni di installazione da un dominio applicazione | Microsoft Docs"
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
  - "AppDomainSetup (oggetto)"
  - "domini applicazione, recupero di informazioni di installazione"
  - "recupero di informazioni di installazione"
ms.assetid: 5cdb12ae-1e37-4a62-8ec7-93d6dcc6e8d9
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Recupero di informazioni di installazione da un dominio applicazione
Ogni istanza di un dominio applicazione è costituita da proprietà e da informazioni <xref:System.AppDomainSetup>.  È possibile recuperare le informazioni di installazione da un dominio applicazione tramite la classe <xref:System.AppDomain?displayProperty=fullName>.  In tale classe sono disponibili svariati membri che consentono di recuperare informazioni di configurazione relative a un dominio applicazione.  
  
 Per ottenere le informazioni di installazione passate al dominio nella fase di creazione, è inoltre possibile eseguire una query nell'oggetto **AppDomainSetup** e cercare il dominio applicazione.  
  
 L'esempio seguente consente di creare un nuovo dominio applicazione e di stampare nella console svariati valori relativi ai membri.  
  
 [!code-cpp[AppDomain_Setup#2](../../../samples/snippets/cpp/VS_Snippets_CLR/AppDomain_Setup/CPP/source2.cpp#2)]
 [!code-csharp[AppDomain_Setup#2](../../../samples/snippets/csharp/VS_Snippets_CLR/AppDomain_Setup/CS/source2.cs#2)]
 [!code-vb[AppDomain_Setup#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AppDomain_Setup/VB/source2.vb#2)]  
  
 L'esempio seguente consente di impostare e recuperare le informazioni di installazione per un dominio applicazione.  Si noti che le informazioni di configurazione vengono ricevute da `AppDomain.SetupInformation.ApplicationBase`.  
  
 [!code-cpp[AppDomain_Setup#3](../../../samples/snippets/cpp/VS_Snippets_CLR/AppDomain_Setup/CPP/source3.cpp#3)]
 [!code-csharp[AppDomain_Setup#3](../../../samples/snippets/csharp/VS_Snippets_CLR/AppDomain_Setup/CS/source3.cs#3)]
 [!code-vb[AppDomain_Setup#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AppDomain_Setup/VB/source3.vb#3)]  
  
## Vedere anche  
 [Hosting Overview](http://msdn.microsoft.com/it-it/ea527626-99e3-4995-81c4-c8f3e60eb6d5)   
 [Programming with Application Domains](http://msdn.microsoft.com/it-it/bd36055b-56bd-43eb-b4d8-820c37172131)   
 [Uso dei domini dell'applicazione](../../../docs/framework/app-domains/use.md)