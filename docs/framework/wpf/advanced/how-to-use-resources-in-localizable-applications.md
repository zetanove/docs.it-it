---
title: "Procedura: utilizzare le risorse in applicazioni localizzabili | Microsoft Docs"
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
  - "applicazioni, localizzabili"
  - "localizzabili (applicazioni)"
ms.assetid: 08539ad6-7fca-4f34-b82b-ff439e11dfa7
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: utilizzare le risorse in applicazioni localizzabili
Per localizzazione si intende l'adattamento di un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] a impostazioni cultura diverse.  A questo scopo, testo quali titoli, didascalie, elementi di caselle di riepilogo e così via devono essere tradotti.  Per semplificare la traduzione, gli elementi localizzabili vengono raccolti in file di risorse.  Per informazioni su come creare un file di risorse da destinare alla localizzazione, vedere [Localizzare un'applicazione](../../../../docs/framework/wpf/advanced/how-to-localize-an-application.md).  Per rendere localizzabile un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], è necessario che gli sviluppatori compilino tutte le risorse localizzabili in un assembly di risorse.  L'assembly di risorse viene localizzato in lingue diverse e il code\-behind utilizza l'[!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] di gestione risorse per il caricamento.  Uno dei file necessari per un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è un file di progetto \(proj\).  Tutte le risorse utilizzate nell'applicazione devono essere incluse nel file di progetto.  Di seguito è riportato un esempio di codice.  
  
## Esempio  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]  
  
 `<Resource Include="data\picture1.jpg"/>`  
  
 `<EmbeddedResource Include="data\stringtable.en-US.restext"/>`  
  
 Per utilizzare una risorsa nell'applicazione, creare un'istanza dell'oggetto <xref:System.Resources.ResourceManager> e caricare la risorsa che si desidera utilizzare.  Di seguito viene illustrato come procedere.  
  
 [!code-csharp[LocalizationResources#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationResources/CSharp/page1.xaml.cs#2)]