---
title: "Procedura: utilizzare l&#39;antialiasing nel testo | Microsoft Docs"
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
  - "anti-aliasing, utilizzo con il testo"
  - "stringhe [Windows Form], anti-aliasing durante il disegno"
  - "stringhe [Windows Form], smussamento del disegno"
  - "testo [Windows Form], anti-aliasing"
  - "testo [Windows Form], smussamento"
ms.assetid: 48fc34f3-f236-4b01-a0cb-f0752e6d22ae
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: utilizzare l&#39;antialiasing nel testo
*L'antialiasing* è un arrotondamento dei margini irregolari di grafica e testo disegnati, finalizzato a migliorarne aspetto o leggibilità.  Con le classi gestite di [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è possibile visualizzare sia testo con antialiasing di alta qualità sia testo di qualità inferiore.  Generalmente il rendering a qualità elevata richiede tempi di elaborazione maggiori di quello a bassa qualità.  Per impostare il livello di qualità del testo, impostare la proprietà <xref:System.Drawing.Graphics.TextRenderingHint%2A> di un oggetto <xref:System.Drawing.Graphics> su uno degli elementi dell'enumerazione <xref:System.Drawing.Text.TextRenderingHint>  
  
## Esempio  
 Nell'esempio che segue viene creato testo con due diverse impostazioni di qualità.  
  
 Nell'esempio che segue è illustrato l'output del codice di esempio.  
  
 ![Testo caratteri](../../../../docs/framework/winforms/advanced/media/fontstext10.png "FontsText10")  
  
 [!code-csharp[System.Drawing.FontsAndText#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.FontsAndText#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#21)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs>`e`, un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## Vedere anche  
 [Utilizzo di tipi di carattere e testo](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)