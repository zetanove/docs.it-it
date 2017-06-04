---
title: "Procedura: creare un pulsante con un&#39;immagine | Microsoft Docs"
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
  - "Button (controlli) [WPF], creazione"
ms.assetid: 607a193c-4098-4dd8-8dc0-51256cec2020
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: creare un pulsante con un&#39;immagine
In questo esempio viene illustrato come includere un'immagine in un oggetto <xref:System.Windows.Controls.Button>.  
  
## Esempio  
 Nell'esempio seguente vengono creati due controlli <xref:System.Windows.Controls.Button>.  Un controllo <xref:System.Windows.Controls.Button> contiene il testo, l'altro contiene un'immagine.  L'immagine è in una cartella denominata data, che è una sottocartella della cartella del progetto di esempio.  Quando un utente fa clic sul controllo <xref:System.Windows.Controls.Button> che contiene l'immagine, lo sfondo e il testo dell'altro controllo <xref:System.Windows.Controls.Button> viene modificato.  
  
 In questo esempio vengono creati i controlli <xref:System.Windows.Controls.Button> utilizzando markup, ma utilizza codice per scrivere i gestori degli eventi <xref:System.Windows.Controls.Primitives.ButtonBase.Click>.  
  
 [!code-xml[BtnColor#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BtnColor/CSharp/Pane1.xaml#4)]  
  
 [!code-csharp[BtnColor#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BtnColor/CSharp/Pane1.xaml.cs#6)]
 [!code-vb[BtnColor#6](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BtnColor/VisualBasic/Pane1.xaml.vb#6)]  
  
## Vedere anche  
 [Controlli](../../../../docs/framework/wpf/controls/index.md)   
 [Libreria di controlli](../../../../docs/framework/wpf/controls/control-library.md)