---
title: "Procedura: creare testo in una posizione specificata | Microsoft Docs"
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
  - "creazione di testo"
  - "creazione di testo, posizioni specificate [Windows Form]"
  - "testo, disegno in posizioni specificate [Windows Form]"
  - "Windows Form, disegno di testo in una posizione specificata"
ms.assetid: 60816423-1c38-465e-980d-2c2b64d74086
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Procedura: creare testo in una posizione specificata
Quando si esegue il disegno personalizzato, è possibile creare testo in un'unica riga orizzontale partendo da un punto specificato.  È possibile creare testo in questa maniera utilizzando il metodo di overload <xref:System.Drawing.Graphics.DrawString%2A> della classe <xref:System.Drawing.Graphics> che accetta un parametro <xref:System.Drawing.Point> o <xref:System.Drawing.PointF>.  Il metodo <xref:System.Drawing.Graphics.DrawString%2A> richiede anche una classe <xref:System.Drawing.Brush> e <xref:System.Drawing.Font>.  
  
 È inoltre possibile utilizzare il metodo di overload <xref:System.Windows.Forms.TextRenderer.DrawText%2A> della classe <xref:System.Windows.Forms.TextRenderer> che accetta una struttura <xref:System.Drawing.Point>.  Inoltre, <xref:System.Windows.Forms.TextRenderer.DrawText%2A> richiede un parametro <xref:System.Drawing.Color> e un parametro <xref:System.Drawing.Font>.  
  
 Nell'immagine riportata di seguito viene illustrato il risultato della creazione di testo in un punto specificato quando si utilizza il metodo di overload <xref:System.Drawing.Graphics.DrawString%2A>.  
  
 ![Testo caratteri](../../../../docs/framework/winforms/advanced/media/csfontstext1.png "csfontstext1")  
  
### Per disegnare una riga di testo con GDI\+  
  
1.  Utilizzare il metodo <xref:System.Drawing.Graphics.DrawString%2A> per passare il testo desiderato, la struttura <xref:System.Drawing.Point> o <xref:System.Drawing.PointF>, la classe <xref:System.Drawing.Font> e la classe <xref:System.Drawing.Brush>.  
  
     [!code-csharp[System.Drawing.AlignDrawnText#30](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/CS/Form1.cs#30)]
     [!code-vb[System.Drawing.AlignDrawnText#30](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/VB/Form1.vb#30)]  
  
### Per disegnare una riga di testo con GDI  
  
1.  Utilizzare il metodo <xref:System.Windows.Forms.TextRenderer.DrawText%2A> per passare il testo desiderato, la struttura <xref:System.Drawing.Point>, la classe <xref:System.Drawing.Font> e la struttura <xref:System.Drawing.Color>.  
  
     [!code-csharp[System.Drawing.AlignDrawnText#40](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/CS/Form1.cs#40)]
     [!code-vb[System.Drawing.AlignDrawnText#40](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/VB/Form1.vb#40)]  
  
## Compilazione del codice  
 Gli esempi precedenti richiedono:  
  
-   <xref:System.Windows.Forms.PaintEventArgs>  `e`, ovvero un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## Vedere anche  
 [Procedura: creare testo con GDI](../../../../docs/framework/winforms/advanced/how-to-draw-text-with-gdi.md)   
 [Utilizzo di tipi di carattere e testo](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)   
 [Procedura: creare caratteri e gruppi di caratteri](../../../../docs/framework/winforms/advanced/how-to-construct-font-families-and-fonts.md)   
 [Procedura: creare testo disposto su più righe in un rettangolo](../../../../docs/framework/winforms/advanced/how-to-draw-wrapped-text-in-a-rectangle.md)