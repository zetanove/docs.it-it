---
title: "Stili della cella nel controllo DataGridView Windows Form | Microsoft Docs"
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
  - "celle, stili"
  - "griglie dei dati, stili della cella"
  - "DataGridView (controllo) [Windows Form], stili della cella"
ms.assetid: dbb75ed6-8804-4232-8382-f9920c2e380c
caps.latest.revision: 33
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 33
---
# Stili della cella nel controllo DataGridView Windows Form
Ogni cella contenuta nel controllo <xref:System.Windows.Forms.DataGridView> può disporre di uno stile specifico, ad esempio il formato del testo, il colore di sfondo, il colore di primo piano e il tipo di carattere.  Di solito, tuttavia, più celle condividono caratteristiche di stile particolari.  
  
 I gruppi di celle che condividono gli stili possono essere composti da tutte le celle contenute in righe o colonne particolari, da tutte le celle che contengono valori particolari o da tutte le celle del controllo.  Poiché tali gruppi si sovrappongono, è possibile che le informazioni sullo stile per ciascuna cella derivino da più fonti.  Si supponga, ad esempio, di desiderare che tutte le celle di un controllo <xref:System.Windows.Forms.DataGridView> utilizzino lo stesso tipo di carattere ma che solo le celle nelle colonne della valuta utilizzino la formattazione per la valuta e che solo le celle relative alla valuta con numeri negativi utilizzino il rosso come colore di primo piano.  
  
## Classe DataGridViewCellStyle  
 La classe <xref:System.Windows.Forms.DataGridViewCellStyle> contiene le proprietà riportate di seguito relative allo stile di visualizzazione:  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.BackColor%2A> e <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.SelectionBackColor%2A> e <xref:System.Windows.Forms.DataGridViewCellStyle.SelectionForeColor%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.Font%2A>  
  
 La classe contiene inoltre le proprietà riportate di seguito relative alla formattazione:  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A> e <xref:System.Windows.Forms.DataGridViewCellStyle.FormatProvider%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.NullValue%2A> e <xref:System.Windows.Forms.DataGridViewCellStyle.DataSourceNullValue%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.Alignment%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.Padding%2A>  
  
 Per ulteriori informazioni su queste proprietà e su altre proprietà relative allo stile delle celle, vedere la documentazione di riferimento su <xref:System.Windows.Forms.DataGridViewCellStyle> e gli argomenti elencati nella sezione Vedere anche alla fine del presente argomento.  
  
## Utilizzo di oggetti DataGridViewCellStyle  
 È possibile recuperare oggetti <xref:System.Windows.Forms.DataGridViewCellStyle> da varie proprietà delle classi <xref:System.Windows.Forms.DataGridView>, <xref:System.Windows.Forms.DataGridViewColumn>, <xref:System.Windows.Forms.DataGridViewRow> e <xref:System.Windows.Forms.DataGridViewCell> e delle classi derivate.  Se una di tali proprietà non è ancora stata impostata, il recupero del relativo valore comporterà la creazione di un nuovo oggetto <xref:System.Windows.Forms.DataGridViewCellStyle>.  È inoltre possibile creare istanze personalizzate di oggetti <xref:System.Windows.Forms.DataGridViewCellStyle> e assegnarle a tali proprietà.  
  
 Per evitare un'inutile duplicazione di informazioni sullo stile, è possibile fare in modo che oggetti <xref:System.Windows.Forms.DataGridViewCellStyle> vengano condivisi da più elementi <xref:System.Windows.Forms.DataGridView>.  Poiché gli stili impostati a livello di controllo, colonna e riga eseguono un'azione di filtro verso il basso fino al livello della cella, è inoltre possibile evitare la duplicazione degli stili impostando a ogni livello solo le proprietà di stile diverse rispetto ai livelli superiori.  Ciò viene descritto in modo più approfondito nella sezione Ereditarietà dello stile riportata di seguito.  
  
 Nella tabella seguente sono elencate le proprietà principali che ottengono o impostano oggetti <xref:System.Windows.Forms.DataGridViewCellStyle>.  
  
