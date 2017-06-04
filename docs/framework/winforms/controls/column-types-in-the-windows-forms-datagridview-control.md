---
title: "Tipi di colonna nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "colonne [Windows Form], tipi"
  - "griglie dei dati, colonne"
  - "DataGridView (controllo) [Windows Form], tipi di colonna"
ms.assetid: f0a0a9f1-8757-4bfd-891f-d7d12870dbed
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Tipi di colonna nel controllo DataGridView di Windows Form
Il controllo <xref:System.Windows.Forms.DataGridView> utilizza diversi tipi di colonna per visualizzare le informazioni e consentire la modifica o l'aggiunta di informazioni.  
  
 Quando si associa un controllo <xref:System.Windows.Forms.DataGridView> e si imposta la proprietà <xref:System.Windows.Forms.DataGridView.AutoGenerateColumns%2A> su `true`, le colonne vengono generate automaticamente in base ai tipi di colonna predefiniti appropriati per i tipi di dati contenuti nell'origine dati associata.  
  
 È inoltre possibile creare istanze di qualsiasi classe di colonne e aggiungerle alla raccolta restituita dalla proprietà <xref:System.Windows.Forms.DataGridView.Columns%2A>.  È possibile creare queste istanze per utilizzarle come colonne non associate oppure è possibile associarle manualmente.  Le colonne associate manualmente sono utili, ad esempio, quando si desidera sostituire una colonna generata automaticamente di un tipo con una colonna di un altro tipo.  
  
 Nella tabella seguente vengono descritte le varie classi di colonne disponibili nel controllo <xref:System.Windows.Forms.DataGridView>.  
  
