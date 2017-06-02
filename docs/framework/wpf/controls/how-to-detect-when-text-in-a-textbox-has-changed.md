---
title: "Procedura: rilevare eventuali modifiche del testo in un oggetto TextBox | Microsoft Docs"
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
  - "rilevamento delle modifiche del testo"
  - "modifiche del testo, rilevamento"
  - "TextBox (controllo), rilevamento delle modifiche del testo"
ms.assetid: 1c39ee14-e37f-49fb-a0d1-a9824ca13584
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: rilevare eventuali modifiche del testo in un oggetto TextBox
In questo esempio viene illustrata una modalità di utilizzo dell'evento <xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> per eseguire un metodo ogni volta che viene modificato il testo in un controllo <xref:System.Windows.Controls.TextBox>.  
  
 Nella classe code\-behind per [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] che contiene il controllo <xref:System.Windows.Controls.TextBox> di cui si intende monitorare le modifiche, inserire un metodo da chiamare ogni volta che viene generato l'evento <xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged>.  Questo metodo deve avere una firma corrispondente a quella prevista dal delegato <xref:System.Windows.Controls.TextChangedEventHandler>.  
  
 Il gestore eventi viene chiamato ogni volta che il contenuto del controllo <xref:System.Windows.Controls.TextBox> viene modificato, da un utente o a livello di codice.  
  
 **Nota:** questo evento viene generato quando il controllo <xref:System.Windows.Controls.TextBox> viene creato e compilato inizialmente con un testo.  
  
## Esempio  
 Nel codice [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] che definisce il controllo <xref:System.Windows.Controls.TextBox>, specificare l'attributo <xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> con un valore corrispondente al nome del metodo del gestore eventi.  
  
 [!code-xml[TextBox_MiscCode#_TextChangedXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_textchangedxaml)]  
  
## Esempio  
 Nella classe code\-behind per [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] che contiene il controllo <xref:System.Windows.Controls.TextBox> di cui si intende monitorare le modifiche, inserire un metodo da chiamare ogni volta che viene generato l'evento <xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged>.  Questo metodo deve avere una firma corrispondente a quella prevista dal delegato <xref:System.Windows.Controls.TextChangedEventHandler>.  
  
 [!code-csharp[TextBox_MiscCode#_TextChangedEventHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_textchangedeventhandler)]
 [!code-vb[TextBox_MiscCode#_TextChangedEventHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_textchangedeventhandler)]  
  
 Il gestore eventi viene chiamato ogni volta che il contenuto del controllo <xref:System.Windows.Controls.TextBox> viene modificato, da un utente o a livello di codice.  
  
 **Nota:** questo evento viene generato quando il controllo <xref:System.Windows.Controls.TextBox> viene creato e compilato inizialmente con un testo.  
  
 Commenti  
  
## Vedere anche  
 <xref:System.Windows.Controls.TextChangedEventArgs>   
 [Cenni preliminari sulla classe TextBox](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [Cenni generali sul controllo RichTextBox](../../../../docs/framework/wpf/controls/richtextbox-overview.md)