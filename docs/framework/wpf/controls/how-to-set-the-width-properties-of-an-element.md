---
title: "Procedura: impostare le propriet&#224; di larghezza di un elemento | Microsoft Docs"
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
  - "Panel (controllo), proprietà di larghezza degli elementi"
  - "proprietà di larghezza"
ms.assetid: 6ee04a9d-63f0-4f5b-a406-0a8cd4c35729
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: impostare le propriet&#224; di larghezza di un elemento
## Esempio  
 In questo esempio vengono illustrate le differenze nel comportamento di rendering tra le quattro proprietà correlate alla larghezza disponibili in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  
  
 La classe <xref:System.Windows.FrameworkElement> espone quattro proprietà che descrivono le caratteristiche di larghezza di un elemento.  Queste quattro proprietà possono entrare in conflitto e, in tal caso, il valore che ha la precedenza è determinato come segue: il valore <xref:System.Windows.FrameworkElement.MinWidth%2A> ha la precedenza sul valore <xref:System.Windows.FrameworkElement.MaxWidth%2A>, che a sua volta ha la precedenza sul valore <xref:System.Windows.FrameworkElement.Width%2A>.  Una quarta proprietà, <xref:System.Windows.FrameworkElement.ActualWidth%2A>, è di sola lettura e specifica la larghezza effettiva determinata dalle interazioni con il processo di layout.  
  
 Negli esempi [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] seguenti viene tracciato un elemento <xref:System.Windows.Shapes.Rectangle> \(`rect1`\) come elemento figlio di <xref:System.Windows.Controls.Canvas>.  È possibile modificare le proprietà di larghezza di un oggetto <xref:System.Windows.Shapes.Rectangle> utilizzando una serie di elementi <xref:System.Windows.Controls.ListBox> che rappresentano i valori delle proprietà <xref:System.Windows.FrameworkElement.MinWidth%2A>, <xref:System.Windows.FrameworkElement.MaxWidth%2A> e <xref:System.Windows.FrameworkElement.Width%2A>.  In questo modo, la precedenza di ogni proprietà viene visualizzata graficamente.  
  
 [!code-xml[WidthMinWidthMaxWidth#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WidthMinWidthMaxWidth/CSharp/Window1.xaml#1)]  
[!code-xml[WidthMinWidthMaxWidth#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WidthMinWidthMaxWidth/CSharp/Window1.xaml#2)]  
  
 Negli esempi code\-behind seguenti sono gestiti gli eventi generati dall'evento <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged>.  Ogni metodo personalizzato accetta l'input dall'oggetto <xref:System.Windows.Controls.ListBox>, analizza il valore come <xref:System.Double> e lo applica alla proprietà correlata alla larghezza specificata.  I valori di larghezza vengono inoltre convertiti in una stringa e scritti nei vari elementi <xref:System.Windows.Controls.TextBlock>. La definizione di tali elementi non viene illustrata nel codice XAML selezionato.  
  
 [!code-csharp[WidthMinWidthMaxWidth#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WidthMinWidthMaxWidth/CSharp/Window1.xaml.cs#3)]
 [!code-vb[WidthMinWidthMaxWidth#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WidthMinWidthMaxWidth/VisualBasic/Window1.xaml.vb#3)]  
  
 Per l'esempio completo, vedere [Esempio di confronto di proprietà Width](http://go.microsoft.com/fwlink/?LinkID=160050) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Controls.ListBox>   
 <xref:System.Windows.FrameworkElement>   
 <xref:System.Windows.FrameworkElement.ActualWidth%2A>   
 <xref:System.Windows.FrameworkElement.MaxWidth%2A>   
 <xref:System.Windows.FrameworkElement.MinWidth%2A>   
 <xref:System.Windows.FrameworkElement.Width%2A>   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [Impostare le proprietà di altezza di un elemento](../../../../docs/framework/wpf/controls/how-to-set-the-height-properties-of-an-element.md)   
 [Esempio di confronto di proprietà Width](http://go.microsoft.com/fwlink/?LinkID=160050)