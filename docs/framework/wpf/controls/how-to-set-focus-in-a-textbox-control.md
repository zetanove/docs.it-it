---
title: "Procedura: impostare lo stato attivo in un controllo TextBox | Microsoft Docs"
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
  - "stato attivo, impostazione"
  - "TextBox (controllo), impostazione dello stato attivo"
ms.assetid: 24b61b45-dc2d-425e-9839-b017af7ab86f
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: impostare lo stato attivo in un controllo TextBox
In questo esempio viene illustrato come utilizzare il metoco <xref:System.Windows.UIElement.Focus%2A> per impostare lo stato attivo su un controllo <xref:System.Windows.Controls.TextBox>.  
  
## Esempio  
 Nell'esempio di [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] riportato di seguito viene illustrato un semplice controllo <xref:System.Windows.Controls.TextBox> denominato *tbFocusMe*.  
  
 [!code-xml[TextBox_MiscCode#_TextBoxFocusXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_textboxfocusxaml)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene chiamato il metodo <xref:System.Windows.UIElement.Focus%2A> per impostare lo stato attivo sul controllo <xref:System.Windows.Controls.TextBox> denominato *tbFocusMe*.  
  
 [!code-csharp[TextBox_MiscCode#_FocusTextBox](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_focustextbox)]
 [!code-vb[TextBox_MiscCode#_FocusTextBox](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_focustextbox)]  
  
## Vedere anche  
 <xref:System.Windows.UIElement.Focusable%2A>   
 <xref:System.Windows.UIElement.IsFocused%2A>   
 [Cenni preliminari sulla classe TextBox](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [Cenni generali sul controllo RichTextBox](../../../../docs/framework/wpf/controls/richtextbox-overview.md)