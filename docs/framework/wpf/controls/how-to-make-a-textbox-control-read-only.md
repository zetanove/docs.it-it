---
title: "Procedura: impostare la propriet&#224; di sola lettura per un controllo TextBox | Microsoft Docs"
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
  - "sola lettura (controlli TextBox)"
  - "TextBox (controlli di sola lettura)"
ms.assetid: e707ec59-8b22-473e-b77c-3060a237517a
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: impostare la propriet&#224; di sola lettura per un controllo TextBox
In questo esempio viene illustrato come configurare un controllo <xref:System.Windows.Controls.TextBox> al fine di impedire input o modifiche dell'utente.  
  
## Esempio  
 Per impedire agli utenti di modificare il contenuto di un controllo <xref:System.Windows.Controls.TextBox>, impostare l'attributo <xref:System.Windows.Controls.Primitives.TextBoxBase.IsReadOnly%2A> su **true**.  
  
 [!code-xml[TextBox_MiscCode#_ReadOnlyTextBoxXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_readonlytextboxxaml)]  
  
 L'attributo <xref:System.Windows.Controls.Primitives.TextBoxBase.IsReadOnly%2A> influisce solo sull'input dell'utente e non sul testo impostato nella descrizione [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] di un controllo <xref:System.Windows.Controls.TextBox> o sul testo impostato a livello di codice mediante la proprietà <xref:System.Windows.Controls.TextBox.Text%2A>.  
  
 Il valore predefinito di <xref:System.Windows.Controls.Primitives.TextBoxBase.IsReadOnly%2A> è **false**.  
  
## Vedere anche  
 [Cenni preliminari sulla classe TextBox](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [Cenni generali sul controllo RichTextBox](../../../../docs/framework/wpf/controls/richtextbox-overview.md)