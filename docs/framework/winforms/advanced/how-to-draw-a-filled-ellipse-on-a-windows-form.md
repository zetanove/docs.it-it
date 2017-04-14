---
title: "Procedura: disegnare un&#39;ellisse con riempimento in un Windows Form | Microsoft Docs"
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
  - "Graphics.FillEllipse"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "cerchi, disegno"
  - "forme circolari"
  - "disegno, ellissi"
  - "ellissi, disegno"
  - "form, disegno di ellissi"
  - "forme, disegno"
ms.assetid: 781db806-950d-4c5b-b022-493f7fd0c4a8
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: disegnare un&#39;ellisse con riempimento in un Windows Form
Nell'esempio riportato di seguito viene creata un'ellisse piena in un form.  
  
## Esempio  
 [!code-cpp[System.Drawing.ConceptualHowTos#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#1)]
 [!code-csharp[System.Drawing.ConceptualHowTos#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#1)]
 [!code-vb[System.Drawing.ConceptualHowTos#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#1)]  
  
## Compilazione del codice  
 Non è possibile chiamare questo metodo nel gestore eventi <xref:System.Windows.Forms.Form.Load>.  Se il form viene ridimensionato o nascosto da un altro form, il contenuto creato non verrà ricreato.  Per ridisegnare automaticamente il contenuto è necessario eseguire l'override del metodo <xref:System.Windows.Forms.Control.OnPaint%2A>.  
  
## Programmazione efficiente  
 È sempre necessario chiamare il metodo <xref:System.IDisposable.Dispose%2A> sugli oggetti che richiedono un notevole utilizzo delle risorse di sistema, quali gli oggetti <xref:System.Drawing.Brush> e <xref:System.Drawing.Graphics>.  
  
## Vedere anche  
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [Guida introduttiva alla programmazione grafica](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [Linee e riempimenti con fusione alfa](../../../../docs/framework/winforms/advanced/alpha-blending-lines-and-fills.md)   
 [Utilizzo di un oggetto Brush per il riempimento di forme](../../../../docs/framework/winforms/advanced/using-a-brush-to-fill-shapes.md)