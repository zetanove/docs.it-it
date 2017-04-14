---
title: "Ellissi e archi in GDI+ | Microsoft Docs"
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
  - "archi"
  - "disegno, archi"
  - "disegno, ellissi"
  - "ellissi"
  - "GDI+, archi"
  - "GDI+, ellissi"
ms.assetid: 34f35133-a835-4ca4-81f6-0dfedee8b683
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Ellissi e archi in GDI+
È possibile disegnare con facilità ellissi e archi utilizzando i metodi <xref:System.Drawing.Graphics.DrawEllipse%2A> e <xref:System.Drawing.Graphics.DrawArc%2A> della classe <xref:System.Drawing.Graphics>.  
  
## Disegno di un'ellisse  
 Per disegnare un'ellisse, sono necessari un oggetto <xref:System.Drawing.Graphics> e un oggetto <xref:System.Drawing.Pen>.  L'oggetto <xref:System.Drawing.Graphics> fornisce il metodo <xref:System.Drawing.Graphics.DrawEllipse%2A>, mentre nell'oggetto <xref:System.Drawing.Pen> sono memorizzati gli attributi, quale il colore e lo spessore, della linea utilizzata per eseguire il rendering dell'ellisse.  L'oggetto <xref:System.Drawing.Pen> viene passato come argomento al metodo <xref:System.Drawing.Graphics.DrawEllipse%2A>.  Gli argomenti rimanenti passati al metodo <xref:System.Drawing.Graphics.DrawEllipse%2A> consentono di specificare il rettangolo di delimitazione dell'ellisse.  Nell'immagine seguente vengono mostrati un'ellisse e il relativo rettangolo di delimitazione.  
  
 ![Ellissi e archi](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art05.png "Aboutgdip02\_art05")  
  
 L'esempio seguente consente di tracciare un'ellisse. Il rettangolo di delimitazione ha larghezza di 80, altezza di 40 e angolo superiore sinistro nel punto \(100, 50\):  
  
 [!code-csharp[LinesCurvesAndShapes#51](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#51)]
 [!code-vb[LinesCurvesAndShapes#51](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#51)]  
  
 <xref:System.Drawing.Graphics.DrawEllipse%2A> è un metodo di overload della classe <xref:System.Drawing.Graphics>, quindi è possibile fornire argomenti a tale metodo in vari modi.  È ad esempio possibile costruire un oggetto <xref:System.Drawing.Rectangle> e passare tale oggetto <xref:System.Drawing.Rectangle> al metodo <xref:System.Drawing.Graphics.DrawEllipse%2A> come argomento:  
  
 [!code-csharp[LinesCurvesAndShapes#52](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#52)]
 [!code-vb[LinesCurvesAndShapes#52](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#52)]  
  
## Disegno di un arco  
 Un arco è una porzione di un'ellisse.  Per disegnare un arco, è necessario chiamare il metodo <xref:System.Drawing.Graphics.DrawArc%2A> della classe <xref:System.Drawing.Graphics>.  I parametri del metodo <xref:System.Drawing.Graphics.DrawArc%2A> sono uguali a quelli del metodo <xref:System.Drawing.Graphics.DrawEllipse%2A>, ma per <xref:System.Drawing.Graphics.DrawArc%2A> sono necessari un angolo iniziale e un angolo della curva.  L'esempio seguente consente di tracciare un arco con angolo iniziale di 30 gradi e angolo della curva di 180 gradi:  
  
 [!code-csharp[LinesCurvesAndShapes#53](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#53)]
 [!code-vb[LinesCurvesAndShapes#53](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#53)]  
  
 Nell'immagine seguente vengono mostrati l'arco, l'ellisse e il rettangolo di delimitazione.  
  
 ![Ellissi e archi](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art06.png "Aboutgdip02\_art06")  
  
## Vedere anche  
 <xref:System.Drawing.Graphics?displayProperty=fullName>   
 <xref:System.Drawing.Pen?displayProperty=fullName>   
 [Linee, curve e forme](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [Procedura: creare oggetti Graphics per disegnare](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)   
 [Procedura: creare un oggetto Pen](../../../../docs/framework/winforms/advanced/how-to-create-a-pen.md)   
 [Procedura: creare una forma con contorno](../../../../docs/framework/winforms/advanced/how-to-draw-an-outlined-shape.md)