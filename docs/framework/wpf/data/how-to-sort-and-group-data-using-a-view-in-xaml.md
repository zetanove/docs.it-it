---
title: "Procedura: ordinare e raggruppare i dati tramite una visualizzazione di XAML | Microsoft Docs"
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
  - "associazione dati, raggruppamento di dati in visualizzazioni in XAML"
  - "associazione dati, ordinamento di dati in visualizzazioni in XAML"
  - "raggruppamento di dati in visualizzazioni in XAML"
  - "ordinamento di dati in visualizzazioni in XAML"
  - "visualizzazioni, raggruppamento di dati"
  - "visualizzazioni, ordinamento dei dati"
  - "XAML, raggruppamento di dati in visualizzazioni"
  - "XAML, ordinamento di dati in visualizzazioni"
ms.assetid: 145c8c3f-dbdd-4d0d-816f-90b35eba7eda
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: ordinare e raggruppare i dati tramite una visualizzazione di XAML
In questo esempio viene illustrato come creare una visualizzazione di una raccolta dati in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  Le visualizzazioni tengono conto delle funzionalità di raggruppamento, ordinamento, filtro e del concetto di elemento corrente.  
  
## Esempio  
 Nell'esempio riportato di seguito, la risorsa statica denominata *places* viene definita come una raccolta di oggetti *Place* nella quale ogni oggetto *Place* è dato da un nome di città e di stato.  Il prefisso *src* viene mappato allo spazio dei nomi in cui è definita l'origine dati *Places*.  Il prefisso *scm* è mappato a `"clr-namespace:System.ComponentModel;assembly=WindowsBase"` e *dat* è mappato a `"clr-namespace:System.Windows.Data;assembly=PresentationFramework"`.  
  
 Nell'esempio riportato di seguito viene creata una visualizzazione della raccolta dati ordinata in base al nome della città e raggruppata in base allo stato.  
  
 [!code-xml[CollectionViewSource#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#1)]  
  
 La visualizzazione può essere un'origine di associazione, come nell'esempio riportato di seguito:  
  
 [!code-xml[CollectionViewSource#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#2)]  
  
 Per le associazioni ai dati XML definite in una risorsa <xref:System.Windows.Data.XmlDataProvider>, anteporre il simbolo @ al nome XML.  
  
 [!code-xml[CollectionViewSource#XDPChunk](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#xdpchunk)]  
  
 [!code-xml[CollectionViewSource#Attribute](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#attribute)]  
  
## Vedere anche  
 <xref:System.Windows.Data.CollectionViewSource>   
 [Ottenere la visualizzazione predefinita di una raccolta dati](../../../../docs/framework/wpf/data/how-to-get-the-default-view-of-a-data-collection.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)