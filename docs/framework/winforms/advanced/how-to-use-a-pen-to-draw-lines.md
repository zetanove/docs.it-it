---
title: "Procedura: utilizzare un oggetto Pen per disegnare linee | Microsoft Docs"
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
  - "linee, disegno"
  - "penne, disegno di linee"
ms.assetid: 0828c331-a438-4bdd-a4d6-3ef1e59e8795
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: utilizzare un oggetto Pen per disegnare linee
Per tracciare linee, sono necessari un oggetto <xref:System.Drawing.Graphics> e un oggetto <xref:System.Drawing.Pen>.  L'oggetto <xref:System.Drawing.Graphics> fornisce il metodo <xref:System.Drawing.Graphics.DrawLine%2A>, mentre nell'oggetto <xref:System.Drawing.Pen> sono memorizzati gli attributi, quale il colore e lo spessore della linea.  
  
## Esempio  
 Nell'esempio che segue si traccia una linea tra \(20, 10\) e \(300, 100\).  Nella prima istruzione si utilizza il costruttore della classe <xref:System.Drawing.Pen.%23ctor%2A> per creare una penna di colore nero.  L'argomento passato al costruttore <xref:System.Drawing.Pen.%23ctor%2A> rappresenta un oggetto <xref:System.Drawing.Color> creato con il metodo <xref:System.Drawing.Color.FromArgb%2A>.  I valori utilizzati per creare l'oggetto <xref:System.Drawing.Color> \(255, 0, 0, 0\) corrispondono alle componenti alfa, rosso, verde e blu del colore.  Tali valori consentono di definire una penna di colore nero opaco.  
  
 [!code-csharp[System.Drawing.UsingAPen#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.UsingAPen#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#11)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 <xref:System.Drawing.Pen>   
 [Utilizzo di un oggetto Pen per creare linee e forme](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)   
 [Penne, linee e rettangoli in GDI\+](../../../../docs/framework/winforms/advanced/pens-lines-and-rectangles-in-gdi.md)