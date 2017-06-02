---
title: "Procedura: utilizzare il modello di riga personalizzare le righe nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "griglie dei dati, personalizzazione di righe"
  - "DataGridView (controllo) [Windows Form], personalizzazione di righe"
ms.assetid: 6db61607-7e57-4a84-8d63-9d6a7ed7f9ff
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: utilizzare il modello di riga personalizzare le righe nel controllo DataGridView di Windows Form
Il controllo <xref:System.Windows.Forms.DataGridView> utilizza il modello di riga come base per tutte le righe da aggiungere al controllo mediante l'associazione di dati o la chiamata del metodo <xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A?displayProperty=fullName> senza specificare una riga esistente da utilizzare.  
  
 Il modello di riga fornisce un maggiore controllo sull'aspetto e sul comportamento delle righe rispetto alla proprietà <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A>.  Utilizzando il modello di riga è possibile impostare qualsiasi proprietà <xref:System.Windows.Forms.DataGridViewRow>, tra cui <xref:System.Windows.Forms.DataGridViewRow.DefaultCellStyle%2A>.  
  
 In alcuni casi è necessario utilizzare il modello di riga per ottenere un effetto particolare.  Ad esempio, non è possibile memorizzare informazioni relative all'altezza della riga in un controllo <xref:System.Windows.Forms.DataGridViewCellStyle>, quindi è necessario utilizzare un modello di riga per modificare l'altezza predefinita per tutte le righe.  Il modello di riga è utile anche quando si creano le proprie classi derivandole da <xref:System.Windows.Forms.DataGridViewRow> e si desidera utilizzare un tipo personalizzato per l'aggiunta di nuove righe al controllo.  
  
> [!NOTE]
>  Il modello di riga viene utilizzato solo per le righe aggiunte.  Non è quindi possibile modificare righe esistenti modificando il modello di riga.  
  
### Per utilizzare il modello di riga  
  
-   Impostare le proprietà nell'oggetto recuperato dalla proprietà <xref:System.Windows.Forms.DataGridView.RowTemplate%2A?displayProperty=fullName>.  
  
     [!code-cpp[System.Windows.Forms.DataGridView.RowTemplate#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.RowTemplate/CPP/datagridviewrowtemplate.cpp#1)]
     [!code-csharp[System.Windows.Forms.DataGridView.RowTemplate#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.RowTemplate/CS/datagridviewrowtemplate.cs#1)]
     [!code-vb[System.Windows.Forms.DataGridView.RowTemplate#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.RowTemplate/VB/datagridviewrowtemplate.vb#1)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato`dataGridView1`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName>, <xref:System.Drawing?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewCellStyle>   
 <xref:System.Windows.Forms.DataGridViewRow>   
 <xref:System.Windows.Forms.DataGridView.RowTemplate%2A?displayProperty=fullName>   
 [Formattazione e stile di base nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)   
 [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)