|Classe|Descrizione|  
|------------|-----------------|  
|<xref:System.Windows.Forms.DataGridViewTextBoxColumn>|Utilizzata con valori basati su testo.  Generata automaticamente quando si esegue l'associazione a numeri e stringhe.|  
|<xref:System.Windows.Forms.DataGridViewCheckBoxColumn>|Utilizzata con i valori <xref:System.Boolean> e <xref:System.Windows.Forms.CheckState>.  Generata automaticamente quando si esegue l'associazione a valori di questi tipi.|  
|<xref:System.Windows.Forms.DataGridViewImageColumn>|Utilizzata per visualizzare le immagini.  Generata automaticamente quando si esegue l'associazione a matrici di byte, oggetti <xref:System.Drawing.Image> oppure oggetti <xref:System.Drawing.Icon>.|  
|<xref:System.Windows.Forms.DataGridViewButtonColumn>|Utilizzata per visualizzare i pulsanti nelle celle.  Generata non automaticamente quando si esegue l'associazione.  Usata normalmente come colonna non associata.|  
|<xref:System.Windows.Forms.DataGridViewComboBoxColumn>|Utilizzata per visualizzare elenchi a discesa nelle celle.  Generata non automaticamente quando si esegue l'associazione.  Solitamente associata ai dati manualmente.|  
|<xref:System.Windows.Forms.DataGridViewLinkColumn>|Utilizzata per visualizzare i collegamenti nelle celle.  Generata non automaticamente quando si esegue l'associazione.  Solitamente associata ai dati manualmente.|  
|Tipo di colonna personalizzato|È possibile creare una classe di colonne personalizzate mediante l'eredità della classe <xref:System.Windows.Forms.DataGridViewColumn> o di qualsiasi classe da essa derivata per personalizzare l'aspetto, il comportamento o i controlli contenuti.  Per ulteriori informazioni, vedere [Procedura: personalizzare celle e colonne nel controllo DataGridView di Windows Form estendendone il comportamento e l'aspetto](../../../../docs/framework/winforms/controls/customize-cells-and-columns-in-the-datagrid-by-extending-behavior.md)|  
  
 Questi tipi di colonna sono descritti nei dettagli nelle sezioni seguenti.  
  
## DataGridViewTextBoxColumn  
 <xref:System.Windows.Forms.DataGridViewTextBoxColumn> è un tipo di colonna generica da utilizzare con i valori basati su testo quali numeri e stringhe.  Nella modalità di modifica, nella cella attiva, è visualizzato un controllo <xref:System.Windows.Forms.TextBox> che consente di modificare il valore della cella.  
  
 I valori delle celle vengono convertiti automaticamente in stringhe per la visualizzazione.  I valori immessi o modificati dall'utente vengono automaticamente analizzati per creare un valore della cella del tipo di dati appropriato.  È possibile personalizzare queste conversioni mediante la gestione degli eventi <xref:System.Windows.Forms.DataGridView.CellFormatting> e <xref:System.Windows.Forms.DataGridView.CellParsing> del controllo <xref:System.Windows.Forms.DataGridView>.  
  
 Il tipo di dati del valore della cella di una colonna è specificato nella proprietà <xref:System.Windows.Forms.DataGridViewColumn.ValueType%2A> della colonna.  
  
## DataGridViewCheckBoxColumn  
 <xref:System.Windows.Forms.DataGridViewCheckBoxColumn> viene utilizzato con i valori <xref:System.Boolean> e <xref:System.Windows.Forms.CheckState>.  I valori <xref:System.Boolean> vengono visualizzati sotto forma di caselle di controllo a due o tre stati a seconda del valore della proprietà <xref:System.Windows.Forms.DataGridViewCheckBoxColumn.ThreeState%2A>.  Quando la colonna è associata ai valori <xref:System.Windows.Forms.CheckState>, il valore della proprietà <xref:System.Windows.Forms.DataGridViewCheckBoxColumn.ThreeState%2A> è `true` per impostazione predefinita.  
  
 Normalmente i valori delle celle delle caselle di controllo vengono utilizzati per l'archiviazione, come gli altri dati, o per l'esecuzione di operazioni di massa.  Se si desidera rispondere immediatamente quando l'utente fa clic su una cella di casella di controllo, è possibile gestire l'evento <xref:System.Windows.Forms.DataGridView.CellClick>, che tuttavia si verifica prima il valore della cella venga aggiornato.  Se è necessario disporre del nuovo valore al momento del clic, è possibile calcolare il valore previsto in base al valore corrente.  In alternativa, è possibile eseguire immediatamente il commit della modifica e quindi gestire l'evento <xref:System.Windows.Forms.DataGridView.CellValueChanged> per rispondere a tale modifica.  Per eseguire il commit della modifica quando viene fatto clic sulla cella, è necessario gestire l'evento <xref:System.Windows.Forms.DataGridView.CurrentCellDirtyStateChanged>.  Nel gestore, se la cella corrente è una cella di casella di testo, richiamare il metodo <xref:System.Windows.Forms.DataGridView.CommitEdit%2A> e passare al valore <xref:System.Windows.Forms.DataGridViewDataErrorContexts>.  
  
## DataGridViewImageColumn  
 La classe <xref:System.Windows.Forms.DataGridViewImageColumn> consente di visualizzare le immagini.  Le colonne di immagini possono essere compilate automaticamente da un'origine dati, manualmente per le colonne non associate o dinamicamente in un gestore per l'evento <xref:System.Windows.Forms.DataGridView.CellFormatting>.  
  
 La compilazione automatica di una colonna di immagini da un'origine dati funziona con matrici di byte in una varietà di formati di immagine, compresi tutti i formati supportati dalla classe <xref:System.Drawing.Image> e il formato OLE Picture utilizzato da Microsoft® Access e dal database di esempio Northwind.  
  
 La compilazione manuale di una colonna di immagini è utile quando si desidera fornire la funzionalità di una classe <xref:System.Windows.Forms.DataGridViewButtonColumn>, ma con un aspetto personalizzato.  È possibile gestire l'evento <xref:System.Windows.Forms.DataGridView.CellClick?displayProperty=fullName> per rispondere alle selezioni nella cella di un'immagine.  
  
 La compilazione delle celle di una colonna di immagini in un gestore per l'evento <xref:System.Windows.Forms.DataGridView.CellFormatting> è utile quando si desidera fornire immagini per i valori calcolati o i valori nei formati non di immagine.  Ad esempio, è possibile disporre di una colonna "Rischio" con valori stringa quali `"high"`, `"middle"` e `"low"` che si desidera visualizzare come icone.  In alternativa è possibile disporre di una colonna"Immagine" che contiene i percorsi delle immagini che devono essere caricate invece del contenuto binario delle immagini.  
  
## DataGridViewButtonColumn  
 La classe <xref:System.Windows.Forms.DataGridViewButtonColumn> consente di visualizzare una colonna di celle contenenti pulsanti.  Ciò è utile quando si desidera consentire agli utenti di eseguire facilmente operazioni con record particolari, ad esempio l'effettuazione di un ordine o la visualizzazione di record figlio in una finestra separata.  
  
 Le colonne di pulsanti non vengono generate automaticamente quando si esegue l'associazione ai dati di un controllo<xref:System.Windows.Forms.DataGridView>.  Per utilizzare le colonne di pulsanti, è necessario crearle manualmente e aggiungerle alla raccolta restituita dalla proprietà <xref:System.Windows.Forms.DataGridView.Columns%2A?displayProperty=fullName>.  
  
 È possibile rispondere alle selezioni nelle celle di pulsanti mediante la gestione dell'evento <xref:System.Windows.Forms.DataGridView.CellClick?displayProperty=fullName>.  
  
## DataGridViewComboBoxColumn  
 La classe <xref:System.Windows.Forms.DataGridViewComboBoxColumn> consente di visualizzare una colonna di celle che contengono le caselle di riepilogo a discesa.  Ciò è utile per l'immissione di dati nei campi che possono contenere solo determinati valori, ad esempio la colonna Category della tabella Products nel database di esempio Northwind.  
  
 È possibile compilare l'elenco a discesa utilizzato per tutte le celle allo stesso modo in cui si compilerebbe un elenco a discesa <xref:System.Windows.Forms.ComboBox>: manualmente tramite la raccolta restituita dalla proprietà <xref:System.Windows.Forms.DataGridViewComboBoxColumn.Items%2A> o mediante l'associazione a un'origine dati tramite le proprietà <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DataSource%2A>, <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DisplayMember%2A> e <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A>.  Per ulteriori informazioni, vedere [Controllo ComboBox](../../../../docs/framework/winforms/controls/combobox-control-windows-forms.md).  
  
 È possibile associare i valori effettivi delle celle all'origine dati utilizzata dal controllo <xref:System.Windows.Forms.DataGridView> mediante l'impostazione della proprietà <xref:System.Windows.Forms.DataGridViewColumn.DataPropertyName%2A> della classe <xref:System.Windows.Forms.DataGridViewComboBoxColumn?displayProperty=fullName>.  
  
 Le colonne di caselle combinate non vengono generate automaticamente quando si esegue l'associazione ai dati di un controllo<xref:System.Windows.Forms.DataGridView>.  Per utilizzare le colonne di caselle combinate, è necessario crearle manualmente e aggiungerle alla raccolta restituita dalla proprietà <xref:System.Windows.Forms.DataGridView.Columns%2A>.  
  
## DataGridViewLinkColumn  
 La classe <xref:System.Windows.Forms.DataGridViewLinkColumn> consente di visualizzare una colonna di celle contenenti collegamenti ipertestuali.  Ciò è utile per i valori URL nell'origine dati o come alternativa alla colonna di pulsanti per i comportamenti speciali quali l'apertura di una finestra con record figlio.  
  
 Le colonne di collegamenti non vengono generate automaticamente quando si esegue l'associazione ai dati di un controllo<xref:System.Windows.Forms.DataGridView>.  Per utilizzare le colonne di collegamenti, è necessario crearle manualmente e aggiungerle alla raccolta restituita dalla proprietà <xref:System.Windows.Forms.DataGridView.Columns%2A>.  
  
 È possibile rispondere alle selezioni dei collegamenti mediante la gestione dell'evento <xref:System.Windows.Forms.DataGridView.CellContentClick>.  Questo evento è diverso dagli eventi <xref:System.Windows.Forms.DataGridView.CellClick> e <xref:System.Windows.Forms.DataGridView.CellMouseClick>, che si verificano quando un utente fa clic in un punto qualsiasi di una cella.  
  
 La classe <xref:System.Windows.Forms.DataGridViewLinkColumn> fornisce diverse proprietà per la modifica dell'aspetto dei collegamenti prima, durante e dopo la selezione.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewColumn>   
 <xref:System.Windows.Forms.DataGridViewButtonColumn>   
 <xref:System.Windows.Forms.DataGridViewCheckBoxColumn>   
 <xref:System.Windows.Forms.DataGridViewComboBoxColumn>   
 <xref:System.Windows.Forms.DataGridViewImageColumn>   
 <xref:System.Windows.Forms.DataGridViewTextBoxColumn>   
 <xref:System.Windows.Forms.DataGridViewLinkColumn>   
 [Controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)   
 [Procedura: visualizzare immagini in celle del controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-display-images-in-cells-of-the-windows-forms-datagridview-control.md)   
 [Procedura: utilizzare le colonne di immagini nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-work-with-image-columns-in-the-windows-forms-datagridview-control.md)   
 [Personalizzazione del controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/customizing-the-windows-forms-datagridview-control.md)