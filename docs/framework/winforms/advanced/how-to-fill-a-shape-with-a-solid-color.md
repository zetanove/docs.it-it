---
title: "Procedura: riempire una forma con un colore a tinta unita | Microsoft Docs"
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
  - "colori, aggiunta alle forme"
  - "forme, riempimento"
ms.assetid: 06088b31-bac9-4ef3-9ebe-06c2c764d6df
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: riempire una forma con un colore a tinta unita
Per riempire una forma con un colore a tinta unita, creare un oggetto <xref:System.Drawing.SolidBrush>, quindi passarlo come argomento a uno dei metodi di riempimento della classe <xref:System.Drawing.Graphics>.  Nell'esempio che segue è illustrato come riempire un'ellisse con il colore rosso.  
  
## Esempio  
 Nel codice che segue, il costruttore <xref:System.Drawing.SolidBrush.%23ctor%2A> accetta un oggetto <xref:System.Drawing.Color> che viene considerato come unico argomento.  I valori utilizzati dal metodo <xref:System.Drawing.Color.FromArgb%2A> rappresentano le componenti alfa, rosso, verde e blu del colore.  Ciascun valore deve essere compreso tra 0 e 255.  Il primo valore pari a 255 indica che il colore è completamente opaco, il secondo che il componente rosso è a intensità piena.  Due valori pari a zero indicano che le componenti verde e blu hanno entrambe intensità pari a 0.  
  
 I quattro numeri \(0, 0, 100, 60\) passati al metodo <xref:System.Drawing.Graphics.FillEllipse%2A> specificano la posizione e la dimensione del rettangolo di delimitazione dell'ellisse.  L'angolo superiore sinistro del rettangolo è \(0, 0\), la larghezza è pari a 100 pixel e l'altezza a 60.  
  
 [!code-csharp[System.Drawing.UsingABrush#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.UsingABrush#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#11)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 [Utilizzo di un oggetto Brush per il riempimento di forme](../../../../docs/framework/winforms/advanced/using-a-brush-to-fill-shapes.md)