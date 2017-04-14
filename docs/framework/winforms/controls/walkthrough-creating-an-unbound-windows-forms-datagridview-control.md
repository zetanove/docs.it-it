---
title: "Procedura dettagliata: creazione di un controllo DataGridView Windows Form non associato | Microsoft Docs"
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
  - "dati [Windows Form], visualizzazione senza associazione a origini dati"
  - "dati [Windows Form], senza associazione"
  - "DataGridView (controllo) [Windows Form], visualizzazione di dati non associati a un'origine dati"
  - "DataGridView (controllo) [Windows Form], dati non associati"
  - "procedure dettagliate [Windows Form], DataGridView (controllo)"
ms.assetid: 5a8d6afa-1b4b-4b24-8db8-501086ffdebe
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura dettagliata: creazione di un controllo DataGridView Windows Form non associato
Spesso si desidera visualizzare dati in formato tabulare che non hanno origine da un database.  Ad esempio, si può desiderare di visualizzare i contenuti di una matrice bidimensionale di stringhe.  La classe <xref:System.Windows.Forms.DataGridView> fornisce un metodo semplice e personalizzabile per visualizzare i dati senza associarli a un'origine dati.  In questa procedura dettagliata viene illustrato come popolare un controllo <xref:System.Windows.Forms.DataGridView> e gestire l'aggiunta e l'eliminazione di righe in modalità "svincolata".  Per impostazione predefinita, l'utente può aggiungere nuove righe.  Per impedire l'aggiunta di nuove righe, impostare la proprietà <xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A> su `false`.  
  
 Per copiare il codice nell'argomento corrente come un elenco singolo, vedere [Procedura: creare un controllo DataGridView di Windows Form non associato](../../../../docs/framework/winforms/controls/how-to-create-an-unbound-windows-forms-datagridview-control.md).  
  
## Creazione del form  
  
#### Per utilizzare un controllo DataGridView non associato  
  
