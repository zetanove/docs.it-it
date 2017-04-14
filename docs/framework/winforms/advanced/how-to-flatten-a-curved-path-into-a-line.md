---
title: "Procedura: trasformare un percorso curvo in una linea | Microsoft Docs"
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
  - "curve, appiattimento"
  - "disegno, appiattimento di curve"
  - "Flatten (metodo)"
  - "grafica, appiattimento di curve in linee"
  - "GraphicsPath (oggetto)"
  - "percorsi, appiattimento"
ms.assetid: e654b8de-25f4-4735-9208-42e4514a589c
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: trasformare un percorso curvo in una linea
In un oggetto <xref:System.Drawing.Drawing2D.GraphicsPath> viene memorizzata una sequenza di linee e di spline Bézier.  È possibile aggiungere diversi tipi di curve \(ellissi, archi, spline di tipo Cardinal\) a un percorso, ma ogni curva verrà convertita in spline Bézier prima della memorizzazione nel percorso.  La linearizzazione di un percorso consiste nella conversione di ogni spline Bézier presente nel percorso in una sequenza di linee rette.  Nell'immagine seguente viene mostrato un percorso prima e dopo la linearizzazione.  
  
 ![Curve e linee rette](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art32a.png "AboutGdip02\_Art32A")  
  
### Per appiattire un percorso  
  
-   Chiamare il metodo <xref:System.Drawing.Drawing2D.GraphicsPath.Flatten%2A> dell'oggetto <xref:System.Drawing.Drawing2D.GraphicsPath>:  Il metodo <xref:System.Drawing.Drawing2D.GraphicsPath.Flatten%2A> riceve un argomento di appiattimento che consente di specificare la distanza massima tra il percorso appiattito e il percorso originale.  
  
## Vedere anche  
 <xref:System.Drawing.Drawing2D.GraphicsPath?displayProperty=fullName>   
 [Linee, curve e forme](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [Costruzione e creazione di percorsi](../../../../docs/framework/winforms/advanced/constructing-and-drawing-paths.md)