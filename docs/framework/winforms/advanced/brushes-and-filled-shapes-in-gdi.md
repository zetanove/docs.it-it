---
title: "Pennelli e forme con riempimento in GDI+ | Microsoft Docs"
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
  - "pennelli, GDI+"
  - "pennelli, gradiente"
  - "forme piene, GDI+"
  - "GDI+, pennelli"
  - "GDI+, forme piene"
  - "pennelli per sfumature"
  - "forme, GDI+"
ms.assetid: e863e2a7-0294-4130-99b6-f1ea3201e7cd
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Pennelli e forme con riempimento in GDI+
Una forma chiusa, quale un rettangolo o un'ellisse, è costituita da un contorno e da un interno.  Il contorno viene tracciato con una penna e l'interno viene riempito con un pennello.  In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] sono disponibili diverse classi di pennelli per il riempimento dell'interno di forme chiuse: <xref:System.Drawing.SolidBrush>, <xref:System.Drawing.Drawing2D.HatchBrush>, <xref:System.Drawing.TextureBrush>, <xref:System.Drawing.Drawing2D.LinearGradientBrush> e <xref:System.Drawing.Drawing2D.PathGradientBrush>.  Tutte queste classi ereditano dalla classe <xref:System.Drawing.Brush>.  Nell'immagine seguente viene mostrato un rettangolo riempito con un pennello a tinta unita e una ellisse riempita con un pennello tratteggiato.  
  
 ![Forme piene](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art17.png "Aboutgdip02\_art17")  
  
## Pennelli a tinta unita  
 Per riempire una forma chiusa, sono necessari un'istanza della classe <xref:System.Drawing.Graphics> e <xref:System.Drawing.Brush>.  L'istanza della classe <xref:System.Drawing.Graphics> fornisce i metodi, quali <xref:System.Drawing.Graphics.FillRectangle%2A> e <xref:System.Drawing.Graphics.FillEllipse%2A> mentre nell'oggetto <xref:System.Drawing.Brush> vengono memorizzati gli attributi del riempimento, quali il colore e il motivo.  L'oggetto <xref:System.Drawing.Brush> viene passato come uno degli argomenti al metodo di riempimento.  Nell'esempio che segue è illustrato come riempire un'ellisse con il colore rosso a tinta unita.  
  
 [!code-csharp[LinesCurvesAndShapes#121](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#121)]
 [!code-vb[LinesCurvesAndShapes#121](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#121)]  
  
> [!NOTE]
>  Nell'esempio precedente il pennello è di tipo <xref:System.Drawing.SolidBrush> ed eredita da <xref:System.Drawing.Brush>.  
  
## Pennello tratteggiato  
 Quando si riempie una forma con un pennello tratteggiato, si specifica un colore di primo piano, un colore di sfondo e uno stile di tratteggio.  Il colore di primo piano è il colore utilizzato per il tratteggio.  
  
 [!code-csharp[LinesCurvesAndShapes#122](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#122)]
 [!code-vb[LinesCurvesAndShapes#122](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#122)]  
  
 In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] sono disponibili oltre 50 stili di tratteggio. I tre stili mostrati nell'immagine seguente sono <xref:System.Drawing.Drawing2D.HatchStyle>, <xref:System.Drawing.Drawing2D.HatchStyle> e <xref:System.Drawing.Drawing2D.HatchStyle>.  
  
 ![Forme piene](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art18.png "Aboutgdip02\_art18")  
  
## Pennelli a trama  
 Un pennello a trama consente di riempire una forma con un modello memorizzato in una bitmap.  Si supponga ad esempio che l'immagine seguente sia memorizzata in un file su disco con nome `MyTexture.bmp`.  
  
 ![Forma piena](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art19.png "Aboutgdip02\_Art19")  
  
 L'esempio seguente consente di riempire un'ellisse ripetendo l'immagine memorizzata in `MyTexture.bmp`.  
  
 [!code-csharp[LinesCurvesAndShapes#123](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#123)]
 [!code-vb[LinesCurvesAndShapes#123](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#123)]  
  
 Nell'illustrazione che segue viene mostrata l'ellisse riempita.  
  
 ![Forma piena](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art20.png "AboutGdip02\_Art20")  
  
## Pennelli sfumati  
 In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] sono disponibili due tipi di pennelli sfumati: lineare e di percorso.  Un pennello sfumato lineare consente di riempire una forma con un colore che sfuma gradatamente in un altro colore lungo la forma, orizzontalmente, verticalmente o in diagonale.  L'esempio seguente consente di riempire un'ellisse con un pennello sfumato orizzontale il cui colore passa da blu a verde a partire dal margine sinistro dell'ellisse verso il margine destro.  
  
 [!code-csharp[LinesCurvesAndShapes#124](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#124)]
 [!code-vb[LinesCurvesAndShapes#124](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#124)]  
  
 Nell'illustrazione che segue viene mostrata l'ellisse riempita.  
  
 ![Forma piena](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art21.png "AboutGdip02\_Art21")  
  
 È possibile configurare un pennello sfumato di percorso in modo che il colore sfumi a partire dal centro di un'immagine e verso i contorni.  
  
 ![Forma piena](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art22.png "AboutGdip02\_Art22")  
  
 I pennelli sfumati di percorso sono abbastanza flessibili.  Il pennello sfumato utilizzato per riempire il triangolo mostrato nell'immagine seguente consente di sfumare gradualmente dal colore rosso del centro a tre colori diversi per i vertici.  
  
 ![Forma piena](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art23.png "AboutGdip02\_Art23")  
  
## Vedere anche  
 <xref:System.Drawing.SolidBrush?displayProperty=fullName>   
 <xref:System.Drawing.Drawing2D.HatchBrush?displayProperty=fullName>   
 <xref:System.Drawing.TextureBrush?displayProperty=fullName>   
 <xref:System.Drawing.Drawing2D.LinearGradientBrush?displayProperty=fullName>   
 [Linee, curve e forme](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [Procedura: disegnare un rettangolo con riempimento in un Windows Form](../../../../docs/framework/winforms/advanced/how-to-draw-a-filled-rectangle-on-a-windows-form.md)   
 [Procedura: disegnare un'ellisse con riempimento in un Windows Form](../../../../docs/framework/winforms/advanced/how-to-draw-a-filled-ellipse-on-a-windows-form.md)