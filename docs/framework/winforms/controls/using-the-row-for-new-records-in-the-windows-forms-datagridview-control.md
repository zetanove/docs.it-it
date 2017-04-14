---
title: "Utilizzo della riga per i nuovi record del controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "DataGridView (controllo) [Windows Form], aggiunta di righe per nuovi record"
  - "DataGridView (controllo) [Windows Form], immissione di dati"
  - "righe, nuovi record"
ms.assetid: 6110f1ea-9794-442c-a98a-f104a1feeaf4
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Utilizzo della riga per i nuovi record del controllo DataGridView di Windows Form
Quando si utilizza un controllo <xref:System.Windows.Forms.DataGridView> per modificare i dati in un'applicazione, spesso si desidera consentire agli utenti di aggiungere nuove righe di dati all'archivio dati.  Il controllo <xref:System.Windows.Forms.DataGridView> supporta questa funzionalità fornendo una riga per i nuovi record, che viene sempre visualizzata come ultima riga  e contrassegnata con un asterisco \(\*\) nell'intestazione.  Nelle seguenti sezioni vengono discussi alcuni degli aspetti da considerare durante la programmazione se si utilizza una riga per i nuovi record.  
  
## Visualizzazione della riga per i nuovi record  
 Utilizzare la proprietà <xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A> per indicare se la riga per i nuovi record viene visualizzata.  Il valore predefinito di questa proprietà è `true`.  
  
 Se i dati sono associati, la riga per i nuovi record viene visualizzata se la proprietà <xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A> del controllo e la proprietà <xref:System.ComponentModel.IBindingList.AllowNew%2A?displayProperty=fullName> dell'origine dati sono entrambe `true`.  Se una delle due proprietà è `false`, la riga non viene visualizzata.  
  
## Compilazione della riga per i nuovi record con dati predefiniti  
 Quando l'utente seleziona la riga per i nuovi record come riga corrente, il controllo <xref:System.Windows.Forms.DataGridView> genera l'evento <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded>  
  
 Questo evento fornisce l'accesso alla nuova riga <xref:System.Windows.Forms.DataGridViewRow> e consente di compilarla con dati predefiniti.  Per ulteriori informazioni, vedere [Procedura: specificare i valori predefiniti per le nuove righe nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/specify-default-values-for-new-rows-in-the-datagrid.md)  
  
## La raccolta Rows  
 La riga per nuovi record è contenuta nella raccolta <xref:System.Windows.Forms.DataGridView.Rows%2A> del controllo <xref:System.Windows.Forms.DataGridView>, ma si comporta in modo diverso sotto due aspetti:  
  
-   La riga per i nuovi record non può essere rimossa dalla raccolta <xref:System.Windows.Forms.DataGridView.Rows%2A> a livello di codice,  altrimenti verrà generata un'eccezione <xref:System.InvalidOperationException>.  L'utente inoltre non può eliminare la riga per i nuovi record  perché il metodo <xref:System.Windows.Forms.DataGridViewRowCollection.Clear%2A?displayProperty=fullName> non rimuove tale riga dalla raccolta <xref:System.Windows.Forms.DataGridView.Rows%2A>.  
  
-   Non è possibile aggiungere alcuna riga dopo la riga per i nuovi record,  altrimenti verrà generata un'eccezione <xref:System.InvalidOperationException>.  Di conseguenza, la riga per i nuovi record è sempre l'ultima riga del controllo <xref:System.Windows.Forms.DataGridView>.  I metodi che consentono di aggiungere righe a <xref:System.Windows.Forms.DataGridViewRowCollection>, <xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A>, <xref:System.Windows.Forms.DataGridViewRowCollection.AddCopy%2A> e <xref:System.Windows.Forms.DataGridViewRowCollection.AddCopies%2A> chiamano tutti internamente i metodi di inserimento quando è presente la riga per i nuovi record.  
  
## Personalizzazione della visualizzazione della riga per i nuovi record  
 Quando viene creata, la riga per i nuovi record è basata sulla riga specificata dalla proprietà <xref:System.Windows.Forms.DataGridView.RowTemplate%2A>.  Eventuali stili di cella non specificati per questa riga vengono ereditati da altre proprietà.  Per ulteriori informazioni sull'ereditarietà degli stili delle celle, vedere [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md).  
  
 I valori iniziali visualizzati dalle celle nella riga per i nuovi record vengono recuperati dalla proprietà <xref:System.Windows.Forms.DataGridViewCell.DefaultNewRowValue%2A> di ciascuna cella.  Per le celle di tipo <xref:System.Windows.Forms.DataGridViewImageCell>, la proprietà restituisce un'immagine segnaposto,  mentre negli altri casi restituisce `null`.  Sebbene sia possibile eseguire l'override di questa proprietà per restituire un valore personalizzato,  i valori iniziali possono essere sostituiti da un gestore eventi <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded> quando la riga per i nuovi record diventa attiva.  
  
 Le icone standard per l'intestazione della riga, ossia una freccia o un asterisco, non sono esposte pubblicamente.  Se si desidera personalizzare le icone, è necessario creare una classe <xref:System.Windows.Forms.DataGridViewRowHeaderCell> personalizzata.  
  
 Le icone standard utilizzano la proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A> dello stile <xref:System.Windows.Forms.DataGridViewCellStyle> in uso nella cella dell'intestazione di riga.  Le icone standard non vengono rappresentate se lo spazio disponibile non è sufficiente a visualizzarle completamente.  
  
 Se per la cella dell'intestazione di riga è impostato un valore di stringa e lo spazio non è sufficiente sia per il testo che per l'icona, verrà prima rimossa l'icona.  
  
## Ordinamento  
 In modalità non associata i nuovi record vengono sempre aggiunti alla fine del controllo <xref:System.Windows.Forms.DataGridView>, anche se il contenuto del controllo è stato ordinato.  Sarà quindi necessario applicare nuovamente l'ordinamento per visualizzare le righe nella posizione corretta \(comportamento simile a quello del controllo <xref:System.Windows.Forms.ListView>\).  
  
 In modalità associata e in modalità virtuale il comportamento dell'inserimento quando viene applicato un ordinamento dipende dall'implementazione del modello dati.  In [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)], la riga viene immediatamente ordinata nella posizione corretta.  
  
## Altre note relative alla riga per i nuovi record  
 Non è possibile impostare la proprietà <xref:System.Windows.Forms.DataGridViewRow.Visible%2A> di questa riga su `false`,  altrimenti verrà generata un'eccezione <xref:System.InvalidOperationException>.  
  
 La riga per i nuovi record viene sempre creata come non selezionata.  
  
## Modalità virtuale  
 Se si implementa la modalità virtuale, è necessario tenere traccia di quando è necessaria una riga per i nuovi record nel modello dati e di quando eseguire il rollback per l'aggiunta di tale riga.  L'implementazione esatta di questa funzionalità dipende dall'implementazione del modello dati e dalla relativa semantica delle transazioni, ad esempio se l'ambito del commit è a livello di cella o di riga.  Per ulteriori informazioni, vedere [Modo virtuale nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/virtual-mode-in-the-windows-forms-datagridview-control.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded?displayProperty=fullName>   
 [Immissione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/data-entry-in-the-windows-forms-datagridview-control.md)   
 [Procedura: specificare i valori predefiniti per le nuove righe nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/specify-default-values-for-new-rows-in-the-datagrid.md)