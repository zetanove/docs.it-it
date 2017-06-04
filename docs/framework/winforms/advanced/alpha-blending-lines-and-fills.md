---
title: "Linee e riempimenti con fusione alfa | Microsoft Docs"
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
  - "sfumatura alfa"
  - "sfumatura alfa, utilizzo con riempimenti"
  - "sfumatura alfa, utilizzo con righe"
  - "esempi [Windows Form], sfumatura alfa"
  - "riempimenti, sfumatura alfa"
  - "linee, aggiunta di trasparenze"
  - "linee, sfumatura alfa"
  - "forme, aggiunta di trasparenze"
ms.assetid: 5440f48c-3ac9-44c3-b170-c1c110bdbab8
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Linee e riempimenti con fusione alfa
In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] un colore corrisponde a un valore a 32 bit con 8 bit ciascuno per alfa, rosso, verde e blu.  Il valore alfa indica la trasparenza del colore, ovvero la misura in cui il colore è sfumato rispetto al colore di sfondo.  L'intervallo dei valori alfa è compreso tra 0 e 255, dove 0 rappresenta un colore completamente trasparente e 255 rappresenta un colore completamente opaco.  
  
 La fusione alfa è una sfumatura pixel per pixel dei dati relativi ai colori di sfondo e di origine.  Ciascuna delle componenti rosso, verde e blu di un dato colore di origine viene sfumata con la componente corrispondente del colore di sfondo, in base alla seguente formula:  
  
 Colore\_di\_visualizzazione \= Colore\_di\_origine x alfa \/ 255 \+ Colore\_di\_sfondo x \(255 \- alfa\) \/ 255  
  
 Si supponga, ad esempio, che la componente rosso del colore di origine sia 150 e quella del colore di sfondo sia 100.  Se il valore alfa è 200, la componente rosso del colore risultante viene calcolata come segue:  
  
 150 × 200 \/ 255 \+ 100 × \(255 – 200\) \/ 255 \= 139  
  
## In questa sezione  
 [Procedura: disegnare linee opache e semitrasparenti](../../../../docs/framework/winforms/advanced/how-to-draw-opaque-and-semitransparent-lines.md)  
 Mostra come disegnare linee con fusione alfa.  
  
 [Procedura: disegnare con pennelli opachi e semitrasparenti](../../../../docs/framework/winforms/advanced/how-to-draw-with-opaque-and-semitransparent-brushes.md)  
 Illustra come applicare la fusione alfa tramite pennelli.  
  
 [Procedura: utilizzare la modalità di composizione per controllare la fusione alfa](../../../../docs/framework/winforms/advanced/how-to-use-compositing-mode-to-control-alpha-blending.md)  
 Descrive come controllare la fusione alfa utilizzando <xref:System.Drawing.Drawing2D.CompositingMode>.  
  
 [Procedura: utilizzare una matrice di colori per impostare i valori alfa nelle immagini](../../../../docs/framework/winforms/advanced/how-to-use-a-color-matrix-to-set-alpha-values-in-images.md)  
 Illustra come utilizzare un oggetto <xref:System.Drawing.Imaging.ColorMatrix> per controllare la fusione alfa.