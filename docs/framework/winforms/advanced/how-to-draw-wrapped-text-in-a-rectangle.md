---
title: "Procedura: creare testo disposto su pi&#249; righe in un rettangolo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "stringhe [Windows Form], creazione in un rettangolo"
  - "testo [Windows Form], creazione in un rettangolo"
  - "Windows Form, disegno di testo in un rettangolo"
ms.assetid: e1fb432a-dc90-48b5-9b6b-acc14507133d
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: creare testo disposto su pi&#249; righe in un rettangolo
È possibile creare testo disposto su più righe in un rettangolo utilizzando il metodo di overload <xref:System.Drawing.Graphics.DrawString%2A> della classe <xref:System.Drawing.Graphics> che accetta un parametro <xref:System.Drawing.Rectangle> o <xref:System.Drawing.RectangleF>.  Verranno inoltre utilizzate una classe <xref:System.Drawing.Brush> e una classe <xref:System.Drawing.Font>.  
  
 È possibile creare testo disposto su più righe in un rettangolo anche utilizzando il metodo di overload <xref:System.Windows.Forms.TextRenderer.DrawText%2A> della classe <xref:System.Windows.Forms.TextRenderer> che accetta una struttura <xref:System.Drawing.Rectangle> e un parametro <xref:System.Windows.Forms.TextFormatFlags>.  Verranno inoltre utilizzate una classe <xref:System.Drawing.Color> e una classe <xref:System.Drawing.Font>.  
  
 Nell'immagine riportata di seguito viene illustrato il risultato della creazione di testo nel rettangolo quando si utilizza il metodo <xref:System.Drawing.Graphics.DrawString%2A>.  
  
 ![Testo caratteri](../../../../docs/framework/winforms/advanced/media/csfontstext2.png "csfontstext2")  
  
### Per creare testo disposto su più righe in un rettangolo con GDI\+  
  
1.  Utilizzare il metodo di overload <xref:System.Drawing.Graphics.DrawString%2A> per passare il testo desiderato, la struttura <xref:System.Drawing.Rectangle> o <xref:System.Drawing.RectangleF>, la classe <xref:System.Drawing.Font> e la classe <xref:System.Drawing.Brush>.  
  
     [!code-csharp[System.Drawing.AlignDrawnText#50](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/CS/Form1.cs#50)]
     [!code-vb[System.Drawing.AlignDrawnText#50](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/VB/Form1.vb#50)]  
  
### Per creare testo disposto su più righe in un rettangolo con GDI  
  
1.  Utilizzare il valore dell'enumerazione <xref:System.Windows.Forms.TextFormatFlags> per specificare che il testo dovrà essere disposto su più righe con il metodo di overload <xref:System.Windows.Forms.TextRenderer.DrawText%2A> che passa il testo desiderato, la struttura <xref:System.Drawing.Rectangle>, la classe <xref:System.Drawing.Font> e la struttura <xref:System.Drawing.Color>.  
  
     [!code-csharp[System.Drawing.AlignDrawnText#60](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/CS/Form1.cs#60)]
     [!code-vb[System.Drawing.AlignDrawnText#60](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/VB/Form1.vb#60)]  
  
## Compilazione del codice  
 Gli esempi precedenti richiedono:  
  
-   <xref:System.Windows.Forms.PaintEventArgs> `e`, ovvero un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## Vedere anche  
 [Procedura: creare testo con GDI](../../../../docs/framework/winforms/advanced/how-to-draw-text-with-gdi.md)   
 [Utilizzo di tipi di carattere e testo](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)   
 [Procedura: creare caratteri e gruppi di caratteri](../../../../docs/framework/winforms/advanced/how-to-construct-font-families-and-fonts.md)   
 [Procedura: creare testo in una posizione specificata](../../../../docs/framework/winforms/advanced/how-to-draw-text-at-a-specified-location.md)