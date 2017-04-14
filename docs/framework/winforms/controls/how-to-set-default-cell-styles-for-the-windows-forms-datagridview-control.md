---
title: "Procedura: impostare stili di cella predefiniti per il controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "celle, stili"
  - "griglie dei dati, stili della cella"
  - "DataGridView (controllo) [Windows Form], stili della cella"
ms.assetid: 1aaaca43-5340-447e-99c0-9177d9776aa1
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: impostare stili di cella predefiniti per il controllo DataGridView di Windows Form
Con il controllo <xref:System.Windows.Forms.DataGridView> è possibile specificare gli stili di cella predefiniti per l'intero controllo e per specifiche colonne e righe.  Queste impostazioni predefinite filtrano dal livello di controllo al livello di colonna, quindi al livello di riga e infine di cella.  Se una particolare proprietà <xref:System.Windows.Forms.DataGridViewCellStyle> non è impostata a livello di cella, viene usata l'impostazione predefinita della proprietà a livello di riga.  Se la proprietà non è impostata neanche a livello di riga, viene usata l'impostazione predefinita della colonna.  Infine, se la proprietà non è impostata neanche a livello di colonna, viene usata l'impostazione predefinita <xref:System.Windows.Forms.DataGridView>.  Con questa impostazione è possibile evitare di duplicare le impostazioni della proprietà a più livelli.  A ogni livello è sufficiente specificare gli stili che differiscono dai livelli superiori.  Per altre informazioni, vedere [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md).  
  
 In Visual Studio è disponibile supporto completo per questa attività.  Vedere anche [Procedura: Impostare formati di dati e stili di cella predefiniti per il controllo DataGridView Windows Form usando la finestra di progettazione](http://msdn.microsoft.com/library/95y5fz2x\(v=vs.110\)).  
  
### Per impostare gli stili della cella predefiniti a livello di codice  
  
1.  Impostare le proprietà dell'oggetto <xref:System.Windows.Forms.DataGridViewCellStyle> recuperato tramite la proprietà <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#141](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#141)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#141](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#141)]  
  
2.  Creare e inizializzare nuovi oggetti <xref:System.Windows.Forms.DataGridViewCellStyle> per l'uso da più righe e colonne.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#142](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#142)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#142](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#142)]  
  
3.  Impostare la proprietà `DefaultCellStyle` di righe e colonne specifiche.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#143](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#143)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#143](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#143)]  
  
## Esempio  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#140](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#140)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#140](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#140)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato `dataGridView1`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName>, <xref:System.Drawing?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Programmazione efficiente  
 Per ottenere la massima scalabilità quando si lavora con set di dati molto grandi, è opportuno condividere gli oggetti <xref:System.Windows.Forms.DataGridViewCellStyle> su più righe, colonne o celle che usano lo stesso stile anziché impostare separatamente le proprietà di stile per i singoli elementi.  È anche necessario creare righe condivise e accedervi mediante la proprietà <xref:System.Windows.Forms.DataGridViewRowCollection.SharedRow%2A?displayProperty=fullName>.  Per altre informazioni, vedere [Procedure consigliate per ridimensionare il controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewCellStyle>   
 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewBand.DefaultCellStyle%2A?displayProperty=fullName>   
 [Formattazione e stile di base nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)   
 [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)   
 [Procedure consigliate per ridimensionare il controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md)   
 [Procedura: impostare stili di righe alterne per il controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-alternating-row-styles-for-the-windows-forms-datagridview-control.md)