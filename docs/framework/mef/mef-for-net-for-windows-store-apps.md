---
title: "Spazi dei nomi MEF per .NET per le applicazioni Windows Store | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7667770e-d163-4ad6-a303-085cf73db2f2
caps.latest.revision: 3
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 3
---
# Spazi dei nomi MEF per .NET per le applicazioni Windows Store
<xref:System.Composition?displayProperty=fullName> e i relativi spazi dei nomi figli contengono tipi per sviluppare applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] estendibili con Managed Extensibility Framework \(MEF\).  Questi spazi dei nomi appartengono al sottoinsieme di [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] per il sistema operativo [!INCLUDE[win8](../../../includes/win8-md.md)].  
  
 Questi spazi dei nomi non fanno parte della libreria di classi principale distribuita con .NET Framework.  Per installare questi spazi dei nomi, aprire il progetto in [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)], scegliere **Gestisci pacchetti NuGet** dal menu **Progetto**, ed eseguire la ricerca online del pacchetto Microsoft.Composition.  
  
-   <xref:System.Composition?displayProperty=fullName> fornisce le classi che costituiscono la base di MEF per le applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)].  
  
-   <xref:System.Composition.Convention?displayProperty=fullName> fornisce tipi che supportano l'uso di MEF con un modello di configurazione basato sulle convenzioni.  
  
-   <xref:System.Composition.Hosting?displayProperty=fullName> fornisce tipi MEF utili agli sviluppatori di applicazioni host.  
  
-   <xref:System.Composition.Hosting.Core?displayProperty=fullName> fornisce tipi MEF utilizzati internamente dal motore della composizione.  
  
 Per ulteriori informazioni su [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] e un elenco degli spazi dei nomi e i tipi in essi contenuti, vedere [.NET per una panoramica di applicazioni dello Store di Windows](http://go.microsoft.com/fwlink/p/?LinkID=238312) nel Centro per Sviluppatori di Windows.  
  
## Vedere anche  
 [Panoramica di .NET per le applicazioni Windows Store](http://go.microsoft.com/fwlink/p/?LinkID=238312)   
 [.NET per le applicazioni Windows Store – API supportate](http://go.microsoft.com/fwlink/p/?LinkID=247912)   
 [Managed Extensibility Framework \(MEF\)](../../../docs/framework/mef/index.md)