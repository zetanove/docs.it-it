---
title: "Procedura: aggiungere una filigrana a un oggetto TextBox | Microsoft Docs"
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
  - "migliorare l'usabilità di un controllo Textbox con un'immagine di sfondo [WPF]"
  - "visualizzazione di un'immagine di sfondo in una casella di testo per migliorare l'input utente [WPF]"
ms.assetid: df89bdd8-a0fb-45e0-b312-dd53332d01a8
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: aggiungere una filigrana a un oggetto TextBox
Nell'esempio seguente viene mostrato come migliorare la possibilità di utilizzo di un oggetto <xref:System.Windows.Controls.TextBox> visualizzando un'immagine di sfondo esplicativa all'interno di un oggetto <xref:System.Windows.Controls.TextBox> fino a quando l'utente immette un testo; a quel punto l'immagine viene rimossa.  Inoltre, l'immagine di sfondo viene ripristinata nuovamente se l'utente rimuove l'input.  Vedere l'illustrazione di seguito.  
  
 ![TextBox con immagine di sfondo](../../../../docs/framework/wpf/controls/media/editing-textbox-using-background-image.png "Editing\_TextBox\_using\_background\_image")  
  
> [!NOTE]
>  La ragione per la quale in questo esempio viene utilizzata un'immagine di sfondo piuttosto che modificare semplicemente la proprietà <xref:System.Windows.Controls.TextBox.Text%2A> dell'oggetto <xref:System.Windows.Controls.TextBox> sta nel fatto che un'immagine di sfondo non interferisce con l'associazione dati.  
  
## Esempio  
 [!code-xml[TextBoxMiscSnippets_snip#TextBoxBackgroundExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/textbox_with_background_image.xaml#textboxbackgroundexamplewholepage)]  
  
 [!code-csharp[TextBoxMiscSnippets_snip#TextBoxBackgroundCodeExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/textbox_with_background_image.xaml.cs#textboxbackgroundcodeexamplewholepage)]
 [!code-vb[TextBoxMiscSnippets_snip#TextBoxBackgroundCodeExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/visualbasic/textbox_with_background_image.xaml.vb#textboxbackgroundcodeexamplewholepage)]  
  
## Vedere anche  
 [Cenni preliminari sulla classe TextBox](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [Cenni generali sul controllo RichTextBox](../../../../docs/framework/wpf/controls/richtextbox-overview.md)