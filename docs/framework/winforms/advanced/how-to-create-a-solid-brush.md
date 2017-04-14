---
title: "Procedura: creare un oggetto Solid Brush | Microsoft Docs"
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
  - "pennelli, creazione di colore uniforme"
  - "pennelli, esempi"
  - "pennelli di colore uniforme"
ms.assetid: 85c3fe7d-fb1d-4591-8a9f-d75b556b90af
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: creare un oggetto Solid Brush
Nell'esempio riportato di seguito viene creato un oggetto <xref:System.Drawing.SolidBrush>, che può essere utilizzato da un oggetto <xref:System.Drawing.Graphics> per riempire forme.  
  
## Esempio  
 [!code-cpp[System.Drawing.ConceptualHowTos#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#1)]
 [!code-csharp[System.Drawing.ConceptualHowTos#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#1)]
 [!code-vb[System.Drawing.ConceptualHowTos#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#1)]  
  
## Programmazione efficiente  
 Al termine dell'utilizzo è necessario chiamare il metodo <xref:System.IDisposable.Dispose%2A> sugli oggetti che utilizzano le risorse di sistema, come gli oggetti Brush.  
  
## Vedere anche  
 <xref:System.Drawing.SolidBrush>   
 <xref:System.Drawing.Brush>   
 [Guida introduttiva alla programmazione grafica](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [Pennelli e forme con riempimento in GDI\+](../../../../docs/framework/winforms/advanced/brushes-and-filled-shapes-in-gdi.md)   
 [Utilizzo di un oggetto Brush per il riempimento di forme](../../../../docs/framework/winforms/advanced/using-a-brush-to-fill-shapes.md)