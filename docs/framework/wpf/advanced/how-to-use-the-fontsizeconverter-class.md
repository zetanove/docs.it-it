---
title: "Procedura: utilizzare la classe FontSizeConverter | Microsoft Docs"
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
  - "FontSizeConverter (oggetti)"
  - "tipografia, FontSizeConverter (oggetti)"
ms.assetid: 3b0592bd-7223-4860-a108-a5d72f3a9178
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: utilizzare la classe FontSizeConverter
## Esempio  
 In questo esempio viene illustrato come creare un'istanza di <xref:System.Windows.FontSizeConverter> e utilizzarla per modificare la dimensione del carattere.  
  
 Nell'esempio viene definito un metodo personalizzato denominato `changeSize` che converte il contenuto di un oggetto <xref:System.Windows.Controls.ListBoxItem>, definito in un file [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] separato, in un'istanza di <xref:System.Double> e in un secondo momento in un oggetto <xref:System.String>.  Questo metodo passa l'oggetto <xref:System.Windows.Controls.ListBoxItem> a un oggetto <xref:System.Windows.FontSizeConverter>, che converte la proprietà <xref:System.Windows.Controls.ContentControl.Content%2A> di un oggetto <xref:System.Windows.Controls.ListBoxItem> in un'istanza di <xref:System.Double>.  Questo valore viene quindi passato nuovamente come valore della proprietà <xref:System.Windows.Controls.TextBlock.FontSize%2A> dell'elemento <xref:System.Windows.Controls.TextBlock>.  
  
 In questo esempio viene inoltre definito un secondo metodo personalizzato denominato `changeFamily`.  Questo metodo converte la proprietà <xref:System.Windows.Controls.ContentControl.Content%2A> dell'oggetto <xref:System.Windows.Controls.ListBoxItem> in un oggetto <xref:System.String>, quindi passa tale valore alla proprietà <xref:System.Windows.Controls.TextBlock.FontFamily%2A> dell'elemento <xref:System.Windows.Controls.TextBlock>.  
  
 Questo esempio non viene eseguito.  
  
 [!code-csharp[FontSizeConverter#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSizeConverter/CSharp/Window1.xaml.cs#1)]  
  
## Vedere anche  
 <xref:System.Windows.FontSizeConverter>