---
title: "Procedura: ottenere una raccolta di righe da un controllo TextBox | Microsoft Docs"
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
  - "linee, recupero di raccolte"
  - "TextBox (controllo), recupero di raccolte di linee"
ms.assetid: a12f529d-b926-47f6-92bf-cad5f17b532a
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: ottenere una raccolta di righe da un controllo TextBox
In questo esempio viene mostrato come ottenere una raccolta di righe di testo da un oggetto <xref:System.Windows.Controls.TextBox>.  
  
## Esempio  
 Nell'esempio seguente viene mostrato un semplice metodo che accetta un oggetto <xref:System.Windows.Controls.TextBox> come argomento e restituisce un oggetto <xref:System.Collections.Specialized.StringCollection> contenente le righe di testo in **TextBox**.  La proprietà <xref:System.Windows.Controls.TextBox.LineCount%2A> viene utilizzata per determinare il numero di righe attualmente presente in **TextBox** e il metodo <xref:System.Windows.Controls.TextBox.GetLineText%2A> viene quindi utilizzato per estrarre ciascuna riga e aggiungerla alla relativa raccolta.  
  
 [!code-csharp[TextBox_MiscCode#_TextBox_GetLines](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_textbox_getlines)]  
  
## Vedere anche  
 [Cenni preliminari sulla classe TextBox](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [Cenni generali sul controllo RichTextBox](../../../../docs/framework/wpf/controls/richtextbox-overview.md)