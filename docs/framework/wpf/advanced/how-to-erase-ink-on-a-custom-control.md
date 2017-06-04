---
title: "Procedura: cancellare l&#39;input penna da un controllo personalizzato | Microsoft Docs"
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
  - "controlli personalizzati, cancellazione di input penna"
  - "input penna, cancellazione da controllo personalizzato"
ms.assetid: d88c50f9-b4d8-4962-a28b-67d6a15a5fe0
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: cancellare l&#39;input penna da un controllo personalizzato
L'oggetto <xref:System.Windows.Ink.IncrementalStrokeHitTester> determina se il tratto attualmente tracciato si interseca con un altro tratto.  Questa funzionalità è utile per la creazione di un controllo che consente di cancellare parti di un tratto, la stessa operazione che è possibile eseguire su un oggetto <xref:System.Windows.Controls.InkCanvas> quando la proprietà <xref:System.Windows.Controls.InkCanvas.EditingMode%2A> è impostata su <xref:System.Windows.Controls.InkCanvasEditingMode>.  
  
## Esempio  
 Nell'esempio seguente viene creato un controllo personalizzato che consente all'utente di cancellare parti di tratti.  Il controllo creato contiene input penna quando viene inizializzato.  Per creare un controllo che raccoglie input penna, vedere [Creazione di un controllo di input penna](../../../../docs/framework/wpf/advanced/creating-an-ink-input-control.md).  
  
 [!code-csharp[HowToEraseInk#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToEraseInk/CSharp/InkEraser.cs#1)]
 [!code-vb[HowToEraseInk#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToEraseInk/VisualBasic/InkEraser.vb#1)]