|Proprietà|Classi|Descrizione|  
|---------------|------------|-----------------|  
|`DefaultCellStyle`|<xref:System.Windows.Forms.DataGridView>, <xref:System.Windows.Forms.DataGridViewColumn>, <xref:System.Windows.Forms.DataGridViewRow> e classi derivate|Ottiene o imposta stili predefiniti utilizzati da tutte le celle dell'intero controllo \(celle di intestazione incluse\), di una colonna o di una riga.|  
|<xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A>|<xref:System.Windows.Forms.DataGridView>|Ottiene o imposta stili di cella predefiniti utilizzati da tutte le righe del controllo.  Le celle di intestazione sono escluse.|  
|<xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A>|<xref:System.Windows.Forms.DataGridView>|Ottiene o imposta stili di cella predefiniti utilizzati da righe alterne del controllo.  Utilizzata per creare un effetto registro.|  
|<xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A>|<xref:System.Windows.Forms.DataGridView>|Ottiene o imposta stili di cella predefiniti utilizzati dalle intestazioni di riga del controllo.  Viene sottoposta a override dal tema corrente se sono attivati gli stili di visualizzazione.|  
|<xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A>|<xref:System.Windows.Forms.DataGridView>|Ottiene o imposta stili di cella predefiniti utilizzati dalle intestazioni di colonna del controllo.  Viene sottoposta a override dal tema corrente se sono attivati gli stili di visualizzazione.|  
|<xref:System.Windows.Forms.DataGridViewCell.Style%2A>|<xref:System.Windows.Forms.DataGridViewCell> e classi derivate|Ottiene o imposta stili specificati a livello di cella.  Tali stili eseguono l'override su quelli ereditati dai livelli precedenti.|  
|`InheritedStyle`|Classi <xref:System.Windows.Forms.DataGridViewCell>, <xref:System.Windows.Forms.DataGridViewRow>, <xref:System.Windows.Forms.DataGridViewColumn> e derivate|Ottiene tutti gli stili correnti applicati alla cella, alla riga o alla colonna, tra cui gli stili ereditati dai livelli precedenti.|  
  
 Come accennato in precedenza, una volta ottenuto il valore di una proprietà di stile viene creata automaticamente un'istanza di un nuovo oggetto <xref:System.Windows.Forms.DataGridViewCellStyle>, se la proprietà non è stata ancora impostata.  Per evitare la creazione superflua di tali oggetti, le classi di riga e colonna dispongono di una proprietà <xref:System.Windows.Forms.DataGridViewBand.HasDefaultCellStyle%2A> che è possibile consultare per appurare se la proprietà <xref:System.Windows.Forms.DataGridViewBand.DefaultCellStyle%2A> è stata impostata.  Anche le classi di cella dispongono di una proprietà <xref:System.Windows.Forms.DataGridViewCell.HasStyle%2A> che indica se la proprietà <xref:System.Windows.Forms.DataGridViewCell.Style%2A> è stata impostata.  
  
 A ciascuna proprietà di stile corrisponde un evento *NomeProprietà*`Changed` nel controllo <xref:System.Windows.Forms.DataGridView>.  Per le proprietà di riga, colonna e cella il nome dell'evento inizia per "`Row`", "`Column`" o "`Cell`", ad esempio <xref:System.Windows.Forms.DataGridView.RowDefaultCellStyleChanged>.  Ogni evento si verifica quando la proprietà di stile corrispondente è impostata su un oggetto <xref:System.Windows.Forms.DataGridViewCellStyle> diverso.  Gli eventi non si verificano quando si recupera un oggetto <xref:System.Windows.Forms.DataGridViewCellStyle> da una proprietà di stile e se ne modificano i valori della proprietà.  Per rispondere alle modifiche apportate agli oggetti dello stile di celle stessi, gestire l'evento <xref:System.Windows.Forms.DataGridView.CellStyleContentChanged>.  
  
## Ereditarietà dello stile  
 Ogni classe <xref:System.Windows.Forms.DataGridViewCell> ottiene il relativo aspetto dalla proprietà <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A>.  L'oggetto <xref:System.Windows.Forms.DataGridViewCellStyle> restituito da tale proprietà eredita i valori da una gerarchia di proprietà di tipo <xref:System.Windows.Forms.DataGridViewCellStyle>.  Tali proprietà sono elencate di seguito nell'ordine in cui la proprietà <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A> di celle diverse da quelle di intestazione ottiene i valori.  
  
1.  <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=fullName>  
  
