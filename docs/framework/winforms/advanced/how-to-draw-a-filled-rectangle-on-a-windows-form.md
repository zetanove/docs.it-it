---
title: "Procedura: disegnare un rettangolo con riempimento in un Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Graphics.FillRectangle"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "disegno di rettangoli"
  - "disegno, rettangoli"
  - "rettangoli, disegno"
ms.assetid: d656a93c-987d-4809-aafd-493fe17450f0
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: disegnare un rettangolo con riempimento in un Windows Form
Nell'esempio riportato di seguito viene creato un rettangolo pieno in un form.  
  
## Esempio  
 [!code-cpp[System.Drawing.ConceptualHowTos#2](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#2)]
 [!code-csharp[System.Drawing.ConceptualHowTos#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#2)]
 [!code-vb[System.Drawing.ConceptualHowTos#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#2)]  
  
## Compilazione del codice  
 Non è possibile chiamare questo metodo nel gestore eventi <xref:System.Windows.Forms.Form.Load>.  Se il form viene ridimensionato o nascosto da un altro form, il contenuto creato non verrà ricreato.  Per ridisegnare automaticamente il contenuto è necessario eseguire l'override del metodo <xref:System.Windows.Forms.Control.OnPaint%2A>.  
  
## Programmazione efficiente  
 È sempre necessario chiamare il metodo <xref:System.IDisposable.Dispose%2A> sugli oggetti che richiedono un notevole utilizzo delle risorse di sistema, quali gli oggetti <xref:System.Drawing.Brush> e <xref:System.Drawing.Graphics>.  
  
## Vedere anche  
 <xref:System.Drawing.Graphics.FillRectangle%2A>   
 <xref:System.Windows.Forms.Control.OnPaint%2A>   
 [Guida introduttiva alla programmazione grafica](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [Utilizzo di un oggetto Pen per creare linee e forme](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)   
 [Pennelli e forme con riempimento in GDI\+](../../../../docs/framework/winforms/advanced/brushes-and-filled-shapes-in-gdi.md)