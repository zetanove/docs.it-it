---
title: "Procedura: unire linee | Microsoft Docs"
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
  - "stile di un'unione di linee in rilievo"
  - "disegno, unione di linee"
  - "grafica, unione di linee"
  - "GraphicsPath (oggetto)"
  - "join di linee"
  - "linee, join"
  - "stile di un'unione di linee decorato"
  - "Pen (classe)"
  - "stile di un'unione di linee arrotondato"
ms.assetid: 9fc480c2-3c75-4fd1-8ab5-296a99e820e2
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: unire linee
Un'unione di linee è l'area comune formata da due linee le cui estremità si incontrano e si sovrappongono.  In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] sono disponibili tre stili di unione di linee: decorato, in rilievo e arrotondato.  Lo stile dell'unione di linee è una proprietà della classe <xref:System.Drawing.Pen>.  Quando si specifica lo stile di un'unione di linee per un oggetto <xref:System.Drawing.Pen>, tale stile sarà applicato a tutte le linee collegate in qualsiasi oggetto <xref:System.Drawing.Drawing2D.GraphicsPath> tracciato utilizzando quella penna.  
  
 Nell'immagine seguente è visualizzato il risultato l'unione di linee in rilievo.  
  
 ![Oggetti Pen](../../../../docs/framework/winforms/advanced/media/pens5.png "pens5")  
  
## Esempio  
 È possibile specificare lo stile dell'unione di linee utilizzando la proprietà <xref:System.Drawing.Pen.LineJoin%2A> della classe <xref:System.Drawing.Pen>.  Nell'esempio che segue è illustrata un'unione di linee in rilievo tra una linea orizzontale e una verticale.  Nel codice che segue, il valore <xref:System.Drawing.Drawing2D.LineJoin> assegnato alla proprietà <xref:System.Drawing.Pen.LineJoin%2A> è un membro dell'enumerazione <xref:System.Drawing.Drawing2D.LineJoin>.  Gli altri membri dell'enumerazione <xref:System.Drawing.Drawing2D.LineJoin> sono <xref:System.Drawing.Drawing2D.LineJoin> e <xref:System.Drawing.Drawing2D.LineJoin>.  
  
 [!code-csharp[System.Drawing.UsingAPen#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.UsingAPen#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#31)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 [Utilizzo di un oggetto Pen per creare linee e forme](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)