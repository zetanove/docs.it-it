---
title: "Percorsi di oggetti Graphics in GDI+ | Microsoft Docs"
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
  - "disegno, percorsi"
  - "GDI+, creazione di percorsi"
  - "grafica, percorsi"
  - "percorsi, disegno"
ms.assetid: a5500dec-666c-41fd-9da3-2169dd89c5eb
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Percorsi di oggetti Graphics in GDI+
I percorsi sono costituiti da combinazioni di linee, rettangoli e curve semplici.  Come indicato in [Cenni preliminari sulla grafica vettoriale](../../../../docs/framework/winforms/advanced/vector-graphics-overview.md), i seguenti blocchi predefiniti si sono rivelati i più efficienti per il disegno di immagini:  
  
-   Righe  
  
-   Rettangoli  
  
-   Ellissi  
  
-   Archi  
  
-   Poligoni  
  
-   Spline di tipo Cardinal  
  
-   Spline di Bézier  
  
 In GDI\+ l'oggetto <xref:System.Drawing.Drawing2D.GraphicsPath> consente di riunire in una singola unità una sequenza di tali blocchi predefiniti.  È quindi possibile tracciare l'intera sequenza di linee, rettangoli, poligoni e curve tramite una chiamata al metodo <xref:System.Drawing.Graphics.DrawPath%2A> della classe <xref:System.Drawing.Graphics>.  Nell'immagine seguente viene mostrato un percorso creato tramite una combinazione di una linea, un arco, una spline Bézier e una spline di tipo Cardinal.  
  
 ![Path](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art14.png "Aboutgdip02\_art14")  
  
## Utilizzo di un percorso  
 Nella classe <xref:System.Drawing.Drawing2D.GraphicsPath> sono disponibili i seguenti metodi per la creazione di una sequenza di elementi da tracciare: <xref:System.Drawing.Drawing2D.GraphicsPath.AddLine%2A>, <xref:System.Drawing.Drawing2D.GraphicsPath.AddRectangle%2A>, <xref:System.Drawing.Drawing2D.GraphicsPath.AddEllipse%2A>, <xref:System.Drawing.Drawing2D.GraphicsPath.AddArc%2A>, <xref:System.Drawing.Drawing2D.GraphicsPath.AddPolygon%2A>, <xref:System.Drawing.Drawing2D.GraphicsPath.AddCurve%2A> \(per le spline di tipo Cardinal\) e <xref:System.Drawing.Drawing2D.GraphicsPath.AddBezier%2A>.  Tutti questi metodi sono sottoposti a overload, ovvero ogni metodo supporta svariati elenchi di parametri diversi.  Una variazione del metodo <xref:System.Drawing.Drawing2D.GraphicsPath.AddLine%2A> ad esempio riceve quattro interi e un'altra variazione del metodo <xref:System.Drawing.Drawing2D.GraphicsPath.AddLine%2A> riceve due oggetti <xref:System.Drawing.Point>.  
  
 Ai metodi per l'aggiunta di linee, rettangoli e spline Bézier a un percorso sono associati più metodi correlati che consentono di aggiungere al percorso più elementi in un'unica chiamata: <xref:System.Drawing.Drawing2D.GraphicsPath.AddLines%2A>, <xref:System.Drawing.Drawing2D.GraphicsPath.AddRectangles%2A> e <xref:System.Drawing.Drawing2D.GraphicsPath.AddBeziers%2A>.  Anche ai metodi <xref:System.Drawing.Drawing2D.GraphicsPath.AddCurve%2A> e <xref:System.Drawing.Drawing2D.GraphicsPath.AddArc%2A> sono associati metodi correlati, <xref:System.Drawing.Drawing2D.GraphicsPath.AddClosedCurve%2A> e <xref:System.Drawing.Drawing2D.GraphicsPath.AddPie%2A>, che consentono di aggiungere una curva chiusa a una torta al percorso.  
  
 Per tracciare un percorso, sono necessari un oggetto <xref:System.Drawing.Graphics>, un oggetto <xref:System.Drawing.Pen> e un oggetto <xref:System.Drawing.Drawing2D.GraphicsPath>.  L'oggetto <xref:System.Drawing.Graphics> fornisce il metodo <xref:System.Drawing.Graphics.DrawPath%2A>, mentre nell'oggetto <xref:System.Drawing.Pen> sono memorizzati gli attributi, quale il colore e lo spessore, della linea utilizzata per eseguire il rendering del percorso.  Nell'oggetto <xref:System.Drawing.Drawing2D.GraphicsPath> viene memorizzata la sequenza di linee e curve che costituisce il percorso.  Gli oggetti <xref:System.Drawing.Pen> e <xref:System.Drawing.Drawing2D.GraphicsPath> vengono passati come argomenti al metodo <xref:System.Drawing.Graphics.DrawPath%2A>.  L'esempio seguente consente di tracciare un percorso costituito da una linea, un'ellisse e una spline Bézier:  
  
 [!code-csharp[LinesCurvesAndShapes#101](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#101)]
 [!code-vb[LinesCurvesAndShapes#101](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#101)]  
  
 Nell'immagine seguente viene mostrato il percorso.  
  
 ![Path](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art15.png "Aboutgdip02\_art15")  
  
 Oltre ad aggiungere linee, rettangoli e curve a un percorso, è possibile aggiungere percorsi a un percorso,  in modo da combinare percorsi esistenti per creare percorsi lunghi e complessi.  
  
 [!code-csharp[LinesCurvesAndShapes#102](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#102)]
 [!code-vb[LinesCurvesAndShapes#102](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#102)]  
  
 A un percorso è inoltre possibile aggiungere altri due elementi: stringhe e torte.  Una torta è una porzione dell'interno di un'ellisse.  L'esempio seguente consente di creare un percorso utilizzando un arco, una spline di tipo Cardinal, una stringa e una torta.  
  
 [!code-csharp[LinesCurvesAndShapes#103](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#103)]
 [!code-vb[LinesCurvesAndShapes#103](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#103)]  
  
 Nell'immagine seguente viene mostrato il percorso.  Si noti che non è necessario che un percorso sia collegato. L'arco, la spline di tipo Cardinal, la stringa e la torta sono separati.  
  
 ![Percorsi](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art16.png "Aboutgdip02\_Art16")  
  
## Vedere anche  
 <xref:System.Drawing.Drawing2D.GraphicsPath?displayProperty=fullName>   
 <xref:System.Drawing.Point?displayProperty=fullName>   
 [Linee, curve e forme](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [Procedura: creare oggetti Graphics per disegnare](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)   
 [Costruzione e creazione di percorsi](../../../../docs/framework/winforms/advanced/constructing-and-drawing-paths.md)