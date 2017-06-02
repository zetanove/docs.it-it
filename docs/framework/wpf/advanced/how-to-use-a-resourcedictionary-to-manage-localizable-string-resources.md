---
title: "Procedura: utilizzare un oggetto ResourceDictionary per gestire le risorse di tipo stringa localizzabili | Microsoft Docs"
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
  - "localizzazione [WPF], creazione di package di risorse di tipo stringa"
  - "creazione di package di risorse di tipo stringa"
  - "ResourceDictionary [WPF]"
  - "risorse [WPF], creazione di package di risorse di tipo stringa"
ms.assetid: 19e7d9a5-20df-4ad3-b157-fe6515902e5e
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: utilizzare un oggetto ResourceDictionary per gestire le risorse di tipo stringa localizzabili
In questo esempio viene illustrato come utilizzare <xref:System.Windows.ResourceDictionary> per assemblare risorse di tipo stringa localizzabili per applicazioni [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)].  
  
### Per utilizzare un oggetto ResourceDictionary per gestire le risorse di tipo stringa localizzabili  
  
1.  Creare un oggetto <xref:System.Windows.ResourceDictionary> che contiene le stringhe da localizzare.  Il codice che segue fornisce un esempio in proposito.  
  
     [!code-xml[StringLocalizationSample#StringResourceDictionary](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StringLocalizationSample/CSharp/StringResources.xaml#stringresourcedictionary)]  
  
     Con questo codice viene definita una risorsa di stringa, `localizedMessage`, di tipo <xref:System.String>, dallo spazio dei nomi <xref:System> in mscorlib.dll.  
  
2.  Aggiungere <xref:System.Windows.ResourceDictionary> all'applicazione, utilizzando il codice riportato di seguito.  
  
     [!code-xml[StringLocalizationSample#ReferencingStringResourceDictionary](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StringLocalizationSample/CSharp/App.xaml#referencingstringresourcedictionary)]  
  
3.  Utilizzare la risorsa di tipo stringa dal markup, utilizzando [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] analogo al seguente.  
  
     [!code-xml[StringLocalizationSample#GetLocalizedResourceFromMarkup](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StringLocalizationSample/CSharp/MainWindow.xaml#getlocalizedresourcefrommarkup)]  
  
4.  Utilizzare la risorsa di tipo stringa dal code\-behind, utilizzando codice analogo al seguente.  
  
     [!code-csharp[StringLocalizationSample#GetLocalizedResourceFromCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StringLocalizationSample/CSharp/MainWindow.xaml.cs#getlocalizedresourcefromcode)]
     [!code-vb[StringLocalizationSample#GetLocalizedResourceFromCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StringLocalizationSample/VisualBasic/MainWindow.xaml.vb#getlocalizedresourcefromcode)]  
  
5.  Localizzare l'applicazione.  Per ulteriori informazioni, vedere [Localizzare un'applicazione](../../../../docs/framework/wpf/advanced/how-to-localize-an-application.md).