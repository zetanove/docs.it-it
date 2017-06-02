---
title: "Componenti aggiuntivi di Firefox per supportare la distribuzione di applicazioni .NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "distribuzione di applicazioni .NET, distribuzione con componenti aggiuntivi di Firefox"
  - ".NET Framework Assistant per Firefox"
  - "componenti aggiuntivi di Firefox per la distribuzione di applicazioni .NET"
  - "plug-in WPF per Firefox"
ms.assetid: 2403403b-9b14-48e9-b70d-fa288a3c9081
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# Componenti aggiuntivi di Firefox per supportare la distribuzione di applicazioni .NET
Il plug\-in [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] per Firefox e .NET Framework Assistant per Firefox consentono il funzionamento di [!INCLUDE[TLA#tla_winfxwebapp#plural](../../../../includes/tlasharptla-winfxwebappsharpplural-md.md)], file [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] separati e applicazioni ClickOnce con il browser Mozilla Firefox.  
  
## Plug\-in WPF per Firefox  
 Il plug\-in Mozilla Firefox per Firefox consente l'esplorazione e l'esecuzione di applicazioni [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] e file [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] separati al livello superiore o in un IFRAME HTML nel browser Firefox.  Un'applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] è un'applicazione [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] che può essere pubblicata in un server Web e avviata in browser supportati.  Un file [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] separato è un file solo XAML che può essere esplorare e visualizzato in browser supportati, analogamente a un file XML.  
  
 Il plug\-in [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] per Firefox è installato con [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)].  Windows 7 include [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] ma non include il plug\-in [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] per Firefox. Non è possibile installare il plug\-in [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] per Firefox in Windows 7.  
  
 [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)] non include il plug\-in [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] per Firefox. Tuttavia, se è installato sia [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] che [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)], il plug\-in WPF per Firefox è installato con [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)].  Pertanto le applicazioni [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)] verranno comunque eseguite poiché l'host WPF caricherà la versione corretta del framework.  Per ulteriori informazioni, vedere [Host WPF \(PresentationHost.exe\)](../../../../docs/framework/wpf/app-development/wpf-host-presentationhost-exe.md).  
  
## .NET Framework Assistant per Firefox  
 .NET Framework Assistant per Firefox consente l'esecuzione di applicazioni ClickOnce autonome dal browser Firefox.  .NET Framework Assistant per Firefox funziona in modo identico quando è installato prima o dopo il browser Firefox.  Quando viene avviato il browser Firefox e installato [!INCLUDE[net_v35SP1_short](../../../../includes/net-v35sp1-short-md.md)], viene trovato e installato .NET Framework Assistant per Firefox.  Gli utenti possono configurare .NET Framework Assistant per Firefox per l'esecuzione delle seguenti operazioni:  
  
-   Richiedere prima di eseguire l'applicazione ClickOnce.  
  
-   Riferire tutte le versioni installate di .NET Framework o solo l'ultima versione.  
  
 .NET Framework Assistant per Firefox è incluso con [!INCLUDE[net_v35SP1_short](../../../../includes/net-v35sp1-short-md.md)].  Per informazioni sulla rimozione di .NET Framework Assistant per Firefox, vedere [Come rimuovere .NET Framework Assistant per Firefox](http://go.microsoft.com/fwlink/?LinkId=177944).  
  
## Vedere anche  
 [Distribuzione di un'applicazione WPF](../../../../docs/framework/wpf/app-development/deploying-a-wpf-application-wpf.md)   
 [Panoramica delle applicazioni browser XAML di WPF](../../../../docs/framework/wpf/app-development/wpf-xaml-browser-applications-overview.md)   
 [Verificare se il plug\-in delle applicazioni WPF per Firefox è installato](../../../../docs/framework/wpf/app-development/how-to-detect-whether-the-wpf-plug-in-for-firefox-is-installed.md)