---
title: "Procedura: impostare il contenuto di testo di un controllo TextBox | Microsoft Docs"
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
  - "contenuto testo, impostazione"
  - "TextBox (controllo), impostazione del contenuto del testo"
ms.assetid: bcd25fc7-a52f-4453-b802-2c8d2b335ab8
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: impostare il contenuto di testo di un controllo TextBox
In questo esempio viene illustrata la modalità di utilizzo della proprietà <xref:System.Windows.Controls.TextBox.Text%2A> per l'impostazione del contenuto di testo iniziale di un controllo <xref:System.Windows.Controls.TextBox>.  
  
 **Nota** Anche se nella versione di [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] dell'esempio è possibile utilizzare i tag `<TextBox.Text>` per il contenuto <xref:System.Windows.Controls.TextBox> di ogni pulsante, non è tuttavia necessario perché l'oggetto <xref:System.Windows.Controls.TextBox> applica l'attributo <xref:System.Windows.Markup.ContentPropertyAttribute> alla proprietà <xref:System.Windows.Controls.TextBox.Text%2A>.  Per ulteriori informazioni, vedere [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md).  
  
## Esempio  
 [!code-xml[TextBox_MiscCode#_TextBoxSetTextXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_textboxsettextxaml)]  
  
## Esempio  
 [!code-csharp[TextBox_MiscCode#_TextBoxSetText](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_textboxsettext)]
 [!code-vb[TextBox_MiscCode#_TextBoxSetText](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_textboxsettext)]  
  
## Vedere anche  
 [Cenni preliminari sulla classe TextBox](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [Cenni generali sul controllo RichTextBox](../../../../docs/framework/wpf/controls/richtextbox-overview.md)