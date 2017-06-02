---
title: "Procedura: impostare gli stili di carattere e colore nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "griglie dei dati, stili di colore"
  - "griglie dei dati, personalizzazione di celle"
  - "griglie dei dati, stili dei tipi di carattere"
  - "DataGridView (controllo) [Windows Form], personalizzazione delle celle"
ms.assetid: 588f2c57-d963-41b1-9c1d-d02d71818113
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: impostare gli stili di carattere e colore nel controllo DataGridView di Windows Form
È possibile specificare l'aspetto delle celle all'interno di un controllo <xref:System.Windows.Forms.DataGridView> impostando le proprietà della classe <xref:System.Windows.Forms.DataGridViewCellStyle>.  È possibile recuperare istanze di questa classe da diverse proprietà della classe <xref:System.Windows.Forms.DataGridView> e delle classi correlate o, in alternativa, creare istanze di oggetti <xref:System.Windows.Forms.DataGridViewCellStyle> da assegnare a tali proprietà.  
  
 Le procedure riportate di seguito illustrano la personalizzazione di base dell'aspetto delle celle mediante la proprietà <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A>.  Ogni cella del controllo eredita gli stili specificati mediante questa proprietà, a meno che non vengano sostituiti a livello di colonna, riga o cella.  Per un esempio di ereditarietà degli stili, vedere [Procedura: impostare stili di cella predefiniti per il controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md).  Per informazioni su altri usi della classe <xref:System.Windows.Forms.DataGridViewCellStyle>, vedere gli argomenti elencati nella sezione Vedere anche.  
  
 In Visual Studio è disponibile supporto completo per questa attività.  Vedere anche [Procedura: Impostare formati di dati e stili di cella predefiniti per il controllo DataGridView Windows Form usando la finestra di progettazione](http://msdn.microsoft.com/library/95y5fz2x\(v=vs.110\)).  
  
### Per specificare il carattere usato dalle celle di un DataGridView  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.Font%2A> di un oggetto <xref:System.Windows.Forms.DataGridViewCellStyle>.  Nell'esempio di codice riportato di seguito viene usata la proprietà <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName> per impostare il carattere per tutto il controllo.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#101](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#101)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#101](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#101)]  
  
### Per specificare i colori di primo piano e di sfondo delle celle di un DataGridView  
  
-   Impostare le proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A> e <xref:System.Windows.Forms.DataGridViewCellStyle.BackColor%2A> di un oggetto <xref:System.Windows.Forms.DataGridViewCellStyle>.  Nell'esempio di codice riportato di seguito viene usata la proprietà <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>e per impostare gli stili per tutto il controllo.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#102](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#102)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#102](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#102)]  
  
### Per specificare i colori di primo piano e di sfondo delle celle selezionate di un DataGridView  
  
-   Impostare le proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.SelectionForeColor%2A> e <xref:System.Windows.Forms.DataGridViewCellStyle.SelectionBackColor%2A> di un oggetto <xref:System.Windows.Forms.DataGridViewCellStyle>.  Nell'esempio di codice riportato di seguito viene usata la proprietà <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>e per impostare gli stili per tutto il controllo.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#103](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#103)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#103](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#103)]  
  
## Esempio  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#100](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#100)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#100](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#100)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato `dataGridView1`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName>, <xref:System.Drawing?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Programmazione efficiente  
 Per la massima scalabilità, è opportuno condividere gli oggetti <xref:System.Windows.Forms.DataGridViewCellStyle> su più righe, colonne o celle che usano lo stesso stile anziché impostare separatamente le proprietà di stile per ogni elemento.  Per altre informazioni, vedere [Procedure consigliate per ridimensionare il controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewCellStyle>   
 [Formattazione e stile di base nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)   
 [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)