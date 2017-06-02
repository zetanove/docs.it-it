---
title: "Procedura: impostare le propriet&#224; di altezza di un elemento | Microsoft Docs"
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
  - "altezza (proprietà)"
  - "Panel (controllo), proprietà di altezza degli elementi"
ms.assetid: 5ab9e781-dbb8-469a-a3c8-cf38ce312647
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: impostare le propriet&#224; di altezza di un elemento
## Esempio  
 In questo esempio vengono illustrate le differenze nel comportamento di rendering tra le quattro proprietà correlate all'altezza disponibili in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  
  
 La classe <xref:System.Windows.FrameworkElement> espone quattro proprietà che descrivono le caratteristiche di altezza di un elemento.  Queste quattro proprietà possono entrare in conflitto e, in tal caso, il valore che ha la precedenza è determinato come segue: il valore <xref:System.Windows.FrameworkElement.MinHeight%2A> ha la precedenza sul valore <xref:System.Windows.FrameworkElement.MaxHeight%2A>, che a sua volta ha la precedenza sul valore <xref:System.Windows.FrameworkElement.Height%2A>.  Una quarta proprietà, <xref:System.Windows.FrameworkElement.ActualHeight%2A>, è di sola lettura e specifica l'altezza effettiva determinata dalle interazioni con il processo di layout.  
  
 Negli esempi [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] seguenti viene tracciato un elemento <xref:System.Windows.Shapes.Rectangle> \(`rect1`\) come elemento figlio di <xref:System.Windows.Controls.Canvas>.  È possibile modificare le proprietà di altezza di un oggetto <xref:System.Windows.Shapes.Rectangle> utilizzando una serie di elementi <xref:System.Windows.Controls.ListBox> che rappresentano i valori delle proprietà <xref:System.Windows.FrameworkElement.MinHeight%2A>, <xref:System.Windows.FrameworkElement.MaxHeight%2A> e <xref:System.Windows.FrameworkElement.Height%2A>.  In questo modo, la precedenza di ogni proprietà viene visualizzata graficamente.  
  
 [!code-xml[HeightMinHeightMaxHeight#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HeightMinHeightMaxHeight/CSharp/Window1.xaml#1)]  
[!code-xml[HeightMinHeightMaxHeight#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HeightMinHeightMaxHeight/CSharp/Window1.xaml#2)]  
  
 Negli esempi code\-behind seguenti sono gestiti gli eventi generati dall'evento <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged>.  Ogni gestore accetta l'input dall'oggetto <xref:System.Windows.Controls.ListBox>, analizza il valore come oggetto <xref:System.Double> e applica tale valore alla proprietà correlata all'altezza specificata.  I valori di altezza vengono inoltre convertiti in una stringa e scritti nei vari elementi <xref:System.Windows.Controls.TextBlock>. La definizione di tali elementi non viene illustrata nel codice XAML selezionato.  
  
 [!code-csharp[HeightMinHeightMaxHeight#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HeightMinHeightMaxHeight/CSharp/Window1.xaml.cs#3)]
 [!code-vb[HeightMinHeightMaxHeight#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HeightMinHeightMaxHeight/VisualBasic/Window1.xaml.vb#3)]  
  
 Per l'esempio completo, vedere [Esempio di proprietà di altezza](http://go.microsoft.com/fwlink/?LinkID=159993) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.FrameworkElement>   
 <xref:System.Windows.Controls.ListBox>   
 <xref:System.Windows.FrameworkElement.ActualHeight%2A>   
 <xref:System.Windows.FrameworkElement.MaxHeight%2A>   
 <xref:System.Windows.FrameworkElement.MinHeight%2A>   
 <xref:System.Windows.FrameworkElement.Height%2A>   
 [Impostare le proprietà di larghezza di un elemento](../../../../docs/framework/wpf/controls/how-to-set-the-width-properties-of-an-element.md)   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [Esempio di proprietà di altezza](http://go.microsoft.com/fwlink/?LinkID=159993)