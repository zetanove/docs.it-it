---
title: "Procedura: modificare il tipo di cursore | Microsoft Docs"
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
  - "cursore (puntatore del mouse)"
  - "puntatore del mouse (cursore), tipo di cursore"
ms.assetid: 08c945a7-8ab0-4320-acf3-0b4955a344c2
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: modificare il tipo di cursore
In questo esempio viene illustrato come modificare l'oggetto <xref:System.Windows.Input.Cursor> del puntatore del mouse per un elemento specifico e per l'applicazione.  
  
 Questo esempio è costituito da un file [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] e da un file code\-behind.  
  
## Esempio  
 Viene creata l'interfaccia utente, costituita da un oggetto <xref:System.Windows.Controls.ComboBox> per consentire la selezione dell'oggetto <xref:System.Windows.Input.Cursor> desiderato, da una coppia di oggetti <xref:System.Windows.Controls.RadioButton> per stabilire se la modifica del cursore viene applicata a un solo elemento o all'intera applicazione e da <xref:System.Windows.Controls.Border>, l'elemento al quale viene applicato il nuovo cursore.  
  
 [!code-xml[cursors#ChangeCursorsXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/cursors/CSharp/Window1.xaml#changecursorsxaml)]  
  
 Nel code\-behind riportato di seguito viene creato un gestore eventi <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> che viene chiamato quando il tipo di cursore viene modificato in <xref:System.Windows.Controls.ComboBox>.  Con un'istruzione switch viene applicato un filtro al nome del cursore e la proprietà <xref:System.Windows.FrameworkElement.Cursor%2A> viene impostata su <xref:System.Windows.Controls.Border>, denominato *DisplayArea*.  
  
 Se la modifica del cursore è impostata su "Entire Application", la proprietà <xref:System.Windows.Input.Mouse.OverrideCursor%2A> viene impostata sulla proprietà <xref:System.Windows.FrameworkElement.Cursor%2A> del controllo <xref:System.Windows.Controls.Border>.  In questo modo, al cursore viene imposta la modifica per l'intera applicazione.  
  
 [!code-csharp[cursors#ChangeCursorsSample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/cursors/CSharp/Window1.xaml.cs#changecursorssample)]
 [!code-vb[cursors#ChangeCursorsSample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/cursors/VisualBasic/Window1.xaml.vb#changecursorssample)]  
  
## Vedere anche  
 [Cenni preliminari sull’input](../../../../docs/framework/wpf/advanced/input-overview.md)