2.  <xref:System.Windows.Forms.DataGridViewRow.DefaultCellStyle%2A?displayProperty=fullName>  
  
3.  <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=fullName> \(solo per celle in righe con numeri di indice dispari\)  
  
4.  <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=fullName>  
  
5.  <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A?displayProperty=fullName>  
  
6.  <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>  
  
 Relativamente a celle di intestazione di riga e colonna, la proprietà <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A> eredita i valori dall'elenco di proprietà origine riportato di seguito, nell'ordine indicato.  
  
1.  <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=fullName>  
  
2.  <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A?displayProperty=fullName> oppure <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A?displayProperty=fullName>  
  
3.  <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>  
  
 Nel diagramma che segue viene illustrato questo processo.  
  
 ![Proprietà di tipo DataGridViewCellStyle](../../../../docs/framework/winforms/controls/media/datagridviewcells1.png "DataGridViewCells1")  
  
 È inoltre possibile accedere agli stili ereditati da specifiche righe e colonne.  La proprietà <xref:System.Windows.Forms.DataGridViewColumn.InheritedStyle%2A> di colonna eredita i valori dalle proprietà seguenti.  
  
1.  <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A?displayProperty=fullName>  
  
2.  <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>  
  
 La proprietà <xref:System.Windows.Forms.DataGridViewRow.InheritedStyle%2A> di riga eredita i valori dalle proprietà seguenti.  
  
1.  <xref:System.Windows.Forms.DataGridViewRow.DefaultCellStyle%2A?displayProperty=fullName>  
  
2.  <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=fullName> \(solo per celle in righe con numeri di indice dispari\)  
  
3.  <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=fullName>  
  
4.  <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>  
  
 Per ogni proprietà di un oggetto <xref:System.Windows.Forms.DataGridViewCellStyle> restituito da una proprietà `InheritedStyle`, il valore è ottenuto dal primo stile di cella nell'elenco appropriato la cui proprietà corrispondente è impostata su un valore diverso da quelli predefiniti della classe <xref:System.Windows.Forms.DataGridViewCellStyle>.  
  
 Nella tabella riportata di seguito viene illustrato come il valore della proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A> per una cella di esempio venga ereditato dalla colonna in cui la cella è contenuta.  
  
|Proprietà di tipo `DataGridViewCellStyle`|Valore di esempio di `ForeColor` per l'oggetto recuperato|  
|-----------------------------------------------|---------------------------------------------------------------|  
|<xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=fullName>|<xref:System.Drawing.Color.Empty?displayProperty=fullName>|  
|<xref:System.Windows.Forms.DataGridViewRow.DefaultCellStyle%2A?displayProperty=fullName>|<xref:System.Drawing.Color.Red%2A?displayProperty=fullName>|  
|<xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=fullName>|<xref:System.Drawing.Color.Empty?displayProperty=fullName>|  
|<xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=fullName>|<xref:System.Drawing.Color.Empty?displayProperty=fullName>|  
|<xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A?displayProperty=fullName>|<xref:System.Drawing.Color.DarkBlue%2A?displayProperty=fullName>|  
|<xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>|<xref:System.Drawing.Color.Black%2A?displayProperty=fullName>|  
  
 In tal caso il valore <xref:System.Drawing.Color.Red%2A?displayProperty=fullName> che deriva dalla riga della cella è il primo valore effettivo nell'elenco.  Diventa il valore della proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A> della proprietà <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A> della cella.  
  
 Nel diagramma seguente viene illustrato il modo in cui proprietà <xref:System.Windows.Forms.DataGridViewCellStyle> diverse possono ereditare i rispettivi valori da origini diverse.  
  
 ![Eredità del valore della proprietà DataGridView](../../../../docs/framework/winforms/controls/media/datagridviewcells2.png "DataGridViewCells2")  
  
 L'ereditarietà dello stile consente di fornire stili appropriati per l'intero controllo senza dover specificare le stesse informazioni in più punti.  
  
 Nonostante l'ereditarietà dello stile valga anche per le celle di intestazione, gli oggetti restituiti dalle proprietà <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A> e <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A> del controllo <xref:System.Windows.Forms.DataGridView> dispongono di valori di proprietà iniziali che eseguono l'override di quelli dell'oggetto restituito dalla proprietà <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A>.  Se si desidera che le proprietà impostate per l'oggetto restituito dalla proprietà <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A> vengano applicate alle intestazioni di riga e colonna, è necessario impostare le proprietà corrispondenti degli oggetti restituiti dalle proprietà <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A> e <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A> sui valori predefiniti indicati per la classe <xref:System.Windows.Forms.DataGridViewCellStyle>.  
  
