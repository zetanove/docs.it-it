---
title: "Procedura: creare testo con GDI | Microsoft Docs"
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
  - "disegno, testo"
  - "GDI, creazione di testo [Windows Form]"
  - "testo, disegno con TextRenderer"
  - "Windows Form, disegno di testo con GDI"
ms.assetid: 2a19fe5d-2ace-451c-94db-01cb1118ef7b
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: creare testo con GDI
Con il metodo <xref:System.Windows.Forms.TextRenderer.DrawText%2A> della classe <xref:System.Windows.Forms.TextRenderer> è possibile accedere alla funzionalità [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] per il disegno di testo in un form o in un controllo.  In genere, con il rendering del testo di [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] si ottengono prestazioni migliori e misurazione del testo più accurata di [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)].  
  
> [!NOTE]
>  I metodi <xref:System.Windows.Forms.TextRenderer.DrawText%2A> della classe <xref:System.Windows.Forms.TextRenderer> non supportati per la stampa.  Per stampare, utilizzare sempre i metodi <xref:System.Drawing.Graphics.DrawString%2A> della classe <xref:System.Drawing.Graphics>.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come disegnare testo su più righe all'interno di un rettangolo utilizzando il metodo <xref:System.Windows.Forms.TextRenderer.DrawText%2A>.  
  
 [!code-csharp[System.Windows.Forms.TextRendererExamples#7](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.TextRendererExamples/CS/Form1.cs#7)]
 [!code-vb[System.Windows.Forms.TextRendererExamples#7](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.TextRendererExamples/VB/Form1.vb#7)]  
  
 Per eseguire il rendering del testo con la classe <xref:System.Windows.Forms.TextRenderer>, è necessaria un'interfaccia <xref:System.Drawing.IDeviceContext>, ad esempio una classe <xref:System.Drawing.Graphics> e una classe <xref:System.Drawing.Font>, una posizione per disegnare il testo e il colore in cui deve essere disegnato.  Facoltativamente è possibile specificare la formattazione del testo utilizzando l'enumerazione <xref:System.Windows.Forms.TextFormatFlags>.  
  
 Per ulteriori informazioni sull'ottenimento di una classe <xref:System.Drawing.Graphics>, vedere [Procedura: creare oggetti Graphics per disegnare](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md).  Per ulteriori informazioni sulla costruzione di una classe <xref:System.Drawing.Font>, vedere [Procedura: creare caratteri e gruppi di caratteri](../../../../docs/framework/winforms/advanced/how-to-construct-font-families-and-fonts.md).  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs>`e`, un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.TextRenderer>   
 <xref:System.Drawing.Font>   
 <xref:System.Drawing.Color>   
 <xref:System.Drawing.Color>   
 [Utilizzo di tipi di carattere e testo](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)