---
title: "Procedura: Scaricare un dominio dell&#39;applicazione | Microsoft Docs"
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
  - "metodo Unload"
  - "domini dell'applicazione, scaricamento"
  - "scaricamento di domini dell'applicazione"
ms.assetid: f356116d-e415-4f7c-a332-6e6a60227192
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: Scaricare un dominio dell&#39;applicazione
Una volta terminato l'utilizzo di un dominio applicazione, scaricare tale dominio utilizzando il metodo [System.AppDomain.Unload](frlrfSystemAppDomainClassUnloadTopic).  Il metodo **Unload** consente di chiudere normalmente il dominio applicazione specificato.  Durante il processo di scaricamento, l'accesso al dominio applicazione non è consentito ad alcun nuovo thread e tutti i dati specifici del dominio applicazione vengono liberati.  
  
 Gli assembly caricati nel dominio applicazione vengono rimossi e non risultano più disponibili.  Se un assembly nel dominio applicazione è indipendente dal dominio, i dati relativi all'assembly rimarranno in memoria fino alla chiusura dell'intero processo.  L'unico meccanismo che consente lo scaricamento di un assembly indipendente dal dominio consiste nella chiusura dell'intero processo.  In alcune situazioni non risulta possibile scaricare un dominio dell'applicazione e viene generata un'eccezione <xref:System.CannotUnloadAppDomainException>.  
  
 L'esempio seguente consente di creare un dominio applicazione denominato `MyDomain`, di stampare alcune informazioni nella console e di scaricare il dominio applicazione.  Si noti che nel codice si tenta in seguito di stampare il nome descrittivo del dominio applicazione scaricato nella console.  Questa operazione genera un'eccezione, gestita da istruzioni try\/catch alla fine del programma.  
  
## Esempio  
 [!code-cpp[System.AppDomain.Load#3](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.appdomain.load/cpp/source3.cpp#3)]
 [!code-csharp[System.AppDomain.Load#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.load/cs/source3.cs#3)]
 [!code-vb[System.AppDomain.Load#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.load/vb/source3.vb#3)]  
  
## Vedere anche  
 [Programming with Application Domains](http://msdn.microsoft.com/it-it/bd36055b-56bd-43eb-b4d8-820c37172131)   
 [Procedura: Creare un dominio dell'applicazione](../../../docs/framework/app-domains/how-to-create-an-application-domain.md)   
 [Uso dei domini dell'applicazione](../../../docs/framework/app-domains/use.md)