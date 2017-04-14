---
title: "Procedura: trovare elementi generati da un oggetto ControlTemplate | Microsoft Docs"
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
  - "ControlTemplates [WPF], ricerca di elementi"
  - "ricerca di elementi ControlTemplate"
ms.assetid: d7b25447-ceff-4bb4-9be5-fd7c40ef00af
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: trovare elementi generati da un oggetto ControlTemplate
In questo esempio viene illustrato come trovare elementi generati da <xref:System.Windows.Controls.ControlTemplate>.  
  
## Esempio  
 Nell'esempio seguente viene illustrato uno stile che consente di creare un oggetto <xref:System.Windows.Controls.ControlTemplate> semplice per la classe <xref:System.Windows.Controls.Button>:  
  
 [!code-xml[FindGeneratedItems#CT](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml#ct)]  
  
 Per trovare un elemento all'interno del modello, una volta applicato il modello stesso, è possibile chiamare il metodo <xref:System.Windows.FrameworkTemplate.FindName%2A> di <xref:System.Windows.Controls.Control.Template%2A>.  Nell'esempio seguente viene creata una finestra di messaggio in cui viene indicato il valore della larghezza effettiva dell'oggetto <xref:System.Windows.Controls.Grid> all'interno del modello di controllo:  
  
 [!code-csharp[FindGeneratedItems#CTFindElement](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml.cs#ctfindelement)]
 [!code-vb[FindGeneratedItems#CTFindElement](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindGeneratedItems/VisualBasic/Window1.xaml.vb#ctfindelement)]  
  
## Vedere anche  
 [Trovare elementi generati da un oggetto DataTemplate](../../../../docs/framework/wpf/data/how-to-find-datatemplate-generated-elements.md)   
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [NameScope XAML WPF](../../../../docs/framework/wpf/advanced/wpf-xaml-namescopes.md)   
 [Strutture ad albero in WPF](../../../../docs/framework/wpf/advanced/trees-in-wpf.md)