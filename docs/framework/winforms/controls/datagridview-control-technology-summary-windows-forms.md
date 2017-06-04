---
title: "Riepilogo della tecnologia del controllo DataGridView (Windows Form) | Microsoft Docs"
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
  - "griglie dei dati, informazioni sulle griglie dei dati"
  - "DataGridView (controllo) [Windows Form], informazioni sul controllo DataGridView"
ms.assetid: 094498c3-a126-4a3f-83fe-f69e96c7717b
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Riepilogo della tecnologia del controllo DataGridView (Windows Form)
In questo argomento vengono riepilogate le informazioni sul controllo `DataGridView` e sulle classi che ne supportano l'utilizzo.  
  
 La visualizzazione dei dati in formato tabulare è un'attività che può essere eseguita frequentemente.  Il controllo `DataGridView` è progettato come soluzione completa per la presentazione dei dati in una griglia.  
  
## Parole chiave  
 DataGridView, BindingSource, tabella, cella, associazione dati, modalità virtuale  
  
## Spazi dei nomi  
 <xref:System.Windows.Forms?displayProperty=fullName>  
  
 <xref:System.Data?displayProperty=fullName>  
  
## Tecnologie correlate  
 `BindingSource`  
  
## Background  
 I progettatori dell'interfaccia utente trovano spesso necessario che gli utenti visualizzino i dati in formato tabulare.  [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] fornisce diversi metodi per mostrare i dati in una tabella o una griglia.  Il controllo `DataGridView` rappresenta l'evoluzione più avanzata di questo tipo di tecnologia per le applicazioni Windows Form.  
  
 Il controllo `DataGridView` consente di visualizzare righe di dati contenute in un archivio dati.  Sono supportati molti tipi di archivi dati.  L'archivio dati può contenere dati semplici e non tipizzati, ad esempio matrici unidimensionali, oppure dati tipizzati, ad esempio <xref:System.Data.DataSet>.  Per ulteriori informazioni, vedere [Procedura: associare dati al controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-bind-data-to-the-windows-forms-datagridview-control.md).  
  
 Il controllo `DataGridView` fornisce un sistema efficiente e flessibile per visualizzare i dati in formato tabulare.  È possibile utilizzare il controllo per la visualizzazione di serie di dati di qualsiasi dimensione in sola lettura o con possibilità di modifica.  
  
 Il controllo `DataGridView` può essere esteso in molti modi per inserire comportamenti predefiniti all'interno delle applicazioni.  È possibile specificare ad esempio propri algoritmi di ordinamento a livello di codice e creare tipi personalizzati di celle.  L'aspetto del controllo `DataGridView` può inoltre essere personalizzato facilmente scegliendo diverse proprietà.  Molti tipi di archivi dati possono essere utilizzati come origine dati. In alternativa, il controllo `DataGridView` può funzionare senza che vi sia associata un'origine dati.  
  
## Implementazione delle classi DataGridView  
 Le funzioni di Extensibility del controllo `DataGridView` possono essere sfruttate in molti modi.  È possibile personalizzare numerosi aspetti del controllo mediante eventi e proprietà, ma per alcune personalizzazioni è necessario creare nuove classi derivate dalle classi `DataGridView` già presenti.  
  
 Le classi utilizzate più di frequente sono `DataGridViewCell` e `DataGridViewColumn`.  La classe relativa alla cella può essere derivata da `DataGridViewCell` o da una delle relative classi figlie.  Sebbene sia possibile aggiungere tipi di cella a qualsiasi colonna, verrà in genere utilizzata una classe di colonna associata derivata da `DataGridViewColumn`, in cui per impostazione predefinita vengono inserite le celle del tipo di cella personalizzato.  
  
 È possibile implementare l'interfaccia `IDataGridViewEditingCell` nella classe di cella derivata per creare un tipo di cella che disponga di funzionalità di modifica ma che non contenga un controllo in modalità di modifica.  Per creare un controllo che sia possibile inserire in una cella in modalità di modifica, è possibile implementare l'interfaccia `IDataGridViewEditingControl` in una classe derivata da <xref:System.Windows.Forms.Control>.  
  
 Per ulteriori informazioni, vedere [Procedura: personalizzare celle e colonne nel controllo DataGridView di Windows Form estendendone il comportamento e l'aspetto](../../../../docs/framework/winforms/controls/customize-cells-and-columns-in-the-datagrid-by-extending-behavior.md) e [Procedura: inserire controlli in celle del controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-host-controls-in-windows-forms-datagridview-cells.md).  
  
## Riepilogo delle classi DataGridView  
 <xref:System.Windows.Forms>  
  
|Area tecnologica|Classi\/interfacce\/elementi di configurazione|  
|----------------------|----------------------------------------------------|  
|Associazione dati|<xref:System.Windows.Forms.BindingSource>|  
|Presentazione dei dati|<xref:System.Windows.Forms.DataGridView><br /><br /> <xref:System.Windows.Forms.DataGridViewCell> e classi derivate<br /><br /> <xref:System.Windows.Forms.DataGridViewRow> e classi derivate<br /><br /> <xref:System.Windows.Forms.DataGridViewColumn> e classi derivate<br /><br /> <xref:System.Windows.Forms.DataGridViewCellStyle>|  
|Extensibility <xref:System.Windows.Forms.DataGridView>|<xref:System.Windows.Forms.DataGridViewCell> e classi derivate<br /><br /> <xref:System.Windows.Forms.DataGridViewColumn> e classi derivate<br /><br /> <xref:System.Windows.Forms.IDataGridViewEditingCell><br /><br /> <xref:System.Windows.Forms.IDataGridViewEditingControl>|  
  
## Novità  
 Il controllo <xref:System.Windows.Forms.DataGridView> è progettato come soluzione completa per la visualizzazione dei dati in formato tabulare con Windows Form.  Quando si crea una nuova applicazione, prendere in considerazione l'utilizzo del controllo <xref:System.Windows.Forms.DataGridView> prima di altre soluzioni, come <xref:System.Windows.Forms.DataGrid>.  Per ulteriori informazioni vedere [Differenze tra i controlli DataGridView e DataGrid di Windows Form](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md).  
  
 Il controllo <xref:System.Windows.Forms.DataGridView> può interagire con il componente <xref:System.Windows.Forms.BindingSource>.  Questo componente è progettato per rappresentare l'origine dati principale di un form  ed è in grado di gestire l'interazione tra un controllo <xref:System.Windows.Forms.DataGridView> e la relativa origine dati, a prescindere dal tipo di origine dati.  
  
## Vedere anche  
 [Cenni preliminari sul controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-overview-windows-forms.md)   
 [Architettura del controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-architecture-windows-forms.md)   
 [Protezione delle informazioni di connessione](../../../../docs/framework/data/adonet/protecting-connection-information.md)