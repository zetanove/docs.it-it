---
title: "Penne, linee e rettangoli in GDI+ | Microsoft Docs"
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
  - "disegno, linee"
  - "disegno, rettangoli"
  - "esempi [Windows Form], disegno di linee e forme"
  - "esempi [Windows Form], GDI+"
  - "esempi [Windows Form], penne"
  - "GDI+, linee"
  - "GDI+, penne"
  - "GDI+, rettangoli"
  - "linee"
  - "linee, tratteggiate"
  - "rettangoli"
ms.assetid: 30b25aae-e3eb-4479-bdb8-187cf651fc84
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Penne, linee e rettangoli in GDI+
Per tracciare linee con [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è necessario creare un oggetto <xref:System.Drawing.Graphics> e un oggetto <xref:System.Drawing.Pen>.  L'oggetto <xref:System.Drawing.Graphics> fornisce i metodi che consentono di tracciare effettivamente l'elemento, mentre nell'oggetto <xref:System.Drawing.Pen> sono memorizzati gli attributi, quale il colore, lo spessore e lo stile della linea.  
  
## Creazione di una linea  
 Per tracciare una linea, chiamare il metodo <xref:System.Drawing.Graphics.DrawLine%2A> dell'oggetto <xref:System.Drawing.Graphics>.  L'oggetto <xref:System.Drawing.Pen> viene passato come uno degli argomenti al metodo <xref:System.Drawing.Graphics.DrawLine%2A>.  L'esempio seguente consente di tracciare una linea che unisce il punto \(4, 2\) al punto \(12, 6\):  
  
 [!code-csharp[LinesCurvesAndShapes#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#41)]
 [!code-vb[LinesCurvesAndShapes#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#41)]  
  
 <xref:System.Drawing.Graphics.DrawLine%2A> è un metodo di overload della classe <xref:System.Drawing.Graphics>, quindi è possibile fornire argomenti a tale metodo in svariati modi.  È ad esempio possibile costruire due oggetti <xref:System.Drawing.Point> e passarli come argomenti al metodo <xref:System.Drawing.Graphics.DrawLine%2A>:  
  
 [!code-csharp[LinesCurvesAndShapes#42](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#42)]
 [!code-vb[LinesCurvesAndShapes#42](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#42)]  
  
## Costruzione di una penna  
 Quando si costruisce un oggetto <xref:System.Drawing.Pen>, è possibile specificare determinati attributi.  Un costruttore `Pen` consente ad esempio di specificare il colore e lo spessore.  L'esempio seguente consente di tracciare una linea blu con spessore 2 da \(0, 0\) a \(60, 30\):  
  
 [!code-csharp[LinesCurvesAndShapes#43](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#43)]
 [!code-vb[LinesCurvesAndShapes#43](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#43)]  
  
## Linee tratteggiate ed estremità di linea  
 L'oggetto <xref:System.Drawing.Pen> espone inoltre proprietà, come <xref:System.Drawing.Pen.DashStyle%2A>, che possono essere utilizzate per specificare caratteristiche della linea.  L'esempio seguente consente di tracciare una linea tratteggiata da \(100, 50\) a \(300, 80\):  
  
 [!code-csharp[LinesCurvesAndShapes#44](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#44)]
 [!code-vb[LinesCurvesAndShapes#44](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#44)]  
  
 È possibile utilizzare le proprietà dell'oggetto <xref:System.Drawing.Pen> per impostare molti altri attributi della linea.  Le proprietà <xref:System.Drawing.Pen.StartCap%2A> e <xref:System.Drawing.Pen.EndCap%2A> specificano l'aspetto delle estremità della linea, che possono essere senza effetti, quadrate, arrotondate, triangolari oppure possono assumere una forma personalizzata.  La proprietà <xref:System.Drawing.Pen.LineJoin%2A> consente di specificare se le linee connesse siano unite con angoli netti, unite con angoli smussati, se siano arrotondate o troncate.  Nell'immagine seguente vengono mostrate linee con diversi stili di terminazione e unione.  
  
 ![Linee](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art04.png "Aboutgdip02\_art04")  
  
## Disegno di un rettangolo  
 La procedura per tracciare rettangoli in [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è simile a quella che consente di tracciare linee.  Per tracciare un rettangolo, sono necessari un oggetto <xref:System.Drawing.Graphics> e un oggetto <xref:System.Drawing.Pen>.  L'oggetto <xref:System.Drawing.Graphics> fornisce il metodo <xref:System.Drawing.Graphics.DrawRectangle%2A>, mentre nell'oggetto <xref:System.Drawing.Pen> sono memorizzati gli attributi, quale il colore e lo spessore della linea.  L'oggetto <xref:System.Drawing.Pen> viene passato come uno degli argomenti del metodo <xref:System.Drawing.Graphics.DrawRectangle%2A>.  L'esempio seguente consente di tracciare un rettangolo con angolo superiore sinistro nel punto \(100, 50\), larghezza di 80 e altezza di 40:  
  
 [!code-csharp[LinesCurvesAndShapes#45](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#45)]
 [!code-vb[LinesCurvesAndShapes#45](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#45)]  
  
 <xref:System.Drawing.Graphics.DrawRectangle%2A> è un metodo di overload della classe <xref:System.Drawing.Graphics>, quindi è possibile fornire argomenti a tale metodo in svariati modi.  È ad esempio possibile costruire un oggetto <xref:System.Drawing.Rectangle> e passarlo come argomento al metodo <xref:System.Drawing.Graphics.DrawRectangle%2A>:  
  
 [!code-csharp[LinesCurvesAndShapes#46](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#46)]
 [!code-vb[LinesCurvesAndShapes#46](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#46)]  
  
 All'oggetto <xref:System.Drawing.Rectangle> sono associati metodi e proprietà per la modifica e la raccolta di informazioni relative al rettangolo.  I metodi <xref:System.Drawing.Rectangle.Inflate%2A> e <xref:System.Drawing.Rectangle.Offset%2A>, ad esempio, consentono di cambiare la dimensione e la posizione del rettangolo.  Il metodo <xref:System.Drawing.Rectangle.IntersectsWith%2A> fornisce informazioni sull'eventuale intersezione del rettangolo con un altro rettangolo specificato e il metodo <xref:System.Drawing.Rectangle.Contains%2A> indica se un dato punto si trova all'interno del rettangolo.  
  
## Vedere anche  
 <xref:System.Drawing.Graphics?displayProperty=fullName>   
 <xref:System.Drawing.Pen?displayProperty=fullName>   
 <xref:System.Drawing.Rectangle?displayProperty=fullName>   
 [Procedura: creare un oggetto Pen](../../../../docs/framework/winforms/advanced/how-to-create-a-pen.md)   
 [Procedura: disegnare una linea in un Windows Form](../../../../docs/framework/winforms/advanced/how-to-draw-a-line-on-a-windows-form.md)   
 [Procedura: creare una forma con contorno](../../../../docs/framework/winforms/advanced/how-to-draw-an-outlined-shape.md)