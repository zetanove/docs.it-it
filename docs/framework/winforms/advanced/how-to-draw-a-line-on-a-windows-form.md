---
title: "Procedura: disegnare una linea in un Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Graphics.DrawLine"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "disegno di linee"
  - "disegno, linee"
  - "esempi [Windows Form], disegno di righe nei form"
  - "linee, disegno"
ms.assetid: 55c1dbeb-75d0-430c-9814-a24b8971ad8c
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: disegnare una linea in un Windows Form
Nell'esempio riportato di seguito viene creata una linea in un form.  In genere, quando si disegna in un form, si gestisce l'evento <xref:System.Windows.Forms.Control.Paint> del form e si esegue il disegno utilizzando la proprietà <xref:System.Windows.Forms.PaintEventArgs.Graphics%2A> di <xref:System.Windows.Forms.PaintEventArgs>, come illustrato nell'esempio seguente.  
  
## Esempio  
 [!code-csharp[System.Drawing.UsingAPen#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.UsingAPen#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#11)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Programmazione efficiente  
 È sempre necessario chiamare il metodo <xref:System.IDisposable.Dispose%2A> sugli oggetti che richiedono un notevole utilizzo delle risorse di sistema, quali gli oggetti <xref:System.Drawing.Pen>.  
  
## Vedere anche  
 <xref:System.Drawing.Graphics.DrawLine%2A>   
 <xref:System.Windows.Forms.Control.OnPaint%2A>   
 [Guida introduttiva alla programmazione grafica](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [Utilizzo di un oggetto Pen per creare linee e forme](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)   
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)