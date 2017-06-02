---
title: "Modalit&#224; di ordinamento delle colonne nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "griglie dei dati, modalità di ordinamento"
  - "DataGridView (controllo) [Windows Form], modalità di ordinamento"
ms.assetid: 43715887-2df9-4da7-bcf1-b9c7c842b2bf
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Modalit&#224; di ordinamento delle colonne nel controllo DataGridView di Windows Form
Per le colonne del controllo <xref:System.Windows.Forms.DataGridView> sono disponibili tre modalità di ordinamento.  La modalità di ordinamento per ciascuna colonna viene specificata mediante la proprietà <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> della colonna, che può essere impostata su uno dei seguenti valori di enumerazione <xref:System.Windows.Forms.DataGridViewColumnSortMode>.  
  
|Valore `DataGridViewColumnSortMode`|Descrizione|  
|-----------------------------------------|-----------------|  
|<xref:System.Windows.Forms.DataGridViewColumnSortMode>|Impostazione predefinita per le colonne di caselle di testo.  A meno che le intestazioni delle colonne non vengano utilizzate per la selezione, se si fa clic su un'intestazione, il controllo <xref:System.Windows.Forms.DataGridView> viene ordinato automaticamente in base alla colonna corrispondente e viene visualizzata un'icona che indica l'ordine.|  
|<xref:System.Windows.Forms.DataGridViewColumnSortMode>|Impostazione predefinita per le colonne non di caselle di testo.  È possibile ordinare questa colonna a livello di codice ma, poiché questo tipo non supporta l'ordinamento, non viene riservato alcuno spazio per l'icona di ordinamento.|  
|<xref:System.Windows.Forms.DataGridViewColumnSortMode>|È possibile ordinare questa colonna a livello di codice e viene riservato uno spazio per l'icona di ordinamento.|  
  
 È possibile modificare la modalità di ordinamento per una colonna la cui impostazione predefinita è <xref:System.Windows.Forms.DataGridViewColumnSortMode> se la colonna contiene valori che possono essere ordinati in modo significativo.  Ad esempio, se la colonna di un database contiene numeri che rappresentano gli stati delle voci, è possibile visualizzare questi numeri sotto forma di icone associando una colonna di tipo image alla colonna del database.  È quindi possibile sostituire ai valori numerici delle celle le immagini corrispondenti in un gestore per l'evento <xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=fullName>.  In questo caso, se si imposta la proprietà <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> su <xref:System.Windows.Forms.DataGridViewColumnSortMode>, gli utenti potranno ordinare la colonna.  L'ordinamento automatico consente agli utenti di raggruppare le voci con lo stesso stato anche se gli stati corrispondenti ai numeri non rappresentano una sequenza naturale.  Le colonne di caselle di controllo sono un altro esempio in cui l'ordinamento automatico è utile per raggruppare voci con lo stesso stato.  
  
 È possibile ordinare un controllo <xref:System.Windows.Forms.DataGridView> a livello di codice in base ai valori di una o più colonne, indipendentemente dalle impostazioni di <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A>.  L'ordinamento a livello di codice risulta utile se si desidera fornire un'interfaccia utente personalizzata per l'ordinamento o implementare un ordinamento personalizzato.  Un'interfaccia utente di ordinamento personalizzata potrebbe risultare utile, ad esempio, se si imposta la modalità di selezione del controllo <xref:System.Windows.Forms.DataGridView> per consentire la selezione delle intestazioni delle colonne.  In questo caso, infatti, sebbene le intestazioni delle colonne non possano essere utilizzate per l'ordinamento, è necessario che in esse sia visualizzata l'icona di ordinamento appropriata. A tal fine, impostare la proprietà <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> su <xref:System.Windows.Forms.DataGridViewColumnSortMode>.  
  
 Per le colonne per cui è impostata la modalità di ordinamento a livello di codice non viene visualizzata automaticamente un'icona di ordinamento.  Per visualizzare l'icona per queste colonne, è necessario impostare la proprietà <xref:System.Windows.Forms.DataGridViewColumnHeaderCell.SortGlyphDirection%2A?displayProperty=fullName>.  Ciò è necessario se si desidera un ordinamento personalizzato flessibile.  Ad esempio, se si ordina il controllo <xref:System.Windows.Forms.DataGridView> in base a più colonne, è possibile visualizzare più icone di ordinamento o nessuna.  
  
 Sebbene sia possibile ordinare un controllo <xref:System.Windows.Forms.DataGridView> a livello di codice in base a qualsiasi colonna, alcune colonne, ad esempio le colonne dei pulsanti, potrebbero non contenere valori che possono essere ordinati in modo significativo.  L'impostazione <xref:System.Windows.Forms.DataGridViewColumnSortMode> della proprietà <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A> per queste colonne indica che non verranno mai utilizzate per l'ordinamento e non è quindi necessario riservare spazio nelle relative intestazioni per l'icona di ordinamento.  
  
 Quando un controllo <xref:System.Windows.Forms.DataGridView> è ordinato, è possibile determinare sia la colonna di ordinamento che l'ordine verificando i valori delle proprietà <xref:System.Windows.Forms.DataGridView.SortedColumn%2A> e <xref:System.Windows.Forms.DataGridView.SortOrder%2A>.  Questi valori non sono significativi dopo un'operazione di ordinamento personalizzato.  Per ulteriori informazioni sull'ordinamento personalizzato, vedere la sezione Ordinamento personalizzato riportata di seguito.  
  
 Quando viene ordinato un controllo <xref:System.Windows.Forms.DataGridView> che contiene colonne associate e non, i valori nelle colonne non associate non vengono mantenuti automaticamente.  Per mantenere tali valori, è necessario implementare la modalità virtuale impostando la proprietà <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> su `true` e gestendo gli eventi <xref:System.Windows.Forms.DataGridView.CellValueNeeded> e <xref:System.Windows.Forms.DataGridView.CellValuePushed>.  Per ulteriori informazioni, vedere [Procedura: implementare il modo virtuale nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-implement-virtual-mode-in-the-windows-forms-datagridview-control.md).  L'ordinamento in base a colonne non associate in modalità associata non è supportato.  
  
