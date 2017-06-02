---
title: "Procedura: disegnare con pennelli opachi e semitrasparenti | Microsoft Docs"
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
  - "sfumatura alfa, pennello"
  - "pennelli, utilizzo semi-trasparente"
  - "forme semitrasparenti, disegno"
  - "trasparenza, forme semitrasparenti"
ms.assetid: a4f6f6b8-3bc8-440a-84af-d62ef0f8ff40
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: disegnare con pennelli opachi e semitrasparenti
Quando si riempie una forma, è necessario passare un oggetto <xref:System.Drawing.Brush> a uno dei metodi di riempimento della classe <xref:System.Drawing.Graphics>.  L'unico parametro del costruttore <xref:System.Drawing.SolidBrush.%23ctor%2A> è un oggetto <xref:System.Drawing.Color>.  Per riempire una forma opaca, impostare il componente alfa del colore su 255.  Per riempire una forma semitrasparente, impostare il componente alfa su un valore qualsiasi compreso tra 1 e 254.  
  
 Quando si riempie una forma semitrasparente, il colore della forma viene sfumato con i colori dello sfondo.  Il componente alfa specifica come si combinano i colori della forma e dello sfondo. I valori alfa vicini a 0 rendono più intensi i colori di sfondo, mentre i valori alfa più vicini a 255 rendono più intenso il colore della forma.  
  
## Esempio  
 L'esempio seguente disegna una bitmap e quindi riempie tre ellissi che si sovrappongono alla bitmap.  Per la prima ellisse si usa un componente alfa con un valore pari a 255, quindi l'ellisse risulta opaca.  Per la seconda e la terza ellisse si usa un componente alfa con un valore pari a 128, quindi le ellissi risultano semitrasparenti. L'immagine di sfondo è visibile attraverso le ellissi.  La chiamata che imposta la proprietà <xref:System.Drawing.Graphics.CompositingQuality%2A> determina la sfumatura della terza ellissi ottenuta in combinazione con la correzione gamma.  
  
 L'immagine seguente illustra l'output del codice riportato di seguito.  
  
 ![Opaco e semitrasparente](../../../../docs/framework/winforms/advanced/media/compqualellipse.png "compqualellipse")  
  
 [!code-csharp[System.Drawing.AlphaBlending#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.AlphaBlending#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#31)]  
  
## Compilazione del codice  
 L'esempio precedente è progettato per l'uso con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## Vedere anche  
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [Linee e riempimenti con fusione alfa](../../../../docs/framework/winforms/advanced/alpha-blending-lines-and-fills.md)   
 [Procedura: assegnare uno sfondo trasparente al controllo](../../../../docs/framework/winforms/controls/how-to-give-your-control-a-transparent-background.md)   
 [Procedura: disegnare linee opache e semitrasparenti](../../../../docs/framework/winforms/advanced/how-to-draw-opaque-and-semitransparent-lines.md)