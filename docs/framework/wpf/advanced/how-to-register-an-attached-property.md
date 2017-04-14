---
title: "Procedura: registrare una propriet&#224; associata | Microsoft Docs"
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
  - "proprietà associate, registrazione"
  - "registrazione di proprietà associate"
ms.assetid: eb47bd94-0451-4f8d-8fb6-95f7812ac05b
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: registrare una propriet&#224; associata
In questo esempio viene mostrato come registrare una [proprietà associata](GTMT) e fornire funzioni di accesso pubbliche, in modo da poter utilizzare la proprietà sia in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], sia nel codice.  Le proprietà associate rappresentano un concetto della sintassi definito da [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  La maggior parte delle proprietà associate per i tipi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene anche implementata come [proprietà di dipendenza](GTMT).  È possibile utilizzare le [proprietà di dipendenza](GTMT) in qualsiasi tipo <xref:System.Windows.DependencyObject>.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come registrare una proprietà associata come proprietà di dipendenza utilizzando il metodo <xref:System.Windows.DependencyProperty.RegisterAttached%2A>.  La classe di provider può fornire metadati predefiniti per la proprietà applicabile quando la proprietà viene utilizzata in un'altra classe, a meno che tale classe esegua l'override dei metadati.  In questo esempio, il valore predefinito della proprietà `IsBubbleSource` viene impostato su `false`.  
  
 La classe provider per una proprietà associata \(anche se non è registrata come proprietà di dipendenza\) deve fornire funzioni di accesso get e set statiche basate sulla convenzione di denominazione `Set`*\[NomeProprietàAssociata\]* e `Get`*\[NomeProprietàAssociata\]*. Queste funzioni di accesso sono necessarie per consentire al reader [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] in funzione di riconoscere la proprietà come attributo in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] e risolvere i tipi appropriati.  
  
 [!code-csharp[WPFAquariumSln#RegisterAttachedBubbler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#registerattachedbubbler)]
 [!code-vb[WPFAquariumSln#RegisterAttachedBubbler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#registerattachedbubbler)]  
  
## Vedere anche  
 <xref:System.Windows.DependencyProperty>   
 [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [Procedure relative](../../../../docs/framework/wpf/advanced/properties-how-to-topics.md)