## Ordinamento a livello di codice  
 È possibile ordinare un controllo <xref:System.Windows.Forms.DataGridView> a livello di codice chiamando il metodo <xref:System.Windows.Forms.DataGridView.Sort%2A>.  
  
 L'overload `Sort(DataGridViewColumn,ListSortDirection)` del metodo <xref:System.Windows.Forms.DataGridView.Sort%2A> accetta una classe <xref:System.Windows.Forms.DataGridViewColumn> e un valore di enumerazione <xref:System.ComponentModel.ListSortDirection> come parametri.  Questo overload è utile per l'ordinamento in base a colonne contenenti valori che possono essere ordinati in modo significativo, ma che non si desidera configurare per l'ordinamento automatico.  Quando si chiama questo overload e si passa a una colonna con un valore <xref:System.Windows.Forms.DataGridViewColumnSortMode?displayProperty=fullName> per la proprietà <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A>, le proprietà <xref:System.Windows.Forms.DataGridView.SortedColumn%2A> e <xref:System.Windows.Forms.DataGridView.SortOrder%2A> vengono impostate automaticamente e l'icona di ordinamento appropriata viene visualizzata nell'intestazione della colonna.  
  
> [!NOTE]
>  Se il controllo <xref:System.Windows.Forms.DataGridView> è associato a un'origine dati esterna mediante l'impostazione della proprietà <xref:System.Windows.Forms.DataGridView.DataSource%2A>, l'overload del metodo `Sort(DataGridViewColumn,ListSortDirection)` non funziona per le colonne non associate.  Inoltre, se la proprietà <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> è impostata su `true`, è possibile chiamare questo overload solo per le colonne associate.  Per determinare se una colonna è associata ai dati, verificare il valore della proprietà <xref:System.Windows.Forms.DataGridViewColumn.IsDataBound%2A>.  L'ordinamento in base a colonne non associate in modalità associata non è supportato.  
  