> [!NOTE]
>  Se sono attivati stili di visualizzazione, alle intestazioni di riga e colonna \(ad eccezione della proprietà <xref:System.Windows.Forms.DataGridView.TopLeftHeaderCell%2A>\) viene applicato automaticamente lo stile del tema corrente e viene eseguito l'override di eventuali stili specificati da tali proprietà.  
  
 I tipi <xref:System.Windows.Forms.DataGridViewButtonColumn>, <xref:System.Windows.Forms.DataGridViewImageColumn> e <xref:System.Windows.Forms.DataGridViewCheckBoxColumn> inizializzano inoltre alcuni valori dell'oggetto restituito dalla proprietà <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A> di colonna.  Per ulteriori informazioni, vedere la documentazione di riferimento relativa a tali tipi.  
  
## Impostazione dinamica degli stili  
 Per personalizzare gli stili di celle con valori particolari, implementare un gestore per l'evento <xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=fullName>.  I gestori di tale evento ricevono un argomento di tipo <xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs>.  Tale oggetto contiene proprietà che consentono di determinare il valore della cella formattata unitamente alla sua posizione nel controllo <xref:System.Windows.Forms.DataGridView>.  L'oggetto contiene inoltre una proprietà <xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs.CellStyle%2A> inizializzata sul valore della proprietà <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A> della cella sottoposta a formattazione.  È possibile modificare le proprietà dello stile delle celle per specificare informazioni relative allo stile appropriate per il valore e la posizione della cella.  
  
> [!NOTE]
>  Gli eventi <xref:System.Windows.Forms.DataGridView.RowPrePaint> e <xref:System.Windows.Forms.DataGridView.RowPostPaint> ricevono inoltre un oggetto <xref:System.Windows.Forms.DataGridViewCellStyle> nei dati di evento ma nel loro caso si tratta di una copia della proprietà <xref:System.Windows.Forms.DataGridViewRow.InheritedStyle%2A> della riga in modalità di sola lettura e le modifiche apportate all'oggetto non incidono sul controllo.  
  
 È inoltre possibile modificare dinamicamente gli stili di singole celle in risposta a eventi quali <xref:System.Windows.Forms.DataGridView.CellMouseEnter?displayProperty=fullName> e <xref:System.Windows.Forms.DataGridView.CellMouseLeave>.  In un gestore dell'evento <xref:System.Windows.Forms.DataGridView.CellMouseEnter>, ad esempio, è possibile memorizzare il valore corrente del colore di sfondo della cella \(recuperato dalla proprietà <xref:System.Windows.Forms.DataGridViewCell.Style%2A> della cella\) e impostarlo su un nuovo colore con cui la cella viene evidenziata quando il mouse si posiziona su di essa.  È in seguito possibile ripristinare il valore originale del colore di sfondo in un gestore dell'evento <xref:System.Windows.Forms.DataGridView.CellMouseLeave>.  
  
> [!NOTE]
>  L'inserimento nella cache dei valori memorizzati nella proprietà <xref:System.Windows.Forms.DataGridViewCell.Style%2A> della cella è un'operazione importante indipendentemente dall'impostazione di un valore di stile particolare.  Se si sostituisce temporaneamente un'impostazione dello stile, il ripristino dello stato "non impostato" originale garantisce che la cella ritorni a ereditare l'impostazione dello stile da un livello superiore.  Se è necessario determinare lo stile effettivo attivo per una cella e non è importante sapere se lo stile è ereditato, utilizzare la proprietà <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A> della cella.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewCellStyle>   
 <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewBand.InheritedStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewRow.InheritedStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.InheritedStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewBand.DefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.CellStyleContentChanged?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowPrePaint?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowPostPaint?displayProperty=fullName>   
 [Formattazione e stile di base nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)   
 [Procedura: impostare stili di cella predefiniti per il controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)   
 [Formattazione di dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/data-formatting-in-the-windows-forms-datagridview-control.md)