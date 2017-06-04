---
title: "Procedura: creare e utilizzare un oggetto GridLengthConverter | Microsoft Docs"
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
  - "Grid (controllo), creazione, GridLengthConverter (oggetti)"
ms.assetid: 5ab75911-e36a-4825-80e4-081c57e8e182
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: creare e utilizzare un oggetto GridLengthConverter
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come creare e utilizzare un'istanza dell'oggetto <xref:System.Windows.GridLengthConverter>.  Nell'esempio viene definito un metodo personalizzato denominato `changeCol` che consente di passare <xref:System.Windows.Controls.ListBoxItem> a un oggetto <xref:System.Windows.GridLengthConverter> per convertire la proprietà <xref:System.Windows.Controls.ContentControl.Content%2A> di un oggetto <xref:System.Windows.Controls.ListBoxItem> in un'istanza di <xref:System.Windows.GridLength>.  Il valore convertito viene quindi passato come valore della proprietà <xref:System.Windows.Controls.ColumnDefinition.Width%2A> dell'elemento <xref:System.Windows.Controls.ColumnDefinition>.  
  
 Nell'esempio viene inoltre definito un secondo metodo personalizzato, denominato `changeColVal`.  Questo metodo personalizzato consente di convertire la proprietà <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A> di un oggetto <xref:System.Windows.Controls.Slider> in un oggetto <xref:System.String> e di passare tale valore all'oggetto <xref:System.Windows.Controls.ColumnDefinition> come proprietà <xref:System.Windows.Controls.ColumnDefinition.Width%2A> dell'elemento.  
  
 Si noti che un file [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] separato consente di definire il contenuto di un oggetto <xref:System.Windows.Controls.ListBoxItem>.  
  
 [!code-csharp[gridlengthConverterGrid#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridlengthConverterGrid/CSharp/Window1.xaml.cs#1)]
 [!code-vb[gridlengthConverterGrid#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/gridlengthConverterGrid/VisualBasic/Window1.xaml.vb#1)]  
  
## Vedere anche  
 <xref:System.Windows.GridLengthConverter>   
 <xref:System.Windows.GridLength>