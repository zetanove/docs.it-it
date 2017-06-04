---
title: "Procedura: creare un bordo intorno a un controllo di Windows Form mediante la spaziatura | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli [Windows Form], Margin (proprietà)"
  - "controlli [Windows Form], struttura"
  - "controlli [Windows Form], Padding (proprietà)"
  - "Margin (proprietà) [Windows Form]"
  - "margini"
  - "margini, Windows Form"
  - "Padding (proprietà) [Windows Form]"
  - "spaziatura, Windows Form"
ms.assetid: bac7ed4d-a163-4259-98bd-155a36345890
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: creare un bordo intorno a un controllo di Windows Form mediante la spaziatura
Nell'esempio di codice seguente viene illustrato come creare un bordo o un contorno intorno a un controllo <xref:System.Windows.Forms.RichTextBox>.  Il valore della proprietà <xref:System.Windows.Forms.Padding> di un controllo <xref:System.Windows.Forms.Panel> viene impostato su 5 e la proprietà <xref:System.Windows.Forms.Control.Dock%2A> di un controllo figlio <xref:System.Windows.Forms.RichTextBox> viene impostata su <xref:System.Windows.Forms.DockStyle>.  La proprietà <xref:System.Windows.Forms.Control.BackColor%2A> del controllo <xref:System.Windows.Forms.Panel> è impostata su <xref:System.Drawing.Color.Blue%2A>, che consente di creare un bordo blu intorno al controllo <xref:System.Windows.Forms.RichTextBox>.  
  
## Esempio  
 [!code-csharp[System.Windows.Forms.Padding#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Padding/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.Padding#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Padding/VB/Form1.vb#1)]  
  
## Vedere anche  
 <xref:System.Windows.Forms.Padding>   
 [Margini e spaziatura nei controlli Windows Form](../../../../docs/framework/winforms/controls/margin-and-padding-in-windows-forms-controls.md)