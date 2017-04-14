---
title: "Formattazione e stile di base nel controllo DataGridView Windows Form | Microsoft Docs"
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
  - "griglie dei dati, formattazione"
  - "DataGridView (controllo) [Windows Form], formattazione e stile"
ms.assetid: b9b90836-1f56-4aa9-8db8-edc78fe830e8
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Formattazione e stile di base nel controllo DataGridView Windows Form
Il controllo `DataGridView` facilita la definizione dell'aspetto di base delle celle e del formato di visualizzazione dei valori delle celle.  È possibile definire l'aspetto e gli stili di formattazione di singole celle, di celle in specifiche colonne e righe o di tutte le celle del controllo impostando le proprietà degli oggetti `DataGridViewCellStyle` a cui si accede tramite varie proprietà del controllo `DataGridView`.  È possibile inoltre modificare dinamicamente questi stili, ad esempio in base al valore della cella, gestendo l'evento `CellFormatting`.  
  
## In questa sezione  
 [Procedura: modificare gli stili dei bordi e delle linee della griglia nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/change-the-border-and-gridline-styles-in-the-datagrid.md)  
 Viene illustrato come impostare le proprietà `DataGridView` che definiscono l'aspetto del bordo del controllo e delle linee di separazione tra celle.  
  
 [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)  
 Viene illustrata la classe `DataGridViewCellStyle` e il modo in cui le proprietà di quel tipo interagiscono per definire la modalità di visualizzazione delle celle nel controllo.  
  
 [Procedura: impostare stili di cella predefiniti per il controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)  
 Viene illustrato come utilizzare le proprietà `DataGridViewCellStyle` per stabilire l'aspetto predefinito delle celle in specifiche righe e colonne e nell'intero controllo.  
  
 [Procedura: formattare i dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-format-data-in-the-windows-forms-datagridview-control.md)  
 Viene illustrato come formattare i valori di visualizzazione delle celle mediante le proprietà `DataGridViewCellStyle`.  
  
 [Procedura: impostare gli stili di carattere e colore nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-font-and-color-styles-in-the-windows-forms-datagridview-control.md)  
 Viene illustrato come utilizzare la proprietà `DefaultCellStyle` per impostare le caratteristiche di visualizzazione di base di tutte le celle del controllo.  
  
 [Procedura: impostare stili di righe alterne per il controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-alternating-row-styles-for-the-windows-forms-datagridview-control.md)  
 Viene illustrato come creare un effetto di tipo registro nel controllo visualizzando righe alterne in modo diverso.  
  
 [Procedura: utilizzare il modello di riga personalizzare le righe nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/use-the-row-template-to-customize-rows-in-the-datagrid.md)  
 Viene illustrato come utilizzare la proprietà `RowTemplate` per impostare proprietà di riga che verranno utilizzate per tutte le righe del controllo.  
  
## Riferimenti  
 <xref:System.Windows.Forms.DataGridView>  
 Viene fornita la documentazione di riferimento per il controllo <xref:System.Windows.Forms.DataGridView>.  
  
 <xref:System.Windows.Forms.DataGridViewCellStyle>  
 Viene fornita la documentazione di riferimento per la classe <xref:System.Windows.Forms.DataGridViewCellStyle>.  
  
 <xref:System.Windows.Forms.DataGridView.CellFormatting>  
 Viene fornita la documentazione di riferimento per l'evento <xref:System.Windows.Forms.DataGridView.CellFormatting>.  
  
 <xref:System.Windows.Forms.DataGridView.RowTemplate%2A>  
 Viene fornita la documentazione di riferimento per la proprietà <xref:System.Windows.Forms.DataGridView.RowTemplate%2A>.  
  
## Sezioni correlate  
 [Personalizzazione del controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/customizing-the-windows-forms-datagridview-control.md)  
 Vengono forniti argomenti in cui sono descritti il disegno personalizzato di celle e righe <xref:System.Windows.Forms.DataGridView> e la creazione di tipi di celle, colonne e righe derivati.  
  
 [Funzionalità di base per colonna, riga e cella nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/basic-column-row-and-cell-features-wf-datagridview-control.md)  
 Vengono forniti argomenti in cui sono descritte le proprietà di celle, righe e colonne utilizzate più frequentemente.  
  
## Vedere anche  
 [Controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)