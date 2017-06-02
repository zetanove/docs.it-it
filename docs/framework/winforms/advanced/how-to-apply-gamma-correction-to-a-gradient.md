---
title: "Procedura: applicare la correzione gamma a una sfumatura | Microsoft Docs"
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
  - "pennelli per sfumature, correzione della gamma"
  - "sfumature, correzione della gamma"
ms.assetid: da4690e7-5fac-4fd2-b3f0-5cb35c165b92
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: applicare la correzione gamma a una sfumatura
È possibile attivare la correzione gamma per un pennello a sfumatura lineare impostando la proprietà <xref:System.Drawing.Drawing2D.LinearGradientBrush.GammaCorrection%2A> del pennello su `true`.  Per disabilitare la correzione gamma, impostare la proprietà <xref:System.Drawing.Drawing2D.LinearGradientBrush.GammaCorrection%2A> su `false`.  Per impostazione predefinita la correzione gamma è disabilitata.  
  
## Esempio  
 Nell'esempio che segue viene creato un pennello a sfumatura lineare, utilizzato per riempire due rettangoli.  Il primo rettangolo viene riempito senza correzione gamma, il secondo invece con correzione gamma.  
  
 Nell'illustrazione che segue sono visibili i due rettangoli riempiti.  Il rettangolo superiore, senza correzione gamma, è nero al centro.  Il rettangolo in basso, con correzione gamma, ha un'intensità maggiormente uniforme.  
  
 ![Sfumatura](../../../../docs/framework/winforms/advanced/media/gammagradient1.png "gammagradient1")  
  
 [!code-csharp[System.Drawing.UsingaGradientBrush#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.UsingaGradientBrush#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#31)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 <xref:System.Drawing.Drawing2D.LinearGradientBrush>   
 [Utilizzo di un pennello a sfumatura per il riempimento di forme](../../../../docs/framework/winforms/advanced/using-a-gradient-brush-to-fill-shapes.md)