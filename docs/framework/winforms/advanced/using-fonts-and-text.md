---
title: "Utilizzo di tipi di carattere e testo | Microsoft Docs"
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
  - "esempi [Windows Form], tipi di carattere e testo"
  - "tipi di carattere, utilizzo in Windows Form"
  - "GDI, creazione di testo [Windows Form]"
  - "stringhe [Windows Form], creazione in Windows Form"
  - "testo [Windows Form], creazione in Windows Form"
ms.assetid: d43640f3-da94-4df2-a29d-a9d021a1c069
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Utilizzo di tipi di carattere e testo
Sono numerose le classi offerte da [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] e [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] per il disegno di testo in Windows Form.  La classe [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] <xref:System.Drawing.Graphics> dispone di numerosi metodi <xref:System.Drawing.Graphics.DrawString%2A> che consentono di specificare varie funzionalità di un testo, quali ad esempio la posizione, il rettangolo di delimitazione, il tipo di carattere e il formato.  Inoltre, con [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] è possibile disegnare e misurare il testo mediante i metodi statici <xref:System.Windows.Forms.TextRenderer.DrawText%2A> e <xref:System.Windows.Forms.TextRenderer.MeasureText%2A> offerti dalla classe `TextRenderer`.  Anche i metodi [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] consentono di specificare la posizione, il tipo di carattere e il formato.  Per il rendering del testo, è possibile scegliere tra [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] e [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)], tuttavia [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] offre generalmente prestazioni migliori e misurazione più accurata del testo.  Le altre classi che contribuiscono al rendering del testo sono `FontFamily`, `Font`, <xref:System.Drawing.StringFormat> e `TextFormatFlags`.  
  
## In questa sezione  
 [Procedura: creare caratteri e gruppi di caratteri](../../../../docs/framework/winforms/advanced/how-to-construct-font-families-and-fonts.md)  
 Viene illustrato come creare oggetti `Font` e `FontFamily`.  
  
 [Procedura: creare testo in una posizione specificata](../../../../docs/framework/winforms/advanced/how-to-draw-text-at-a-specified-location.md)  
 Viene descritto come disegnare il testo in una determinata posizione utilizzando [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] e [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)].  
  
 [Procedura: creare testo disposto su più righe in un rettangolo](../../../../docs/framework/winforms/advanced/how-to-draw-wrapped-text-in-a-rectangle.md)  
 Viene spiegato come disegnare il testo in un rettangolo utilizzando [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] e [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)].  
  
 [Procedura: creare testo con GDI](../../../../docs/framework/winforms/advanced/how-to-draw-text-with-gdi.md)  
 Viene illustrato come utilizzare [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] per il disegno di testo.  
  
 [Procedura: allineare il testo creato](../../../../docs/framework/winforms/advanced/how-to-align-drawn-text.md)  
 Viene illustrato come formattare il testo [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] e [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)].  
  
 [Procedura: creare testo verticale](../../../../docs/framework/winforms/advanced/how-to-create-vertical-text.md)  
 Viene descritto come disegnare testo allineato verticalmente con [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)].  
  
 [Procedura: impostare punti di tabulazione nel testo disegnato](../../../../docs/framework/winforms/advanced/how-to-set-tab-stops-in-drawn-text.md)  
 Viene illustrato come disegnare testo con tabulazioni con [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)].  
  
 [Procedura: enumerare i tipi di carattere installati](../../../../docs/framework/winforms/advanced/how-to-enumerate-installed-fonts.md)  
 Viene illustrato come elencare i nomi dei tipi di carattere installati.  
  
 [Procedura: creare una raccolta di caratteri privata](../../../../docs/framework/winforms/advanced/how-to-create-a-private-font-collection.md)  
 Viene descritto come creare un oggetto <xref:System.Drawing.Text.PrivateFontCollection>.  
  
 [Procedura: recuperare i criteri di misurazione dei caratteri](../../../../docs/framework/winforms/advanced/how-to-obtain-font-metrics.md)  
 Viene illustrato come ottenere le dimensioni dei tipi di carattere, as esempio la parte ascendente e discendente delle celle.  
  
 [Procedura: utilizzare l'antialiasing nel testo](../../../../docs/framework/winforms/advanced/how-to-use-antialiasing-with-text.md)  
 Viene descritto come utilizzare l'antialias nel disegno di testo.  
  
## Riferimenti  
 <xref:System.Drawing.Font>  
 Descrive la classe e contiene i collegamenti a tutti i relativi membri.  
  
 <xref:System.Drawing.FontFamily>  
 Descrive la classe e contiene i collegamenti a tutti i relativi membri.  
  
 <xref:System.Drawing.Text.PrivateFontCollection>  
 Descrive la classe e contiene i collegamenti a tutti i relativi membri.  
  
 <xref:System.Windows.Forms.TextRenderer>  
 Descrive la classe e contiene i collegamenti a tutti i relativi membri.  
  
 <xref:System.Windows.Forms.TextFormatFlags>  
 Descrive la classe e contiene i collegamenti a tutti i relativi membri.