---
title: "Procedura: creare una forma con contorno | Microsoft Docs"
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
  - "Graphics.DrawEllipse"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "cerchi"
  - "cerchi, disegno"
  - "forme circolari"
  - "disegno, forme circolari"
  - "disegno, forme"
  - "ellissi, disegno"
  - "form, disegno di forme circolari"
  - "forme con contorni, disegno"
  - "forme con contorni, esempi"
  - "forme, disegno"
ms.assetid: f4f9214c-607e-407d-8cdd-6549f0278451
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: creare una forma con contorno
Nell'esempio riportato di seguito vengono creati ellissi e rettangoli con contorno in un form.  
  
## Esempio  
 [!code-cpp[System.Drawing.ConceptualHowTos#6](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#6)]
 [!code-csharp[System.Drawing.ConceptualHowTos#6](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#6)]
 [!code-vb[System.Drawing.ConceptualHowTos#6](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#6)]  
  
## Compilazione del codice  
 Non è possibile chiamare questo metodo nel gestore eventi <xref:System.Windows.Forms.Form.Load>.  Se il form viene ridimensionato o nascosto da un altro form, il contenuto creato non verrà ricreato.  Per ridisegnare automaticamente il contenuto è necessario eseguire l'override del metodo <xref:System.Windows.Forms.Control.OnPaint%2A>.  
  
## Programmazione efficiente  
 È sempre necessario chiamare il metodo <xref:System.IDisposable.Dispose%2A> sugli oggetti che richiedono un notevole utilizzo delle risorse di sistema, quali gli oggetti <xref:System.Drawing.Pen> e <xref:System.Drawing.Graphics>.  
  
## Vedere anche  
 <xref:System.Drawing.Graphics.DrawEllipse%2A>   
 <xref:System.Windows.Forms.Control.OnPaint%2A>   
 <xref:System.Drawing.Graphics.DrawRectangle%2A>   
 [Guida introduttiva alla programmazione grafica](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [Utilizzo di un oggetto Pen per creare linee e forme](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)   
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)