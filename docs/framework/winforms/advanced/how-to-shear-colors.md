---
title: "Procedura: variare le componenti cromatiche | Microsoft Docs"
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
  - "colori, taglio"
  - "colori, trasformazione con matrici di colore"
ms.assetid: 0a424171-5b8b-45c4-afef-e9720a6c3e22
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: variare le componenti cromatiche
Questa operazione consiste nell'aumentare o diminuire una componente cromatica in modo proporzionale a un'altra.  Si consideri ad esempio una trasformazione in cui la componente rossa viene aumentata della metà del valore di quella blu.  Applicando tale trasformazione il colore \(0,2, 0,5, 1\) diventa \(0,7, 0,5, 1\).  La nuova componente rossa è 0,2 \+ \(1\/2\)\(1\) \= 0,7.  
  
## Esempio  
 Nell'esempio riportato di seguito viene costruito un oggetto <xref:System.Drawing.Image> dal file ColorBars4.bmp.  La trasformazione per variazione descritta nel paragrafo precedente viene quindi applicata a ciascuno dei pixel nell'immagine.  
  
 Nell'illustrazione che segue si mostra l'immagine originale a sinistra e l'immagine tagliata a destra.  
  
 ![Variazione delle componenti cromatiche](../../../../docs/framework/winforms/advanced/media/colortrans6.png "colortrans6")  
  
 Nella tabella che segue sono elencati i vettori di colore per le quattro barre prima e dopo la trasformazione per variazione.  
  
|Originale|Variato|  
|---------------|-------------|  
|\(0, 0, 1, 1\)|\(0.5, 0, 1, 1\)|  
|\(0.5, 1, 0.5, 1\)|\(0.75, 1, 0.5, 1\)|  
|\(1, 1, 0, 1\)|\(1, 1, 0, 1\)|  
|\(0.4, 0.4, 0.4, 1\)|\(0.6, 0.4, 0.4, 1\)|  
  
 [!code-csharp[System.Drawing.Misc3#9](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Misc3/CS/Form1.cs#9)]
 [!code-vb[System.Drawing.Misc3#9](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Misc3/VB/Form1.vb#9)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  Sostituire `ColorBars.bmp` con il nome e il percorso di un'immagine validi nel computer in uso.  
  
## Vedere anche  
 <xref:System.Drawing.Imaging.ColorMatrix>   
 <xref:System.Drawing.Imaging.ImageAttributes>   
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [Ricolorazione di immagini](../../../../docs/framework/winforms/advanced/recoloring-images.md)