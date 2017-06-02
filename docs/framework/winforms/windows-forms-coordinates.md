---
title: "Windows Forms Coordinates | Microsoft Docs"
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
  - "Windows Forms coordinates"
  - "screen coordinates"
  - "client coordinates"
  - "coordinates, Windows Forms"
ms.assetid: cc06e61f-43b6-4408-a676-2542dcfcd96e
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Windows Forms Coordinates
Il sistema di coordinate per un Windows Form è basato sulle coordinate dei dispositivi. L'unità di misura di base quando si disegna in Windows Form è quella del dispositivo, in genere il pixel.  I punti sullo schermo sono descritti da coppie di coordinate x e y, con le coordinate x che aumentano verso destra e le coordinate y che aumentano dall'alto verso il basso.  La posizione dell'origine, rispetto allo schermo, varia in base al fatto che siano specificate coordinate dello schermo o del client.  
  
## Coordinate dello schermo  
 Un'applicazione Windows Form specifica la posizione di una finestra sullo schermo tramite coordinate dello schermo.  Per tali coordinate, l'origine corrisponde all'angolo in alto a sinistra dello schermo.  La posizione completa di una finestra è spesso descritta da una struttura <xref:System.Drawing.Rectangle> che include le coordinate dello schermo di due punti che definiscono gli angoli in alto a sinistra e in basso a destra della finestra.  
  
## Coordinate del client  
 Un'applicazione Windows Form specifica la posizione dei punti in un form o controllo tramite le coordinate del client.  L'origine delle coordinate del client è l'angolo in alto a sinistra dell'area client del controllo o form.  Le coordinate del client assicurano che un'applicazione possa utilizzare valori delle coordinate coerenti nella creazione di un form o controllo, indipendentemente dalla posizione di quest'ultimo sullo schermo.  
  
 Le dimensioni dell'area client sono anch'esse descritte da una struttura <xref:System.Drawing.Rectangle> che include le coordinate del client per l'area.  In tutti i casi, la coordinata in alto a sinistra del rettangolo è inclusa nell'area client, mentre la coordinata in basso a destra è esclusa.  Le operazioni grafiche non includono i margini destro e inferiore e di un'area client.  Ad esempio il metodo <xref:System.Drawing.Graphics.FillRectangle%2A> determinerà il riempimento del margine destro e inferiore del rettangolo specificato, ma non includerà tali margini.  
  
## Mapping tra tipi diversi di coordinate  
 Occasionalmente potrebbe essere necessario eseguire il mapping dalle coordinate dello schermo alle coordinate del client.  Tale operazione può essere eseguita facilmente utilizzando i metodi <xref:System.Windows.Forms.Control.PointToClient%2A> e <xref:System.Windows.Forms.Control.PointToScreen%2A> disponibili nella classe <xref:System.Windows.Forms.Control>.  Ad esempio, la proprietà <xref:System.Windows.Forms.Control.MousePosition%2A> di <xref:System.Windows.Forms.Control> è indicata tramite coordinate dello schermo, ma potrebbe essere necessario esprimerla in coordinate del client.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Control.PointToClient%2A>   
 <xref:System.Windows.Forms.Control.PointToScreen%2A>