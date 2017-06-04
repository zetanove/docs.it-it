---
title: "Differenze tra i controlli DataGridView e DataGrid di Windows Form | Microsoft Docs"
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
  - "griglie dei dati"
  - "DataGrid (controllo) [Windows Form], confronto con il controllo DataGridView"
  - "DataGridView (controllo) [Windows Form], confronto con il controllo DataGrid"
ms.assetid: d412c786-140e-4210-8a56-a68467530a55
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Differenze tra i controlli DataGridView e DataGrid di Windows Form
Il controllo <xref:System.Windows.Forms.DataGridView> è un nuovo controllo che sostituisce il controllo <xref:System.Windows.Forms.DataGrid>.  Il controllo <xref:System.Windows.Forms.DataGridView> fornisce diverse funzionalità di base e avanzate che mancano nel controllo <xref:System.Windows.Forms.DataGrid>.  Inoltre l'architettura del controllo <xref:System.Windows.Forms.DataGridView> facilita l'estensione e la personalizzazione molto più del controllo <xref:System.Windows.Forms.DataGrid>.  
  
 Nella tabella seguente vengono descritte alcune delle funzionalità principali disponibili nel controllo <xref:System.Windows.Forms.DataGridView> che mancano nel controllo <xref:System.Windows.Forms.DataGrid>.  
  
|Funzionalità del controllo DataGridView|Descrizione|  
|---------------------------------------------|-----------------|  
|Più tipi di colonne|Il controllo <xref:System.Windows.Forms.DataGridView> fornisce più tipi di colonne incorporate rispetto al controllo <xref:System.Windows.Forms.DataGrid>.  Questi tipi di colonne soddisfano i requisiti della maggior parte degli scenari, ma sono anche più facili da estendere o sostituire rispetto ai tipi di colonne nel controllo <xref:System.Windows.Forms.DataGrid>.  Per ulteriori informazioni, vedere [Tipi di colonna nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/column-types-in-the-windows-forms-datagridview-control.md).|  
|Più modalità di visualizzazione dei dati|Il controllo <xref:System.Windows.Forms.DataGrid> si limita a visualizzare i dati di un'origine dati esterna.  Il controllo <xref:System.Windows.Forms.DataGridView>, tuttavia, può visualizzare i dati non associati archiviati nel controllo, i dati di un'origine dati associata o associare e annullare l'associazione dei dati.  È inoltre possibile implementare la modalità virtuale nel controllo <xref:System.Windows.Forms.DataGridView> per consentire la gestione personalizzata dei dati.  Per ulteriori informazioni, vedere [Modalità di visualizzazione dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/data-display-modes-in-the-windows-forms-datagridview-control.md).|  
|Più modalità di personalizzazione della visualizzazione dei dati|Il controllo <xref:System.Windows.Forms.DataGridView> fornisce molte proprietà ed eventi che consentono di specificare la modalità di formattazione e visualizzazione dei dati.  Ad esempio, è possibile modificare l'aspetto di celle, righe e colonne a seconda dei dati in esse contenuti oppure sostituire i dati di un tipo con i dati equivalenti di un altro tipo.  Per ulteriori informazioni, vedere [Formattazione di dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/data-formatting-in-the-windows-forms-datagridview-control.md).|  
|Più opzioni per la modifica dell'aspetto e del funzionamento di celle, righe, colonne e intestazioni|Il controllo <xref:System.Windows.Forms.DataGridView> consente di utilizzare singoli componenti di una griglia in numerosi modi diversi.  Ad esempio, è possibile bloccare righe e colonne per evitarne lo scorrimento; nascondere righe, colonne e intestazioni; cambiare la modalità di modifica delle dimensioni di righe, colonne e intestazioni; modificare la modalità di selezione da parte degli utenti; e fornire descrizioni comandi e menu di scelta rapida per singole celle, righe e colonne.|  
  
 Il controllo <xref:System.Windows.Forms.DataGrid> viene mantenuto per la compatibilità con le versioni precedenti e per esigenze speciali.  Per quasi tutti gli scopi è necessario utilizzare il controllo <xref:System.Windows.Forms.DataGridView>.  L'unica funzionalità disponibile nel controllo <xref:System.Windows.Forms.DataGrid>, ma non disponibile nel controllo <xref:System.Windows.Forms.DataGridView>, è la visualizzazione gerarchica delle informazioni di due tabelle correlate in un unico controllo.  È necessario utilizzare due controlli <xref:System.Windows.Forms.DataGridView> per visualizzare le informazioni di due tabelle che hanno una relazione Master\-Details.  
  
## Aggiornamento al controllo DataGridView  
 Se si dispone di applicazioni che utilizzano il controllo <xref:System.Windows.Forms.DataGrid> in un semplice scenario associato ai dati con personalizzazioni, è sufficiente sostituire il controllo vecchio con quello nuovo.  Entrambi i controlli utilizzano l'architettura di associazione di dati Windows Form standard, quindi il controllo <xref:System.Windows.Forms.DataGridView> visualizza i dati associati senza bisogno di altre configurazioni.  È possibile trarre vantaggio dai perfezionamenti dell'associazione di dati. A questo scopo associare i dati a un componente <xref:System.Windows.Forms.BindingSource>, che è possibile quindi associare al controllo <xref:System.Windows.Forms.DataGridView>.  Per ulteriori informazioni, vedere [Il componente BindingSource](../../../../docs/framework/winforms/controls/bindingsource-component.md).  
  
 Poiché il controllo <xref:System.Windows.Forms.DataGridView> presenta un'architettura completamente nuova, non esiste un percorso di conversione diretto che consenta di utilizzare le personalizzazioni della classe <xref:System.Windows.Forms.DataGrid> con il controllo <xref:System.Windows.Forms.DataGridView>.  Tuttavia, grazie alle funzionalità incorporate disponibili nel nuovo controllo, molte personalizzazioni della classe <xref:System.Windows.Forms.DataGrid> non sono necessarie con il controllo <xref:System.Windows.Forms.DataGridView>.  Se si sono creati tipi di colonne personalizzati per il controllo <xref:System.Windows.Forms.DataGrid> che si desidera utilizzare con il controllo <xref:System.Windows.Forms.DataGridView>, è necessario implementarli di nuovo mediante la nuova architettura.  Per ulteriori informazioni, vedere [Personalizzazione del controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/customizing-the-windows-forms-datagridview-control.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGrid>   
 <xref:System.Windows.Forms.BindingSource>   
 [Controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)   
 [Controllo DataGrid](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)   
 [Il componente BindingSource](../../../../docs/framework/winforms/controls/bindingsource-component.md)   
 [Tipi di colonna nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/column-types-in-the-windows-forms-datagridview-control.md)   
 [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)   
 [Modalità di visualizzazione dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/data-display-modes-in-the-windows-forms-datagridview-control.md)   
 [Formattazione di dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/data-formatting-in-the-windows-forms-datagridview-control.md)   
 [Opzioni di ridimensionamento nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/sizing-options-in-the-windows-forms-datagridview-control.md)   
 [Modalità di ordinamento delle colonne nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/column-sort-modes-in-the-windows-forms-datagridview-control.md)   
 [Modalità di selezione nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/selection-modes-in-the-windows-forms-datagridview-control.md)   
 [Personalizzazione del controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/customizing-the-windows-forms-datagridview-control.md)