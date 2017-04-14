---
title: "Procedura: riempire figure aperte | Microsoft Docs"
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
  - "figure, riempimento"
  - "figure aperte, riempimento"
ms.assetid: 5a36b0e4-f1f4-46c0-a85a-22ae98491950
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: riempire figure aperte
È possibile riempire un percorso passando un oggetto <xref:System.Drawing.Drawing2D.GraphicsPath> al metodo <xref:System.Drawing.Graphics.FillPath%2A>.  Il metodo <xref:System.Drawing.Graphics.FillPath%2A> consente di riempire il percorso in base alla modalità di riempimento attualmente impostata per il percorso; è possibile scegliere tra modalità alternata o a chiocciola.  Se il percorso contiene figure aperte, viene riempito come se fossero chiuse.  In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] una figura viene chiusa disegnando un linea retta tra il punto finale e il punto iniziale della figura.  
  
## Esempio  
 Nell'esempio che segue viene creato un percorso che contiene una figura aperta, un arco, e una figura chiusa, un'ellisse.  Con il metodo <xref:System.Drawing.Graphics.FillPath%2A> il percorso viene riempito in base alla modalità di riempimento predefinita, ovvero <xref:System.Drawing.Drawing2D.FillMode>.  
  
 Nell'esempio che segue è illustrato l'output del codice modificato.  Si noti che il percorso viene riempito, secondo <xref:System.Drawing.Drawing2D.FillMode>, come se la figura aperta fosse chiusa da una linea retta tracciata tra il punto finale e il punto iniziale della figura.  
  
 ![Percorso di apertura file](../../../../docs/framework/winforms/advanced/media/fillopenpath.png "FillOpenPath")  
  
 [!code-csharp[System.Drawing.ConstructingDrawingPaths#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.ConstructingDrawingPaths#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/VB/Class1.vb#11)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 <xref:System.Drawing.Drawing2D.GraphicsPath>   
 [Percorsi di oggetti Graphics in GDI\+](../../../../docs/framework/winforms/advanced/graphics-paths-in-gdi.md)