1.  Creare una classe che derivi dalla classe <xref:System.Windows.Forms.Form> e contenga le dichiarazioni di variabili di classe e il metodo `Main` riportati di seguito.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#01](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#01)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#01](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#01)]  
    [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#02](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#02)]
    [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#02](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#02)]  
  
2.  Implementare un metodo `SetupLayout` nella definizione di classe del form per impostare il layout del form.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#20)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#20)]  
  
3.  Creare un metodo `SetupDataGridView` per impostare le colonne e le proprietà della classe <xref:System.Windows.Forms.DataGridView>.  
  
     Questo metodo aggiunge il controllo <xref:System.Windows.Forms.DataGridView> alla raccolta <xref:System.Windows.Forms.Control.Controls%2A> del form.  Successivamente, il numero delle colonne da visualizzare viene impostato mediante la proprietà <xref:System.Windows.Forms.DataGridView.ColumnCount%2A>.  L'impostazione dello stile predefinito per le intestazioni di colonna dipende dall'impostazione delle proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.BackColor%2A>, <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A> e <xref:System.Windows.Forms.DataGridViewCellStyle.Font%2A> di <xref:System.Windows.Forms.DataGridViewCellStyle> restituite dalla proprietà <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A>.  
  
     Vengono impostate le proprietà del layout e dell'aspetto e vengono assegnati i nomi delle colonne.  Quando questo metodo viene chiuso, è possibile popolare il controllo <xref:System.Windows.Forms.DataGridView>.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#30](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#30)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#30](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#30)]  
  
4.  Creare un metodo `PopulateDataGridView` per aggiungere righe al controllo <xref:System.Windows.Forms.DataGridView>.  
  
     Ciascuna riga rappresenta una canzone e le informazioni associate.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#40](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#40)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#40](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#40)]  
  
5.  Con i metodi di utilità in funzione, è possibile associare gestori eventi.  
  
     Verranno gestiti gli eventi <xref:System.Windows.Forms.Control.Click> dei pulsanti **Add** e **Delete**, l'evento <xref:System.Windows.Forms.Form.Load> del form e l'evento <xref:System.Windows.Forms.DataGridView.CellFormatting> del controllo <xref:System.Windows.Forms.DataGridView>.  
  
     Quando viene generato l'evento <xref:System.Windows.Forms.Control.Click> del pulsante **Add**, alla classe <xref:System.Windows.Forms.DataGridView> viene aggiunta una nuova riga vuota.  
  
     Quando viene generato l'evento <xref:System.Windows.Forms.Control.Click> del pulsante **Delete**, la riga selezionata viene eliminata, a meno che non sia la riga riservata ai nuovi record, che consente agli utenti di aggiungere nuove righe.  Questa riga è sempre l'ultima riga all'interno del controllo <xref:System.Windows.Forms.DataGridView>.  
  
     Quando viene generato l'evento <xref:System.Windows.Forms.Form.Load> del form, vengono chiamati i metodi di utilità `SetupLayout`, `SetupDataGridView` e `PopulateDataGridView`.  
  
     Quando viene generato l'evento <xref:System.Windows.Forms.DataGridView.CellFormatting>, ciascuna cella della colonna `Date` viene formattata come data estesa, a meno che non sia possibile analizzare il valore della cella.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#10)]  
  
## Verifica dell'applicazione  
 È ora possibile verificare il form per assicurarsi che funzioni correttamente.  
  
#### Per eseguire il test del form  
  
-   ‎Premere F5 per eseguire l'applicazione.  
  
     Verrà visualizzato un controllo <xref:System.Windows.Forms.DataGridView> che conterrà le canzoni elencate in `PopulateDataGridView`.  Mediante il pulsante **Add Row** è possibile aggiungere nuove righe, mentre è possibile eliminare le righe selezionate mediante il pulsante **Delete Row**.  Il controllo <xref:System.Windows.Forms.DataGridView> non associato è l'archivio dati e i relativi dati sono indipendenti dalle origini esterne, come nel caso di una classe <xref:System.Data.DataSet> o di una matrice.  
  
## Passaggi successivi  
 Questa applicazione fornisce un'idea di massima delle capacità del controllo <xref:System.Windows.Forms.DataGridView>.  È possibile personalizzare l'aspetto e il comportamento del controllo <xref:System.Windows.Forms.DataGridView> in diversi modi:  
  
-   Modificare gli stili di bordi e intestazioni.  Per ulteriori informazioni, vedere [Procedura: modificare gli stili dei bordi e delle linee della griglia nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/change-the-border-and-gridline-styles-in-the-datagrid.md).  
  
-   Consentire o limitare l'input utente nel controllo <xref:System.Windows.Forms.DataGridView>.  Per ulteriori informazioni, vedere [Procedura: impedire l'aggiunta o l'eliminazione di righe nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/prevent-row-addition-and-deletion-datagridview.md) e [Procedura: impostare le colonne come in sola lettura nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-make-columns-read-only-in-the-windows-forms-datagridview-control.md).  
  
-   Verificare eventuali errori relativi al database nell'input utente.  Per ulteriori informazioni, vedere [Procedura dettagliata: gestione degli errori che si verificano durante l'immissione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/handling-errors-that-occur-during-data-entry-in-the-datagrid.md).  
  
-   Gestire dataset di grandi dimensioni utilizzando la modalità virtuale.  Per ulteriori informazioni, vedere [Procedura dettagliata: implementazione della modalità virtuale nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md).  
  
-   Personalizzare l'aspetto delle celle.  Per ulteriori informazioni, vedere [Procedura: personalizzare l'aspetto delle celle nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/customize-the-appearance-of-cells-in-the-datagrid.md) e [Procedura: impostare stili di cella predefiniti per il controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 [Visualizzazione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)   
 [Procedura: creare un controllo DataGridView di Windows Form non associato](../../../../docs/framework/winforms/controls/how-to-create-an-unbound-windows-forms-datagridview-control.md)   
 [Modalità di visualizzazione dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/data-display-modes-in-the-windows-forms-datagridview-control.md)