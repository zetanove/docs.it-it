---
title: "Formattazione di dati nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "dati [Windows Form], formattazione nelle griglie"
  - "griglie dei dati, formattazione di dati"
  - "DataGridView (controllo) [Windows Form], formattazione di dati"
ms.assetid: 07bf558d-3748-42ba-8ba0-37fdef924081
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Formattazione di dati nel controllo DataGridView di Windows Form
Il controllo <xref:System.Windows.Forms.DataGridView> consente la conversione automatica tra i valori delle celle e i tipi di dati visualizzati nelle colonne padre.  Le colonne di caselle di testo, ad esempio, visualizzano rappresentazioni in forma di stringa di valori di data, ora, numero ed enumerazione e convertono i valori di stringa immessi dall'utente nei tipi richiesti dall'archivio dati.  
  
## Formattazione mediante la classe DataGridViewCellStyle  
 Il controllo <xref:System.Windows.Forms.DataGridView> fornisce la formattazione base dei dati per i valori delle celle mediante la classe <xref:System.Windows.Forms.DataGridViewCellStyle>.  È possibile utilizzare la proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A> per formattare valori di data, ora, numero ed enumerazione per le impostazioni cultura predefinite correnti utilizzando gli identificatori di formato descritti in [Formattazione di tipi](../../../../docs/standard/base-types/formatting-types.md).  È anche possibile formattare tali valori per impostazioni cultura specifiche utilizzando la proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.FormatProvider%2A>.  Il formato specificato viene utilizzato sia per visualizzare i dati che per analizzare i dati immessi dall'utente in tale formato.  
  
 La classe <xref:System.Windows.Forms.DataGridViewCellStyle> fornisce ulteriori proprietà di formattazione per ritorno a capo automatico, allineamento del testo e visualizzazione personalizzata dei valori Null del database.  Per ulteriori informazioni, vedere [Procedura: formattare i dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-format-data-in-the-windows-forms-datagridview-control.md).  
  
## Formattazione mediante l'evento CellFormatting  
 Se la formattazione di base non soddisfa le proprie esigenze, è possibile specificare una formattazione personalizzata dei dati in un gestore per l'evento <xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=fullName>.  I dati <xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs> trasferiti al gestore includono una proprietà <xref:System.Windows.Forms.ConvertEventArgs.Value%2A> che inizialmente contiene il valore della cella.  In genere tale valore viene convertito automaticamente in base al tipo di visualizzazione.  Per convertire direttamente il valore, impostare la proprietà <xref:System.Windows.Forms.ConvertEventArgs.Value%2A> su un valore del tipo di visualizzazione.  
  
> [!NOTE]
>  Se per la cella è attiva una stringa di formato, sostituirà la modifica apportata al valore della proprietà <xref:System.Windows.Forms.ConvertEventArgs.Value%2A> a meno che la proprietà <xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs.FormattingApplied%2A> non sia impostata su `true`.  
  
 L'evento <xref:System.Windows.Forms.DataGridView.CellFormatting> risulta utile anche quando si desidera impostare proprietà <xref:System.Windows.Forms.DataGridViewCellStyle> per singole celle in base ai rispettivi valori.  Per ulteriori informazioni, vedere [Procedura: formattare dati personalizzati in un controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md).  
  
 Se l'analisi predefinita dei valori specificati dall'utente non risulta soddisfacente, è possibile gestire l'evento <xref:System.Windows.Forms.DataGridView.CellParsing> del controllo <xref:System.Windows.Forms.DataGridView> per fornire un'analisi personalizzata.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewCellStyle>   
 [Visualizzazione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)   
 [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)   
 [Procedura: formattare i dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-format-data-in-the-windows-forms-datagridview-control.md)   
 [Procedura: formattare dati personalizzati in un controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)