---
title: "Procedura: estrarre il contenuto di testo da un oggetto RichTextBox | Microsoft Docs"
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
  - "contenuto, estrazione"
  - "estrazione di contenuto testo"
  - "RichTextBox (controllo), estrazione di contenuto testo"
  - "contenuto testo, estrazione"
ms.assetid: f13c093f-1a05-45b3-ac8f-c9ea5e4a11c5
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: estrarre il contenuto di testo da un oggetto RichTextBox
In questo esempio viene mostrato come estrarre il contenuto di un oggetto <xref:System.Windows.Controls.RichTextBox> come testo normale.  
  
## Esempio  
 Nel codice [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] riportato di seguito viene descritto un controllo <xref:System.Windows.Controls.RichTextBox> denominato con contenuto semplice.  
  
 [!code-xml[RichTextBoxSnippets#_RTB_XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxSnippets/CSharp/Window1.xaml#_rtb_xaml)]  
  
## Esempio  
 Nel codice seguente viene implementato un metodo che accetta un oggetto <xref:System.Windows.Controls.RichTextBox> come argomento e restituisce una stringa che rappresenta il contenuto di testo normale dell'oggetto <xref:System.Windows.Controls.RichTextBox>.  
  
 Il metodo crea un nuovo oggetto <xref:System.Windows.Documents.TextRange> dai contenuti dell'oggetto <xref:System.Windows.Controls.RichTextBox>, utilizzando <xref:System.Windows.Documents.FlowDocument.ContentStart%2A> e <xref:System.Windows.Documents.FlowDocument.ContentEnd%2A> per indicare l'intervallo di contenuti da estrarre.  Le proprietà <xref:System.Windows.Documents.FlowDocument.ContentStart%2A> e <xref:System.Windows.Documents.FlowDocument.ContentEnd%2A> restituiscono <xref:System.Windows.Documents.TextPointer> e sono accessibili sul FlowDocument sottostante che rappresenta i contenuti di <xref:System.Windows.Controls.RichTextBox>.  <xref:System.Windows.Documents.TextRange> fornisce una proprietà Text che restituisce le parti di testo normale di <xref:System.Windows.Documents.TextRange> come stringa.  
  
 [!code-csharp[RichTextBoxSnippets#_RTB_StringFrom](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxSnippets/CSharp/Window1.xaml.cs#_rtb_stringfrom)]
 [!code-vb[RichTextBoxSnippets#_RTB_StringFrom](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBoxSnippets/visualbasic/window1.xaml.vb#_rtb_stringfrom)]  
  
## Vedere anche  
 [Cenni generali sul controllo RichTextBox](../../../../docs/framework/wpf/controls/richtextbox-overview.md)   
 [Cenni preliminari sulla classe TextBox](../../../../docs/framework/wpf/controls/textbox-overview.md)