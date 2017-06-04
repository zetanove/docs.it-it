---
title: "Cenni preliminari sul controllo DataGridView (Windows Form) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "DataGridView"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli con associazione, DataGridView (controllo)"
  - "colonne [Windows Form], DataGridView (controllo)"
  - "dati [Windows Form], esplorazione"
  - "dati [Windows Form], riordinamento"
  - "associazione dati, DataGridView (controllo)"
  - "griglie dei dati, informazioni sulle griglie dei dati"
  - "origini dati, associazione al controllo DataGridView"
  - "DataGridView (controllo) [Windows Form], informazioni sul controllo DataGridView"
  - "DataGridView (controllo) [Windows Form], associazione dati"
  - "dataset [Windows Form], associazione al controllo DataGridView"
  - "griglia (controlli) [Windows Form]"
  - "griglie [Windows Form]"
  - "tabelle [Windows Form], associazione al controllo DataGridView"
  - "tabelle [Windows Form], visualizzazione nel controllo DataGridView"
ms.assetid: 0a45c661-89dc-4390-9cc6-c47eee501488
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# Cenni preliminari sul controllo DataGridView (Windows Form)
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.DataGridView> sostituisca il controllo <xref:System.Windows.Forms.DataGrid> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.DataGrid> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  Per ulteriori informazioni vedere [Differenze tra i controlli DataGridView e DataGrid di Windows Form](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md).  
  
 Il controllo <xref:System.Windows.Forms.DataGridView> consente di visualizzare e modificare i dati tabulari da molti tipi diversi di origini dati.  
  
 L'associazione di dati al controllo <xref:System.Windows.Forms.DataGridView> è diretta e intuitiva e in molti casi semplice come l'impostazione della proprietà <xref:System.Windows.Forms.DataGridView.DataSource%2A>.  Quando si esegue l'associazione a un'origine dati che contiene più elenchi o tabelle, impostare la proprietà <xref:System.Windows.Forms.DataGridView.DataMember%2A> su una stringa che indichi l'elenco o la tabella a cui eseguire l'associazione.  
  
 Il controllo <xref:System.Windows.Forms.DataGridView> supporta il modello di associazione dati standard di Windows Form e quindi l'associazione viene eseguita alle istanze delle classi descritte nell'elenco che segue.  
  
-   Tutte le classi che implementano l'interfaccia <xref:System.Collections.IList>, incluse le matrici unidimensionali.  
  
-   Tutte le classi che implementano l'interfaccia <xref:System.ComponentModel.IListSource>, ad esempio le classi <xref:System.Data.DataTable> e <xref:System.Data.DataSet>.  
  
-   Tutte le classi che implementano l'interfaccia <xref:System.ComponentModel.IBindingList>, ad esempio la classe <xref:System.ComponentModel.BindingList%601>.  
  
-   Tutte le classi che implementano l'interfaccia <xref:System.ComponentModel.IBindingListView>, ad esempio la classe <xref:System.Windows.Forms.BindingSource>.  
  
 Il controllo <xref:System.Windows.Forms.DataGridView> supporta l'associazione dati alle proprietà pubbliche degli oggetti restituiti da queste interfacce o alla raccolta delle proprietà restituita da un'interfaccia <xref:System.ComponentModel.ICustomTypeDescriptor>, se implementato sugli oggetti restituiti.  
  
 In genere, l'associazione verrà eseguita a un componente <xref:System.Windows.Forms.BindingSource> e il componente <xref:System.Windows.Forms.BindingSource> verrà associato a un'altra origine dati o verrà popolato con oggetti business.  Il componente <xref:System.Windows.Forms.BindingSource> è l'origine dati preferita in quanto è in grado di eseguire l'associazione a numerose origini dati e di risolvere automaticamente molti problemi relativi all'associazione dati.  Per ulteriori informazioni, vedere [Il componente BindingSource](../../../../docs/framework/winforms/controls/bindingsource-component.md).  
  
 Il controllo <xref:System.Windows.Forms.DataGridView> può anche essere utilizzato in modalità *svincolata*, senza archivi dati sottostanti.  Per un esempio di codice in cui viene utilizzato un controllo <xref:System.Windows.Forms.DataGridView> svincolato, vedere [Procedura dettagliata: creazione di un controllo DataGridView Windows Form non associato](../../../../docs/framework/winforms/controls/walkthrough-creating-an-unbound-windows-forms-datagridview-control.md).  
  
 Il controllo <xref:System.Windows.Forms.DataGridView> è particolarmente configurabile ed estendibile e fornisce un gran numero di proprietà, metodi ed eventi per la personalizzazione di aspetto e comportamento.  Quando si desidera visualizzare i dati in formato tabulare nell'applicazione Windows Form, prendere in considerazione l'utilizzo del controllo <xref:System.Windows.Forms.DataGridView> prima degli altri \(ad esempio, <xref:System.Windows.Forms.DataGrid>\).  Se si intende visualizzare una griglia di piccole dimensioni di dati in sola lettura oppure se si desidera consentire a un utente di modificare una tabella con milioni di record, il controllo <xref:System.Windows.Forms.DataGridView> fornisce una soluzione facilmente programmabile e poco dispendiosa in termini di utilizzo della memoria.  
  
## Argomenti della sezione  
 [Riepilogo della tecnologia del controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-technology-summary-windows-forms.md)  
 Vengono riepilogati i concetti relativi al controllo <xref:System.Windows.Forms.DataGridView> e l'utilizzo delle classi collegate.  
  
 [Architettura del controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-architecture-windows-forms.md)  
 Viene descritta l'architettura del controllo <xref:System.Windows.Forms.DataGridView> e ne viene illustrata la gerarchia dei tipi e la struttura di ereditarietà.  
  
 [Scenari del controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-scenarios-windows-forms.md)  
 Vengono illustrati gli scenari più comuni di utilizzo dei controlli <xref:System.Windows.Forms.DataGridView>.  
  
 [Directory del codice del controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-code-directory-windows-forms.md)  
 Vengono forniti collegamenti a esempi di codice presenti nella documentazione per varie attività relative al controllo <xref:System.Windows.Forms.DataGridView>.  Questi esempi sono suddivisi in categorie in base al tipo di attività.  
  
## Sezioni correlate  
 [Tipi di colonna nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/column-types-in-the-windows-forms-datagridview-control.md)  
 Vengono illustrati i tipi di colonne all'interno del controllo <xref:System.Windows.Forms.DataGridView> di Windows Form utilizzati per visualizzare informazioni e consentire agli utenti di modificare o aggiungere informazioni.  
  
 [Visualizzazione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)  
 Vengono forniti argomenti in cui è descritto come compilare il controllo con dati manualmente o con un'origine dati esterna.  
  
 [Personalizzazione del controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/customizing-the-windows-forms-datagridview-control.md)  
 Vengono forniti argomenti in cui sono descritti il disegno personalizzato di celle e righe <xref:System.Windows.Forms.DataGridView> e la creazione di tipi di celle, colonne e righe derivati.  
  
 [Ottimizzazione delle prestazioni nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/performance-tuning-in-the-windows-forms-datagridview-control.md)  
 Vengono forniti argomenti in cui è descritto come utilizzare il controllo in modo efficare per evitare problemi di prestazioni durante l'utilizzo di grandi quantità di dati.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.BindingSource>   
 [Controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)   
 [Funzionalità predefinite nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/default-functionality-in-the-windows-forms-datagridview-control.md)   
 [Gestione predefinita di tastiera e mouse nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/default-keyboard-and-mouse-handling-in-the-windows-forms-datagridview-control.md)