---
title: "Poligoni in GDI+ | Microsoft Docs"
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
  - "disegno, poligoni"
  - "GDI+, poligoni"
  - "poligoni"
ms.assetid: a72213d2-d69a-4c2b-a75c-be7b20390c13
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Poligoni in GDI+
Un poligono è una forma chiusa con tre o più lati diritti.  Un triangolo ad esempio è un poligono con tre lati, un rettangolo è un poligono con quattro lati e un pentagono è un poligono con cinque lati.  Nell'immagine seguente vengono mostrati alcuni poligoni.  
  
 ![Poligoni](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art07.png "Aboutgdip02\_art07")  
  
## Creazione di un poligono  
 Per tracciare un poligono, sono necessari un oggetto <xref:System.Drawing.Graphics>, un oggetto <xref:System.Drawing.Pen> e una matrice di oggetti <xref:System.Drawing.Point> \(o <xref:System.Drawing.PointF>\).  L'oggetto <xref:System.Drawing.Graphics> fornisce il metodo <xref:System.Drawing.Graphics.DrawPolygon%2A>.  Nell'oggetto <xref:System.Drawing.Pen> vengono memorizzati gli attributi, quale lo spessore e il colore, della linea utilizzata per il rendering del poligono e nella matrice di oggetti <xref:System.Drawing.Point> sono memorizzati i punti da connettere tramite linee rette.  L'oggetto <xref:System.Drawing.Pen> e la matrice di oggetti <xref:System.Drawing.Point> vengono passati come argomenti al metodo <xref:System.Drawing.Graphics.DrawPolygon%2A>.  L'esempio seguente consente di tracciare un poligono a tre lati.  Si noti che in  `myPointArray` sono specificati solo tre punti: \(0, 0\), \(50, 30\) e \(30, 60\).  Il metodo <xref:System.Drawing.Graphics.DrawPolygon%2A> chiude automaticamente il poligono tracciando una linea da \(30, 60\) al punto iniziale \(0, 0\).  
  
 [!code-csharp[LinesCurvesAndShapes#111](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#111)]
 [!code-vb[LinesCurvesAndShapes#111](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#111)]  
  
 Nell'immagine seguente viene mostrato il poligono.  
  
 ![Poligono](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art08.png "Aboutgdip02\_art08")  
  
## Vedere anche  
 <xref:System.Drawing.Graphics?displayProperty=fullName>   
 <xref:System.Drawing.Pen?displayProperty=fullName>   
 [Linee, curve e forme](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [Procedura: creare un oggetto Pen](../../../../docs/framework/winforms/advanced/how-to-create-a-pen.md)