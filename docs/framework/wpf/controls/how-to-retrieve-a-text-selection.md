---
title: "Procedura: recuperare un testo selezionato | Microsoft Docs"
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
  - "recupero di testo"
  - "testo, recupero"
  - "TextBox (controllo), recupero di testo"
ms.assetid: d5793172-1e11-4a39-9be0-73f336ed858d
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: recuperare un testo selezionato
In questo esempio viene illustrato l'utilizzo della proprietà <xref:System.Windows.Controls.TextBox.SelectedText%2A> per recuperare il testo selezionato dall'utente in un controllo <xref:System.Windows.Controls.TextBox>.  
  
## Esempio  
 Nel seguente esempio [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] viene mostrata la definizione di un controllo <xref:System.Windows.Controls.TextBox> contenente del testo da selezionare e di un controllo <xref:System.Windows.Controls.Button> specificando un metodo <xref:System.Windows.Controls.Button.OnClick%2A>.  
  
 In questo esempio, un pulsante con un gestore eventi <xref:System.Windows.Controls.Primitives.ButtonBase.Click> associato viene utilizzato per recuperare il testo selezionato.  Quando l'utente fa clic sul pulsante, il metodo <xref:System.Windows.Controls.Button.OnClick%2A> copia in una stringa il testo selezionato nella casella di testo.  La particolare modalità di recupero del testo selezionato \(il clic su un pulsante\), nonché l'operazione eseguita su tale selezione \(la copia del testo selezionato in una stringa\) possono essere facilmente modificate in funzione di una molteplicità di scenari.  
  
 [!code-xml[TextBox_MiscCode#_TextBoxSelectTextXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_textboxselecttextxaml)]  
  
## Esempio  
 Nel seguente esempio [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)] viene mostrato un gestore di eventi <xref:System.Windows.Controls.Button.OnClick%2A> per il pulsante definito in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] di questo esempio.  
  
 [!code-csharp[TextBox_MiscCode#_SelectText](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_selecttext)]
 [!code-vb[TextBox_MiscCode#_SelectText](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_selecttext)]  
  
## Vedere anche  
 [Cenni preliminari sulla classe TextBox](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [Cenni generali sul controllo RichTextBox](../../../../docs/framework/wpf/controls/richtextbox-overview.md)