---
title: "Personalizzazione del controllo DataGridView Windows Form | Microsoft Docs"
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
  - "griglie dei dati, personalizzazione"
  - "DataGridView (controllo) [Windows Form], personalizzazione"
ms.assetid: 01ea5d4c-a736-4596-b0e9-a67a1b86e15f
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Personalizzazione del controllo DataGridView Windows Form
Il controllo `DataGridView` fornisce diverse proprietà che è possibile utilizzare per modificare l'aspetto e il comportamento di base delle relative celle, righe e colonne.  Se, per esigenze speciali, è necessario estendere le capacità della classe <xref:System.Windows.Forms.DataGridViewCellStyle>, è anche possibile implementare il disegno personalizzato per il controllo o estenderne le capacità creando celle, colonne e righe personalizzate.  
  
 Per disegnare celle e righe personalizzate, è possibile gestire vari eventi `DataGridView`.  Per modificare la funzionalità esistente o fornire nuove funzionalità, si possono creare tipi personalizzati derivati dai tipi `DataGridViewCell`, `DataGridViewColumn` e `DataGridViewRow` già presenti.  È anche possibile fornire nuove capacità di modifica mediante la creazione di tipi derivati che consentono di visualizzare un controllo a propria scelta quando una cella è in modalità di modifica.  
  
## In questa sezione  
 [Procedura: personalizzare l'aspetto delle celle nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/customize-the-appearance-of-cells-in-the-datagrid.md)  
 Viene illustrato come gestire l'evento <xref:System.Windows.Forms.DataGridView.CellPainting> per disegnare le celle manualmente.  
  
 [Procedura: personalizzare l'aspetto delle righe nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/customize-the-appearance-of-rows-in-the-datagrid.md)  
 Viene illustrato come gestire gli eventi <xref:System.Windows.Forms.DataGridView.RowPrePaint> e <xref:System.Windows.Forms.DataGridView.RowPostPaint> per disegnare righe con uno sfondo sfumato personalizzato e un contenuto che occupa più colonne.  
  
 [Procedura: personalizzare celle e colonne nel controllo DataGridView di Windows Form estendendone il comportamento e l'aspetto](../../../../docs/framework/winforms/controls/customize-cells-and-columns-in-the-datagrid-by-extending-behavior.md)  
 Viene illustrato come creare tipi personalizzati derivati dai tipi `DataGridViewCell` e `DataGridViewColumn` per evidenziare le celle quando il puntatore del mouse viene posizionato sopra di esse.  
  
 [Procedura: disabilitare i pulsanti in una colonna del controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/disable-buttons-in-a-button-column-in-the-datagrid.md)  
 Viene illustrato come creare tipi personalizzati derivati dai tipi <xref:System.Windows.Forms.DataGridViewButtonCell> e <xref:System.Windows.Forms.DataGridViewButtonColumn> per visualizzare i pulsanti disabilitati in una colonna di pulsanti.  
  
 [Procedura: inserire controlli in celle del controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-host-controls-in-windows-forms-datagridview-cells.md)  
 Viene descritto come implementare l'interfaccia `IDataGridViewEditingControl` e creare tipi personalizzati derivati da `DataGridViewCell` e `DataGridViewColumn` allo scopo di visualizzare un controllo <xref:System.Windows.Forms.DateTimePicker> quando una cella è in modalità di modifica.  
  
## Riferimenti  
 <xref:System.Windows.Forms.DataGridView>  
 Viene fornita la documentazione di riferimento per il controllo <xref:System.Windows.Forms.DataGridView>.  
  
 <xref:System.Windows.Forms.DataGridViewCell>  
 Viene fornita la documentazione di riferimento per la classe <xref:System.Windows.Forms.DataGridViewCell>.  
  
 <xref:System.Windows.Forms.DataGridViewRow>  
 Viene fornita la documentazione di riferimento per la classe <xref:System.Windows.Forms.DataGridViewRow>.  
  
 <xref:System.Windows.Forms.DataGridViewColumn>  
 Viene fornita la documentazione di riferimento per la classe <xref:System.Windows.Forms.DataGridViewColumn>.  
  
 <xref:System.Windows.Forms.IDataGridViewEditingControl>  
 Viene fornita la documentazione di riferimento per l'interfaccia <xref:System.Windows.Forms.IDataGridViewEditingControl>.  
  
## Sezioni correlate  
 [Formattazione e stile di base nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)  
 Vengono forniti argomenti in cui è descritto come modificare l'aspetto di base del controllo e il formato di visualizzazione dei dati delle celle.  
  
## Vedere anche  
 [Controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)   
 [Tipi di colonna nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/column-types-in-the-windows-forms-datagridview-control.md)