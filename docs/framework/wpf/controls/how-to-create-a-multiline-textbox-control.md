---
title: "Procedura: creare un controllo TextBox su pi&#249; righe | Microsoft Docs"
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
  - "TextBox (controllo), più righe di testo"
ms.assetid: 05914a93-d0ea-4a9a-b693-09df7d4e2ac2
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: creare un controllo TextBox su pi&#249; righe
In questo esempio viene illustrato come utilizzare [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] per definire un controllo <xref:System.Windows.Controls.TextBox> che si espanda automaticamente per inserire più righe di testo.  
  
## Esempio  
 Impostando l'attributo <xref:System.Windows.Controls.TextBox.TextWrapping%2A> su **Wrap**, il testo immesso va a capo in una nuova riga quando viene raggiunto il bordo del controllo <xref:System.Windows.Controls.TextBox>, espandendo automaticamente l'altezza del controllo <xref:System.Windows.Controls.TextBox> per includere eventualmente spazio per una riga nuova.  
  
 Impostando l'attributo <xref:System.Windows.Controls.Primitives.TextBoxBase.AcceptsReturn%2A> su **true** viene inserita una nuova riga quando viene premuto il tasto INVIO e anche in questo caso <xref:System.Windows.Controls.TextBox> si espande automaticamente per inserire, se necessario, una nuova riga.  
  
 L'attributo <xref:System.Windows.Controls.Primitives.TextBoxBase.VerticalScrollBarVisibility%2A> consente di aggiungere una barra di scorrimento al controllo <xref:System.Windows.Controls.TextBox>, affinché sia possibile scorrere il contenuto del controllo <xref:System.Windows.Controls.TextBox> qualora <xref:System.Windows.Controls.TextBox> si espanda oltre il frame o la finestra che lo contiene.  
  
 [!code-xml[TextBox_MiscCode#_MultilineTextBoxXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_multilinetextboxxaml)]  
  
## Vedere anche  
 <xref:System.Windows.TextWrapping>   
 [Cenni preliminari sulla classe TextBox](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [Cenni generali sul controllo RichTextBox](../../../../docs/framework/wpf/controls/richtextbox-overview.md)