## Ordinamento personalizzato  
 È possibile personalizzare il controllo <xref:System.Windows.Forms.DataGridView> utilizzando l'overload `Sort(IComparer)` del metodo <xref:System.Windows.Forms.DataGridView.Sort%2A> o gestendo l'evento <xref:System.Windows.Forms.DataGridView.SortCompare>.  
  
 L'overload del metodo `Sort(IComparer)` accetta come parametro un'istanza di una classe che implementa l'interfaccia <xref:System.Collections.IComparer>.  Questo overload è utile quando si desidera fornire l'ordinamento personalizzato. Ad esempio, quando i valori in una colonna non sono ordinati in modo naturale o quando l'ordine naturale non è appropriato.  In questo caso non è possibile utilizzare l'ordinamento automatico, ma è possibile consentire agli utenti di fare clic sulle intestazioni delle colonne per eseguire l'ordinamento.  È possibile chiamare questo overload in un gestore per l'evento <xref:System.Windows.Forms.DataGridView.ColumnHeaderMouseClick> anche se non si utilizzano le intestazioni delle colonne per la selezione.  
  
> [!NOTE]
>  L'overload del metodo `Sort(IComparer)` funziona solo quando il controllo <xref:System.Windows.Forms.DataGridView> non è associato a un'origine dati esterna e la proprietà <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> è impostata su `false`.  Per personalizzare l'ordinamento delle colonne associate a un'origine dati esterna, è necessario utilizzare le operazioni di ordinamento fornite dall'origine dati.  In modalità virtuale è necessario fornire operazioni di ordinamento personalizzate per le colonne non associate.  
  
 Per utilizzare l'overload del metodo `Sort(IComparer)`, è necessario creare la propria classe che implementa l'interfaccia <xref:System.Collections.IComparer>.  Nell'ambito di questa interfaccia la classe deve implementare il metodo <xref:System.Collections.IComparer.Compare%2A?displayProperty=fullName>, a cui il controllo <xref:System.Windows.Forms.DataGridView> passa gli oggetti <xref:System.Windows.Forms.DataGridViewRow> come input quando viene chiamato l'overload del metodo `Sort(IComparer)`.  In questo modo è possibile calcolare l'ordinamento corretto delle righe in base ai valori di qualsiasi colonna.  
  
 Poiché l'overload del metodo `Sort(IComparer)` non consente di impostare le proprietà <xref:System.Windows.Forms.DataGridView.SortedColumn%2A> e <xref:System.Windows.Forms.DataGridView.SortOrder%2A>, è necessario impostare sempre la proprietà <xref:System.Windows.Forms.DataGridViewColumnHeaderCell.SortGlyphDirection%2A?displayProperty=fullName> per visualizzare l'icona di ordinamento.  
  
 Un'alternativa all'overload del metodo `Sort(IComparer)` è l'ordinamento personalizzato mediante l'implementazione di un gestore per l'evento <xref:System.Windows.Forms.DataGridView.SortCompare>.  Questo evento si verifica quando gli utenti fanno clic su intestazioni di colonne per le quali è configurato l'ordinamento automatico o quando si chiama l'overload `Sort(DataGridViewColumn,ListSortDirection)` del metodo <xref:System.Windows.Forms.DataGridView.Sort%2A>.  L'evento si verifica per ciascuna coppia di righe nel controllo e consente di calcolarne l'ordine corretto.  
  
> [!NOTE]
>  L'evento <xref:System.Windows.Forms.DataGridView.SortCompare> non si verifica quando è impostata la proprietà <xref:System.Windows.Forms.DataGridView.DataSource%2A> o quando la proprietà <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> è impostata su `true`.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.Sort%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.SortedColumn%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.SortOrder%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumnHeaderCell.SortGlyphDirection%2A?displayProperty=fullName>   
 [Ordinamento dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/sorting-data-in-the-windows-forms-datagridview-control.md)   
 [Procedura: impostare le modalità di ordinamento delle colonne nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/set-the-sort-modes-for-columns-wf-datagridview-control.md)   
 [Procedura: personalizzare l'ordinamento nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-customize-sorting-in-the-windows-forms-datagridview-control.md)