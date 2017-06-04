---
title: "Procedura: creare figure da linee, curve e forme | Microsoft Docs"
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
  - "figure, creazione da righe"
  - "figure, creazione da forme"
ms.assetid: 82fd56c7-b443-4765-9b7c-62ce030656ec
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: creare figure da linee, curve e forme
Per creare una figura, costruire un oggetto <xref:System.Drawing.Drawing2D.GraphicsPath> e quindi chiamare i metodi, ad esempio <xref:System.Drawing.Drawing2D.GraphicsPath.AddLine%2A> e <xref:System.Drawing.Drawing2D.GraphicsPath.AddCurve%2A>, per aggiungere le primitive al percorso.  
  
## Esempio  
 Negli esempi di codice riportati di seguito vengono creati percorsi contenenti figure:  
  
-   Nel primo esempio qui di seguito viene creato un percorso con una singola figura.  La figura è composta da un singolo arco.  L'arco ha un angolo di scansione di \-180 gradi, ovvero in senso antiorario nel sistema di coordinate predefinito.  
  
-   Nel secondo esempio qui di seguito si crea un percorso con due figure.  La prima figura è un arco seguito da una linea.  La seconda figura è una linea seguita da una curva seguita da una linea.  La prima figura resta aperta, la seconda è chiusa.  
  
 [!code-csharp[System.Drawing.ConstructingDrawingPaths#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.ConstructingDrawingPaths#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/VB/Class1.vb#21)]  
  
 [!code-csharp[System.Drawing.ConstructingDrawingPaths#22](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/CS/Class1.cs#22)]
 [!code-vb[System.Drawing.ConstructingDrawingPaths#22](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/VB/Class1.vb#22)]  
  
## Compilazione del codice  
 Gli esempi precedenti sono progettati per essere utilizzati con Windows Form e richiedono <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 <xref:System.Drawing.Drawing2D.GraphicsPath>   
 [Costruzione e creazione di percorsi](../../../../docs/framework/winforms/advanced/constructing-and-drawing-paths.md)   
 [Utilizzo di un oggetto Pen per creare linee e forme](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)