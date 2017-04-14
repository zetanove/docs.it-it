---
title: "Costruzione e creazione di curve | Microsoft Docs"
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
  - "curve, disegno"
  - "disegno, curve"
  - "esempi [Windows Form], disegno delle curve"
ms.assetid: 76e92623-4130-4644-b867-faca58bdb3a2
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Costruzione e creazione di curve
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] supporta vari tipi di curve: ellissi, archi, spline di tipo Cardinal e spline di Bézier.  Un'ellisse è definita dal proprio rettangolo di delimitazione, un arco è la parte di un'ellisse definita da un angolo di partenza e da un angolo di apertura.  Una spline di tipo Cardinal è definita da una matrice di punti e da un parametro di tensione. La curva passa per ogni punto della matrice e il parametro di tensione ne influenza la curvatura.  Una spline di Bézier è definita da due punti finali e da due punti di controllo. La curva non passa per i punti di controllo, ma questi influenzano la direzione e la curvatura nel tratto in cui la curva passa da un punto finale all'altro.  
  
## In questa sezione  
 [Procedura: disegnare spline di tipo Cardinal](../../../../docs/framework/winforms/advanced/how-to-draw-cardinal-splines.md)  
 Descrive le spline di tipo Cardinal e come disegnarle.  
  
 [Procedura: disegnare una singola spline di Bézier](../../../../docs/framework/winforms/advanced/how-to-draw-a-single-bezier-spline.md)  
 Descrive una spline di Bézier e come disegnarla.  
  
 [Procedura: disegnare una sequenza di spline di Bézier](../../../../docs/framework/winforms/advanced/how-to-draw-a-sequence-of-bezier-splines.md)  
 Illustra come disegnare varie spline di Bézier in sequenza.