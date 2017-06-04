---
title: "Procedura: impostare il colore di un oggetto Pen | Microsoft Docs"
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
  - "penne colorate"
  - "penne, impostazione del colore"
ms.assetid: a9df06f9-a6d5-4d9b-a2d1-583943540775
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: impostare il colore di un oggetto Pen
Nell'esempio qui di seguito viene modificato il colore di un oggetto <xref:System.Drawing.Pen> esistente.  
  
## Esempio  
 [!code-cpp[System.Drawing.ConceptualHowTos#9](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#9)]
 [!code-csharp[System.Drawing.ConceptualHowTos#9](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#9)]
 [!code-vb[System.Drawing.ConceptualHowTos#9](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#9)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un oggetto <xref:System.Drawing.Pen> denominato  `myPen`.  
  
## Programmazione efficiente  
 È sempre necessario chiamare il metodo <xref:System.Drawing.Pen.Dispose%2A> sugli oggetti che richiedono un notevole impiego delle risorse di sistema, quali gli oggetti <xref:System.Drawing.Pen>, al termine del loro utilizzo.  
  
## Vedere anche  
 <xref:System.Drawing.Pen>   
 [Guida introduttiva alla programmazione grafica](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [Procedura: creare un oggetto Pen](../../../../docs/framework/winforms/advanced/how-to-create-a-pen.md)   
 [Utilizzo di un oggetto Pen per creare linee e forme](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)   
 [Penne, linee e rettangoli in GDI\+](../../../../docs/framework/winforms/advanced/pens-lines-and-rectangles-in-gdi.md)