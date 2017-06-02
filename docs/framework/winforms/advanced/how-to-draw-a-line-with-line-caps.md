---
title: "Procedura: disegnare una linea con estremit&#224; | Microsoft Docs"
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
  - "disegno di linee, estremità di linea"
  - "disegno, linee"
  - "linee, disegno"
  - "penne, disegno di linee"
ms.assetid: eb68c3e1-c400-4886-8a04-76978a429cb6
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: disegnare una linea con estremit&#224;
È possibile applicare all'inizio o alla fine di una linea una delle diverse forme dette estremità di linea.  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] supporta numerose estremità di linee, quali rotonda, quadrata, a rombo e a punta di freccia.  
  
## Esempio  
 È possibile specificare le estremità di linea per l'inizio della linea, detta estremità iniziale, per la fine della linea, detta estremità finale, oppure i trattini di una linea tratteggiata, dette estremità tratteggiate.  
  
 Nell'esempio che segue si traccia una linea con una punta di freccia a un'estremità e un'estremità rotonda all'altra.  Nell'illustrazione che segue è visibile la linea risultante:  
  
 ![Oggetti Pen](../../../../docs/framework/winforms/advanced/media/pens4.png "pens4")  
  
 [!code-csharp[System.Drawing.UsingAPen#71](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#71)]
 [!code-vb[System.Drawing.UsingAPen#71](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#71)]  
  
## Compilazione del codice  
  
-   Creare un Windows Form e gestire l'evento <xref:System.Windows.Forms.Control.Paint> del form.  Incollare il codice precedente nel gestore eventi <xref:System.Windows.Forms.Control.Paint> passando `e` come <xref:System.Windows.Forms.PaintEventArgs>.  
  
## Vedere anche  
 <xref:System.Drawing.Pen?displayProperty=fullName>   
 <xref:System.Drawing.Drawing2D.LineCap?displayProperty=fullName>   
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [Utilizzo di un oggetto Pen per creare linee e forme](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)