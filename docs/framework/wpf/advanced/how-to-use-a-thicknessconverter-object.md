---
title: "Procedura: utilizzare un oggetto ThicknessConverter | Microsoft Docs"
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
  - "spessore del bordo"
  - "ThicknessConverter (oggetti)"
ms.assetid: 52682194-d7fd-499c-8005-73fcc84e7b2c
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: utilizzare un oggetto ThicknessConverter
## Esempio  
 In questo esempio viene illustrato come creare un'istanza di <xref:System.Windows.ThicknessConverter> e utilizzarla per modificare lo spessore di un bordo.  
  
 Nell'esempio viene definito un metodo personalizzato denominato `changeThickness`, che prima converte il contenuto di un oggetto <xref:System.Windows.Controls.ListBoxItem>, definito in un file [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] separato, in un'istanza di <xref:System.Windows.Thickness> e successivamente converte il contenuto in un oggetto <xref:System.String>.  Questo metodo passa l'oggetto <xref:System.Windows.Controls.ListBoxItem> a un oggetto <xref:System.Windows.ThicknessConverter>, che converte la proprietà <xref:System.Windows.Controls.ContentControl.Content%2A> di un oggetto <xref:System.Windows.Controls.ListBoxItem> in un'istanza di <xref:System.Windows.Thickness>.  Questo valore viene quindi passato nuovamente come valore della proprietà <xref:System.Windows.Controls.Border.BorderThickness%2A> dell'oggetto <xref:System.Windows.Controls.Border>.  
  
 Questo esempio non viene eseguito.  
  
 [!code-csharp[ThicknessConverter#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ThicknessConverter/CSharp/Window1.xaml.cs#1)]
 [!code-vb[ThicknessConverter#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ThicknessConverter/VisualBasic/Window1.xaml.vb#1)]  
  
## Vedere anche  
 <xref:System.Windows.Thickness>   
 <xref:System.Windows.ThicknessConverter>   
 <xref:System.Windows.Controls.Border>   
 [How to: Change the Margin Property](http://msdn.microsoft.com/it-it/8a313efd-5f99-4097-b4c1-8fa49d8379a2)   
 [How to: Convert a ListBoxItem to a new Data Type](http://msdn.microsoft.com/it-it/7a080b88-184e-4b27-bb61-d42bafba9727)   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)