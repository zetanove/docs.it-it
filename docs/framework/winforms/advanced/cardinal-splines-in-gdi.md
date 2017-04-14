---
title: "Spline di tipo Cardinal in GDI+ | Microsoft Docs"
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
  - "spline cardinali"
  - "GDI+, spline cardinali"
  - "spline, cardinali"
ms.assetid: 09b3797a-6294-422d-9adf-a5a0a7695c0c
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Spline di tipo Cardinal in GDI+
Una spline di tipo Cardinal è costituita da una sequenza di curve individuali unite per creare una curva più ampia.  La spline viene specificata da una matrice di punti e da un parametro di tensione.  Una spline di tipo Cardinal attraversa in modo uniforme tutti i punti della matrice. Nella curva non sono presenti angoli netti o modifiche nette nella tensione della curva.  Nell'immagine seguente vengono mostrati un insieme di punti e una spline di tipo Cardinal che passa attraverso ogni punto dell'insieme.  
  
 ![Spline di tipo Cardinal](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art09.png "Aboutgdip02\_art09")  
  
## Spline fisiche e matematiche  
 La spline fisica è una stecca sottile di legno o di altro materiale flessibile.  Prima dell'introduzione delle spline matematiche, le spline fisiche venivano utilizzate per tracciare curve.  La spline veniva appoggiata su un pezzo di carta e ancorata a un dato insieme di punti.  Facendo scorrere la matita o la penna lungo la spline era quindi possibile tracciare una curva.  Un dato insieme di punti poteva dare origine a svariati tipi di curve, a seconda delle proprietà della spline fisica.  Una spline molto rigida ad esempio consentiva di produrre una curva diversa da quella creata con una spline estremamente flessibile.  
  
 Le formule per le spline matematiche sono basate sulle proprietà delle canne flessibili, quindi le curve prodotte da spline matematiche sono simili alle curve prodotte con le spline fisiche.  Così come le spline fisiche di diversa tensione consentivano di produrre diverse curve attraverso un dato insieme di punti, le spline matematiche con diversi valori per il parametro di tensione produrranno curve diverse che attraversano l'insieme di punti dato.  Nell'immagine seguente vengono mostrate quattro spline di tipo Cardinal che attraversano lo stesso insieme di punti.  Viene mostrata la tensione relativa a ogni spline.  Si noti che il valore di tensione 0 corrisponde a una tensione fisica infinita, che fa in modo che la curva scelga il percorso più breve \(linee rette\) tra i punti.  Un valore di tensione pari a 1 corrisponde a tensione fisica nulla e consente alla spline di adottare il percorso associato alla minima curvatura totale.  Se si impostano valori di tensione superiori a 1, la curva si comporta come una molla compressa, costretta ad adottare un percorso più lungo.  
  
 ![Spline di tipo Cardinal](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art10.png "Aboutgdip02\_art10")  
  
 Si noti che le quattro spline mostrate nell'immagine precedente condividono la stessa tangente nel punto iniziale.  La tangente è la linea che unisce il punto iniziale e il punto successivo lungo la curva.  Analogamente, la tangente condivisa al punto finale corrisponde alla linea che unisce il punto finale e il punto precedente lungo la curva.  
  
 Per creare una spline di tipo Cardinal, sono necessari un'istanza della classe <xref:System.Drawing.Graphics>, un <xref:System.Drawing.Pen> e una matrice di oggetti <xref:System.Drawing.Point>. L'istanza della classe <xref:System.Drawing.Graphics> fornisce il metodo <xref:System.Drawing.Graphics.DrawCurve%2A> che traccia la spline, mentre nell'oggetto <xref:System.Drawing.Pen> vengono memorizzati gli attributi della spline, ad esempio lo spessore e il colore della linea.  Nella matrice di oggetti <xref:System.Drawing.Point> vengono memorizzati i punti che verranno attraversati dalla curva.  Nell'esempio di codice che segue viene illustrato come creare una spline di tipo Cardinal che attraversa i punti contenuti in  `myPointArray`.  Il terzo parametro è la tensione.  
  
 [!code-csharp[LinesCurvesAndShapes#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#31)]
 [!code-vb[LinesCurvesAndShapes#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#31)]  
  
## Vedere anche  
 [Linee, curve e forme](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [Costruzione e creazione di curve](../../../../docs/framework/winforms/advanced/constructing-and-drawing-curves.md)