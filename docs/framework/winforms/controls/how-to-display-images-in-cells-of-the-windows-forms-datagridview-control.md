---
title: "Procedura: visualizzare immagini in celle del controllo DataGridView di Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "celle, visualizzazione di immagini"
  - "griglie dei dati, visualizzazione di immagini in celle"
  - "griglie dei dati, visualizzazione in griglie"
  - "DataGridView (controllo) [Windows Form], visualizzazione di immagini"
ms.assetid: 53b13d31-1b56-476d-9ab4-18bfac138a22
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: visualizzare immagini in celle del controllo DataGridView di Windows Form
In una riga di dati è possibile visualizzare un'immagine o un elemento grafico.  Spesso si tratta della fotografia di un dipendente o di un logo aziendale.  
  
 L'inserimento delle immagini è semplice se i dati sono visualizzati in un controllo <xref:System.Windows.Forms.DataGridView>,  in quanto tale controllo gestisce a livello nativo qualsiasi formato di immagine supportato dalla classe <xref:System.Drawing.Image> nonché il formato OLE utilizzato da alcuni database.  
  
 Se l'origine dati del controllo <xref:System.Windows.Forms.DataGridView> presenta una colonna di tipo image, le immagini verranno visualizzate automaticamente dal controllo <xref:System.Windows.Forms.DataGridView>.  
  
 L'esempio di codice riportato di seguito illustra come estrarre un'icona da una risorsa incorporata e convertirla in una bitmap da visualizzare in ogni cella di una colonna di tipo image.  Per un altro esempio in cui i valori di testo delle celle vengono convertiti in immagini, vedere [Procedura: formattare dati personalizzati in un controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md).  
  
## Esempio  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#050](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#050)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#050](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#050)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato`dataGridView1`.  
  
-   Una risorsa con icona incorporata denominata `tree.ico`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName>, <xref:System.Windows.Forms?displayProperty=fullName> e <xref:System.Drawing?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 [Funzionalità di base per colonna, riga e cella nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/basic-column-row-and-cell-features-wf-datagridview-control.md)   
 [Procedura: formattare dati personalizzati in un controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)