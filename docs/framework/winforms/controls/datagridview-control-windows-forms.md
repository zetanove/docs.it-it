---
title: "Controllo DataGridView (Windows Form) | Microsoft Docs"
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
  - "dati [Windows Form], visualizzazione in formato tabella"
  - "griglie dei dati"
  - "presentazione dei dati"
  - "DataGridView (controllo) [Windows Form]"
  - "dataset [Windows Form], visualizzazione nel controllo DataGridView"
  - "dataset [Windows Form], interfaccia utente"
  - "griglia (controlli) [Windows Form]"
  - "tabelle [Windows Form]"
  - "dati tabulari, visualizzazione su Windows Form"
  - "Windows Form, visualizzazione di dati"
ms.assetid: dbee73f2-bba6-4874-9389-cd21d44309be
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Controllo DataGridView (Windows Form)
Il controllo `DataGridView` fornisce un sistema efficiente e flessibile per visualizzare i dati in formato tabulare.  È possibile usare il controllo `DataGridView` per mostrare le visualizzazioni di sola lettura di una piccola quantità di dati oppure ridimensionarlo per mostrare le visualizzazioni modificabili di set di dati di dimensioni molto estese.  
  
 È possibile estendere il controllo `DataGridView` in diversi modi per sviluppare comportamenti personalizzati nelle applicazioni.  Ad esempio, è possibile specificare a livello di codice i propri algoritmi di ordinamento e creare i propri tipi di celle.  È possibile personalizzare facilmente l'aspetto del controllo `DataGridView` scegliendo tra diverse proprietà.  Si possono usare molti tipi di archivi dati come origine dati, ma il controllo `DataGridView` può operare anche senza alcuna origine dati associata.  
  
 Gli argomenti di questa sezione descrivono i concetti e le tecniche che è possibile usare per compilare funzionalità `DataGridView` nelle applicazioni.  
  
## In questa sezione  
 [Cenni preliminari sul controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-overview-windows-forms.md)  
 Fornisce argomenti che descrivono l'architettura e i concetti principali del controllo `DataGridView` Windows Form.  
  
 [Funzionalità predefinite nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/default-functionality-in-the-windows-forms-datagridview-control.md)  
 Descrive l'aspetto e il comportamento predefiniti del controllo `DataGridView` Windows Form quando è associato a un'origine dati.  
  
 [Tipi di colonna nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/column-types-in-the-windows-forms-datagridview-control.md)  
 Descrive i tipi di colonna nel controllo `DataGridView` Windows Form, usati per visualizzare i dati e consentire agli utenti di modificare o aggiungere dati.  
  
 [Funzionalità di base per colonna, riga e cella nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/basic-column-row-and-cell-features-wf-datagridview-control.md)  
 Fornisce argomenti che descrivono le proprietà di uso comune di celle, righe e colonne.  
  
 [Formattazione e stile di base nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)  
 Fornisce argomenti che descrivono come modificare l'aspetto del controllo e la formattazione di base dei dati delle celle.  
  
 [Visualizzazione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)  
 Fornisce argomenti che descrivono come popolare il controllo con i dati manualmente o da un'origine dati esterna.  
  
 [Ridimensionamento di colonne e righe nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/resizing-columns-and-rows-in-the-windows-forms-datagridview-control.md)  
 Fornisce argomenti che spiegano come le dimensioni di righe e colonne possano essere adattate automaticamente al contenuto delle celle o alla larghezza disponibile del controllo.  
  
 [Ordinamento dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/sorting-data-in-the-windows-forms-datagridview-control.md)  
 Fornisce argomenti che descrivono le funzionalità di ordinamento nel controllo.  
  
 [Immissione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/data-entry-in-the-windows-forms-datagridview-control.md)  
 Fornisce argomenti che spiegano come cambiare la modalità di aggiunta e modifica dei dati nel controllo da parte degli utenti.  
  
 [Utilizzo della selezione e degli Appunti con il controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/selection-and-clipboard-use-with-the-windows-forms-datagridview-control.md)  
 Fornisce argomenti che descrivono le funzionalità di selezione di celle, righe e colonne del controllo.  
  
 [Programmazione con celle, righe e colonne nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/programming-with-cells-rows-and-columns-in-the-datagrid.md)  
 Fornisce argomenti che descrivono come eseguire la programmazione con oggetti cella, riga e colonna.  
  
 [Personalizzazione del controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/customizing-the-windows-forms-datagridview-control.md)  
 Fornisce argomenti che descrivono come disegnare celle e righe personalizzate di `DataGridView` e come creare tipi di cella, colonna e riga derivati.  
  
 [Ottimizzazione delle prestazioni nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/performance-tuning-in-the-windows-forms-datagridview-control.md)  
 Fornisce argomenti che descrivono come usare il controllo in modo efficiente per evitare problemi di prestazioni quando si lavora con grandi quantità di dati.  
  
 [Gestione predefinita di tastiera e mouse nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/default-keyboard-and-mouse-handling-in-the-windows-forms-datagridview-control.md)  
 Descrive come gli utenti possono interagire con il controllo `DataGridView` tramite tastiera e mouse.  
  
 [Differenze tra i controlli DataGridView e DataGrid di Windows Form](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)  
 Descrive come il controllo `DataGridView` migliori e sostituisca il controllo <xref:System.Windows.Forms.DataGrid>.  
  
 Vedere anche [Uso della finestra di progettazione con il controllo DataGridView Windows Form](http://msdn.microsoft.com/library/vstudio/ms171593\(v=vs.110\)).  
  
## Riferimenti  
 <xref:System.Windows.Forms.DataGridView>  
 Fornisce la documentazione di riferimento per il controllo <xref:System.Windows.Forms.DataGridView>.  
  
 <xref:System.Windows.Forms.BindingSource>  
 Fornisce la documentazione di riferimento per il componente <xref:System.Windows.Forms.BindingSource>.  Il controllo <xref:System.Windows.Forms.DataGridView> e il componente <xref:System.Windows.Forms.BindingSource> sono progettati per interagire tra loro.  
  
## Vedere anche  
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)