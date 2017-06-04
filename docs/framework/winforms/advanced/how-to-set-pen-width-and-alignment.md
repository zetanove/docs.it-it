---
title: "Procedura: impostare la larghezza e l&#39;allineamento di un oggetto Pen | Microsoft Docs"
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
  - "penne, impostazione dell'allineamento"
  - "penne, impostazione della larghezza"
ms.assetid: a202af36-4d31-4401-a126-b232f51db581
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: impostare la larghezza e l&#39;allineamento di un oggetto Pen
Quando si crea un oggetto <xref:System.Drawing.Pen>, è possibile fornire la sua larghezza come uno degli argomenti al costruttore.  È inoltre possibile modificare tale larghezza tramite la proprietà <xref:System.Drawing.Pen.Width%2A> della classe <xref:System.Drawing.Pen>.  
  
 Una linea teorica ha larghezza pari a 0.  Quando si disegna una linea con larghezza pari a 1 pixel, i pixel vengono allineati al centro rispetto alla linea teorica.  Se si traccia una linea con larghezza maggiore di un pixel i pixel vengono centrati rispetto alla linea teorica oppure vengono visualizzati a lato di essa.  È possibile impostare la proprietà di allineamento della penna di un oggetto <xref:System.Drawing.Pen> per determinare la posizione relativa alle linee teoriche dei pixel disegnati con quella penna.  
  
 I valori <xref:System.Drawing.Drawing2D.PenAlignment>, <xref:System.Drawing.Drawing2D.PenAlignment> e <xref:System.Drawing.Drawing2D.PenAlignment> visualizzati negli esempi seguenti sono membri dell'enumerazione <xref:System.Drawing.Drawing2D.PenAlignment>.  
  
 Nell'esempio che segue si traccia una linea due volte: la prima con una penna di colore nero e larghezza 1, la seconda con una penna di colore verde e larghezza 10.  
  
### Per modificare la larghezza di una penna  
  
-   Impostare il valore della proprietà <xref:System.Drawing.Pen.Alignment%2A> su <xref:System.Drawing.Drawing2D.PenAlignment> \(impostazione predefinita\) per specificare che i pixel tracciati con la penna di colore verde saranno centrati rispetto alla linea teorica.  Nell'illustrazione che segue è visibile la linea risultante.  
  
     ![Oggetti Pen](../../../../docs/framework/winforms/advanced/media/pens1a.png "pens1A")  
  
     Nell'esempio che segue si traccia un rettangolo due volte: il primo con una penna di colore nero e larghezza 1, il secondo con una penna di colore verde e larghezza 10.  
  
     [!code-csharp[System.Drawing.UsingAPen#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#41)]
     [!code-vb[System.Drawing.UsingAPen#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#41)]  
  
### Per modificare l'allineamento di una penna  
  
-   Impostare il valore della proprietà <xref:System.Drawing.Pen.Alignment%2A> su <xref:System.Drawing.Drawing2D.PenAlignment> per specificare che i pixel tracciati con la penna di colore verde saranno centrati rispetto al limite del rettangolo.  
  
     Nell'illustrazione che segue si mostra il rettangolo risultante.  
  
     ![Oggetti Pen](../../../../docs/framework/winforms/advanced/media/pens2.png "pens2")  
  
     [!code-csharp[System.Drawing.UsingAPen#42](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#42)]
     [!code-vb[System.Drawing.UsingAPen#42](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#42)]  
  
### Per creare una penna di inserimento bordo  
  
-   È possibile modificare l'allineamento della penna di colore verde modificando come segue la terza istruzione nel codice precedente:  
  
     [!code-csharp[System.Drawing.UsingAPen#43](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#43)]
     [!code-vb[System.Drawing.UsingAPen#43](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#43)]  
  
     I pixel della linea verde più larga vengono ora visualizzati all'interno del rettangolo, come mostrato nell'illustrazione che segue.  
  
     ![Oggetti Pen](../../../../docs/framework/winforms/advanced/media/pens3.png "pens3")  
  
## Vedere anche  
 [Utilizzo di un oggetto Pen per creare linee e forme](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)   
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)