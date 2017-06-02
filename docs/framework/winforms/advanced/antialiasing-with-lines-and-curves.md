---
title: "Anti-aliasing con linee e curve | Microsoft Docs"
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
  - "anti-aliasing"
  - "anti-aliasing, modalità di smussamento"
  - "GDI+, anti-aliasing"
ms.assetid: 810da1a4-c136-4abf-88df-68e49efdd8d4
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Anti-aliasing con linee e curve
Per tracciare una linea tramite [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)], è necessario specificare i punti iniziale e finale della linea ma non le informazioni sui singoli pixel.  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] opera congiuntamente al software del driver video per determinare i pixel da attivare per mostrare la linea in un particolare dispositivo di visualizzazione.  
  
## Aliasing  
 Si prenda in considerazione la linea retta rossa che unisce il punto \(4, 2\) al punto \(16, 10\).  Si supponga che l'origine del sistema di coordinate si trovi nell'angolo superiore sinistro e che l'unità di misura sia il pixel.  Si supponga inoltre che l'asse x sia rivolto verso destra e l'asse y verso il basso.  Nell'immagine seguente viene mostrato un ingrandimento della linea rossa tracciata su uno sfondo multicolore.  
  
 ![Linea, senza antialiasing](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art33.png "AboutGdip02\_Art33")  
  
 Si noti che i pixel rossi utilizzati per il rendering della linea sono opachi.  Lungo la linea non sono presenti pixel parzialmente trasparenti.  Questo tipo di rendering attribuisce alla linea un aspetto irregolare: la linea assomiglia infatti quasi a una scala.  La tecnica di rappresentazione di una linea come una scala è definita aliasing: la scala è un alias della linea teorica.  
  
## Anti\-aliasing  
 Una tecnica più avanzata per il rendering di una linea implica l'utilizzo di pixel parzialmente trasparenti insieme ai pixel opachi.  Il colore dei pixel è impostato su rosso puro o su una fusione di rosso e del colore dello sfondo in base alla vicinanza dei pixel alla linea.  Questo tipo di rendering è definito antialias e consente di ottenere una linea che viene percepita come maggiormente uniforme.  Nell'immagine seguente viene mostrata la fusione di alcuni pixel con il colore dello sfondo per creare una linea di tipo antialias.  
  
 ![Antialiasing di una linea](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art34.png "AboutGdip02\_Art34")  
  
 È possibile applicare l'anti\-aliasing \(smussamento\) anche alle curve.  Nell'immagine seguente viene mostrato un ingrandimento di un'ellisse smussata.  
  
 ![Antialiasing di curve](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art35.png "AboutGdip02\_Art35")  
  
 Nell'immagine seguente viene mostrata la stessa ellisse a dimensioni effettive, senza e con anti\-aliasing.  
  
 ![Esempio di antialiasing](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art36.gif "AboutGdip02\_Art36")  
  
 Per tracciare linee e curve che utilizzano l'anti\-aliasing, creare un'istanza della classe <xref:System.Drawing.Graphics> e impostarne la proprietà <xref:System.Drawing.Graphics.SmoothingMode%2A> su <xref:System.Drawing.Drawing2D.SmoothingMode> o su <xref:System.Drawing.Drawing2D.SmoothingMode>.  Chiamare quindi uno dei metodi di disegno della stessa classe <xref:System.Drawing.Graphics>.  
  
 [!code-csharp[LinesCurvesAndShapes#81](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#81)]
 [!code-vb[LinesCurvesAndShapes#81](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#81)]  
  
## Vedere anche  
 <xref:System.Drawing.Drawing2D.SmoothingMode?displayProperty=fullName>   
 [Linee, curve e forme](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [Procedura: utilizzare l'antialiasing nel testo](../../../../docs/framework/winforms/advanced/how-to-use-antialiasing-with-text.md)