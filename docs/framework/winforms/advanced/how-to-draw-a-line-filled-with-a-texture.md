---
title: "Procedura: disegnare una linea con riempimento a trama | Microsoft Docs"
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
  - "disegno di linee, trama"
  - "disegno, linee"
  - "linee, trama"
ms.assetid: dc9118cc-f3c2-42e5-8173-f46d41d18fd5
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: disegnare una linea con riempimento a trama
Anziché tracciare una linea con un colore a tinta unita è possibile utilizzare una trama.  Per tracciare linee e curve con una trama, creare un oggetto <xref:System.Drawing.TextureBrush> e passarlo a un costruttore <xref:System.Drawing.Pen.%23ctor%2A>.  L'oggetto Bitmap associato al pennello a trama viene utilizzato per affiancare il piano in modo non visibile; quando la penna traccia una linea o una curva, il tratto della penna stessa rende visibili determinati pixel della trama affiancata.  
  
## Esempio  
 Nell'esempio che segue si crea un oggetto <xref:System.Drawing.Bitmap> dal file  `Texture1.jpg`.  L'oggetto Bitmap viene utilizzato per costruire un oggetto <xref:System.Drawing.TextureBrush>, il quale consente a sua volta di costruire un oggetto <xref:System.Drawing.Pen>.  Con la chiamata a <xref:System.Drawing.Graphics.DrawImage%2A> viene tracciato l'oggetto Bitmap con l'angolo superiore sinistro in posizione \(0, 0\).  Con la chiamata a <xref:System.Drawing.Graphics.DrawEllipse%2A> viene utilizzato l'oggetto <xref:System.Drawing.Pen> per tracciare un'ellisse a trama.  
  
 Nell'illustrazione che segue si mostrano l'oggetto Bitmap e l'ellisse a trama.  
  
 ![Oggetti Pen](../../../../docs/framework/winforms/advanced/media/pens7.png "pens7")  
  
 [!code-csharp[System.Drawing.UsingAPen#61](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#61)]
 [!code-vb[System.Drawing.UsingAPen#61](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#61)]  
  
## Compilazione del codice  
 Creare un Windows Form e gestire l'evento <xref:System.Windows.Forms.Control.Paint> del form.  Incollare il codice precedente nel gestore eventi <xref:System.Windows.Forms.Control.Paint>.  Sostituire  `Texture.jpg` con un'immagine disponibile sul proprio computer.  
  
## Vedere anche  
 [Utilizzo di un oggetto Pen per creare linee e forme](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)   
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)