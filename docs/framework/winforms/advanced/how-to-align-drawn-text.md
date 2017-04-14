---
title: "Procedura: allineare il testo creato | Microsoft Docs"
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
  - "testo, allineamento"
  - "Windows Form, allineamento del testo disegnato"
ms.assetid: 83c10a81-1a90-4b5c-98aa-2c6c4b280079
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: allineare il testo creato
Quando si esegue il disegno personalizzato, spesso può essere opportuno centrare il testo disegnato in un form o in un controllo.  Per facilitare l'allineamento del testo disegnato con i metodi <xref:System.Drawing.Graphics.DrawString%2A> o <xref:System.Windows.Forms.TextRenderer.DrawText%2A>, è possibile creare l'oggetto di formattazione corretto e impostare i flag di formato appropriati.  
  
### Per disegnare il testo centrato con GDI\+ \(DrawString\)  
  
1.  Utilizzare una classe <xref:System.Drawing.StringFormat> con il metodo <xref:System.Drawing.Graphics.DrawString%2A> appropriato per specificare il testo centrato.  
  
     [!code-csharp[System.Drawing.AlignDrawnText#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/CS/Form1.cs#10)]
     [!code-vb[System.Drawing.AlignDrawnText#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/VB/Form1.vb#10)]  
  
### Per disegnare il testo centrato con GDI \(DrawText\)  
  
1.  Utilizzare l'enumerazione <xref:System.Windows.Forms.TextFormatFlags> per il riporto a capo e la centratura verticale e orizzontale del testo con il metodo <xref:System.Windows.Forms.TextRenderer.DrawText%2A> appropriato.  
  
     [!code-csharp[System.Drawing.AlignDrawnText#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/CS/Form1.cs#20)]
     [!code-vb[System.Drawing.AlignDrawnText#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlignDrawnText/VB/Form1.vb#20)]  
  
## Compilazione del codice  
 Gli esempi di codice riportati in precedenza sono stati creati per essere utilizzati con Windows Forms e richiedono <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## Vedere anche  
 [Procedura: creare testo con GDI](../../../../docs/framework/winforms/advanced/how-to-draw-text-with-gdi.md)   
 [Utilizzo di tipi di carattere e testo](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)   
 [Procedura: creare caratteri e gruppi di caratteri](../../../../docs/framework/winforms/advanced/how-to-construct-font-families-and-fonts.md)