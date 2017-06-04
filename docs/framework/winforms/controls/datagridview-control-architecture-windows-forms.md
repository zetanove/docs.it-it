---
title: "Architettura del controllo DataGridView (Windows Form) | Microsoft Docs"
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
  - "DataGridView (controllo) [Windows Form], architettura"
ms.assetid: 1c6cabf0-02ee-4bbc-9574-b54bb7f5b19e
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Architettura del controllo DataGridView (Windows Form)
Il controllo <xref:System.Windows.Forms.DataGridView> e le relative classi sono progettati per costituire un sistema flessibile ed estendibile per la visualizzazione e la modifica di dati in formato tabulare.  Queste classi sono contenute tutte nello spazio dei nomi <xref:System.Windows.Forms?displayProperty=fullName> e sono contrassegnate con il prefisso "DataGridView".  
  
## Elementi dell'architettura  
 Le principali classi correlate <xref:System.Windows.Forms.DataGridView> derivano da <xref:System.Windows.Forms.DataGridViewElement>.  Nel modello a oggetti riportato di seguito viene illustrata la gerarchia di ereditarietà di <xref:System.Windows.Forms.DataGridViewElement>.  
  
 ![Modello a oggetti DataGridViewElement](../../../../docs/framework/winforms/controls/media/datagridviewelement.png "DataGridViewElement")  
Modello a oggetti DataGridViewElement  
  
 La classe <xref:System.Windows.Forms.DataGridViewElement> fornisce un riferimento al controllo padre <xref:System.Windows.Forms.DataGridView> e dispone di una proprietà <xref:System.Windows.Forms.DataGridViewElement.State%2A> che contiene un valore che rappresenta una combinazione dei valori dell'enumerazione <xref:System.Windows.Forms.DataGridViewElementStates>.  
  
 Nelle sezioni che seguono le classi correlate <xref:System.Windows.Forms.DataGridView> vengono illustrate in modo dettagliato.  
  
### DataGridViewElementStates  
 L'enumerazione <xref:System.Windows.Forms.DataGridViewElementStates> contiene i valori indicati di seguito.  
  
-   <xref:System.Windows.Forms.DataGridViewElementStates>  
  
-   <xref:System.Windows.Forms.DataGridViewElementStates>  
  
-   <xref:System.Windows.Forms.DataGridViewElementStates>  
  
-   <xref:System.Windows.Forms.DataGridViewElementStates>  
  
-   <xref:System.Windows.Forms.DataGridViewElementStates>  
  
-   <xref:System.Windows.Forms.DataGridViewElementStates>  
  
-   <xref:System.Windows.Forms.DataGridViewElementStates>  
  
 I valori di questa enumerazione possono essere combinati con operatori logici bit per bit, per cui la proprietà <xref:System.Windows.Forms.DataGridViewElement.State%2A> è in grado di esprimere più di uno stato alla volta.  Ad esempio, la classe <xref:System.Windows.Forms.DataGridViewElement> può essere contemporaneamente nello stato <xref:System.Windows.Forms.DataGridViewElementStates>, <xref:System.Windows.Forms.DataGridViewElementStates> e <xref:System.Windows.Forms.DataGridViewElementStates>.  
  
### Celle e bande  
 Il controllo <xref:System.Windows.Forms.DataGridView> comprende due tipi fondamentali di oggetti: celle e bande.  Tutte le celle derivano dalla classe base <xref:System.Windows.Forms.DataGridViewCell>.  I due tipi di bande, <xref:System.Windows.Forms.DataGridViewColumn> e <xref:System.Windows.Forms.DataGridViewRow>, derivano entrambi dalla classe base <xref:System.Windows.Forms.DataGridViewBand>.  
  
 Il controllo <xref:System.Windows.Forms.DataGridView> interagisce con diverse classi, ma quelle utilizzate più di frequente sono <xref:System.Windows.Forms.DataGridViewCell>, <xref:System.Windows.Forms.DataGridViewColumn> e <xref:System.Windows.Forms.DataGridViewRow>.  
  
### DataGridViewCell  
 La cella è l'unità di base di interazione per la classe <xref:System.Windows.Forms.DataGridView>.  La visualizzazione si basa sulle celle e l'immissione dei dati viene spesso eseguita mediante le celle.  È possibile accedere alle celle utilizzando la raccolta <xref:System.Windows.Forms.DataGridViewRow.Cells%2A> della classe <xref:System.Windows.Forms.DataGridViewRow> e accedere alle celle selezionate utilizzando la raccolta <xref:System.Windows.Forms.DataGridView.SelectedCells%2A> del controllo <xref:System.Windows.Forms.DataGridView>.  Nel modello a oggetti riportato di seguito vengono illustrati tale utilizzo e la gerarchia di ereditarietà di <xref:System.Windows.Forms.DataGridViewCell>.  
  
 ![Modello a oggetti DataGridViewCell](../../../../docs/framework/winforms/controls/media/datagridviewcell.png "DataGridViewCell")  
Modello a oggetti DataGridViewCell  
  
 Il tipo <xref:System.Windows.Forms.DataGridViewCell> è una classe base astratta, da cui derivano tutti i tipi di cella.  <xref:System.Windows.Forms.DataGridViewCell> e i tipi derivati non sono controlli Windows Form, ma alcuni di essi contengono controlli Windows Form.  Tutte le funzionalità di modifica supportate da una cella sono in genere gestite da un controllo inserito.  
  
 Gli oggetti <xref:System.Windows.Forms.DataGridViewCell> non controllano le funzionalità relative all'aspetto e al disegno alla stessa maniera dei controlli Windows Form.  Al contrario, il controllo <xref:System.Windows.Forms.DataGridView> determina l'aspetto dei relativi oggetti <xref:System.Windows.Forms.DataGridViewCell>.  È possibile modificare in modo significativo l'aspetto e il comportamento delle celle interagendo con le proprietà e gli eventi del controllo <xref:System.Windows.Forms.DataGridView>.  Se i requisiti di personalizzazione necessari vanno oltre le capacità del controllo <xref:System.Windows.Forms.DataGridView>, è possibile implementare una classe personalizzata derivata da <xref:System.Windows.Forms.DataGridViewCell> o da una delle classi figlie.  
  
 Nell'elenco riportato di seguito sono riportate le classi che derivano da <xref:System.Windows.Forms.DataGridViewCell>.  
  
-   <xref:System.Windows.Forms.DataGridViewTextBoxCell>  
  
-   <xref:System.Windows.Forms.DataGridViewButtonCell>  
  
-   <xref:System.Windows.Forms.DataGridViewLinkCell>  
  
-   <xref:System.Windows.Forms.DataGridViewCheckBoxCell>  
  
-   <xref:System.Windows.Forms.DataGridViewComboBoxCell>  
  
-   <xref:System.Windows.Forms.DataGridViewImageCell>  
  
-   <xref:System.Windows.Forms.DataGridViewHeaderCell>  
  
-   <xref:System.Windows.Forms.DataGridViewRowHeaderCell>  
  
-   <xref:System.Windows.Forms.DataGridViewColumnHeaderCell>  
  
-   <xref:System.Windows.Forms.DataGridViewTopLeftHeaderCell>  
  
-   Tipi di celle personalizzate  
  
### DataGridViewColumn  
 Lo schema dell'archivio dati collegato del controllo <xref:System.Windows.Forms.DataGridView> è espresso nelle colonne del controllo <xref:System.Windows.Forms.DataGridView>.  È possibile accedere alle colonne del controllo <xref:System.Windows.Forms.DataGridView> utilizzando la raccolta <xref:System.Windows.Forms.DataGridView.Columns%2A>.  È possibile accedere alle colonne selezionate utilizzando la raccolta <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A>.  Nel modello a oggetti riportato di seguito vengono illustrati tale utilizzo e la gerarchia di ereditarietà di <xref:System.Windows.Forms.DataGridViewColumn>.  
  
 ![Modello a oggetti DataGridViewColumn](../../../../docs/framework/winforms/controls/media/datagridviewcolumn.png "DataGridViewColumn")  
Modello a oggetti DataGridViewColumn  
  
 Per alcuni dei tipi di celle principali sono presenti tipi di colonne corrispondenti,  derivate dalla classe base <xref:System.Windows.Forms.DataGridViewColumn>.  
  
 Nell'elenco seguente sono riportate le classi che derivano da <xref:System.Windows.Forms.DataGridViewColumn>.  
  
-   <xref:System.Windows.Forms.DataGridViewButtonColumn>  
  
-   <xref:System.Windows.Forms.DataGridViewCheckBoxColumn>  
  
-   <xref:System.Windows.Forms.DataGridViewComboBoxColumn>  
  
-   <xref:System.Windows.Forms.DataGridViewImageColumn>  
  
-   <xref:System.Windows.Forms.DataGridViewTextBoxColumn>  
  
-   <xref:System.Windows.Forms.DataGridViewLinkColumn>  
  
-   Tipi di colonne personalizzati  
  
### Controlli di modifica DataGridView  
 Per le celle che supportano funzionalità di modifica avanzate viene in genere utilizzato un controllo inserito derivato da un controllo Windows Form.  Questi controlli implementano anche l'interfaccia <xref:System.Windows.Forms.IDataGridViewEditingControl>.  Nel modello a oggetti riportato di seguito viene illustrato l'utilizzo di questi controlli.  
  
 ![Modello a oggetti del controllo di modifica DataGridView](../../../../docs/framework/winforms/controls/media/datagridviewediting.png "DataGridViewEditing")  
Modello a oggetti del controllo di modifica DataGridView  
  
 I controlli di modifica riportati di seguito vengono forniti con il controllo <xref:System.Windows.Forms.DataGridView>.  
  
-   <xref:System.Windows.Forms.DataGridViewComboBoxEditingControl>  
  
-   <xref:System.Windows.Forms.DataGridViewTextBoxEditingControl>  
  
 Per informazioni sulla creazione di controlli di modifica personalizzati, vedere [Procedura: inserire controlli in celle del controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-host-controls-in-windows-forms-datagridview-cells.md).  
  
 Nella tabella riportata di seguito viene illustrata la relazione tra i tipi di celle, i tipi di colonne e i controlli di modifica.  
  
|Tipo di cella|Controllo inserito|Tipo di colonna|  
|-------------------|------------------------|---------------------|  
|<xref:System.Windows.Forms.DataGridViewButtonCell>|n\/d|<xref:System.Windows.Forms.DataGridViewButtonColumn>|  
|<xref:System.Windows.Forms.DataGridViewCheckBoxCell>|n\/d|<xref:System.Windows.Forms.DataGridViewCheckBoxColumn>|  
|<xref:System.Windows.Forms.DataGridViewComboBoxCell>|<xref:System.Windows.Forms.DataGridViewComboBoxEditingControl>|<xref:System.Windows.Forms.DataGridViewComboBoxColumn>|  
|<xref:System.Windows.Forms.DataGridViewImageCell>|n\/d|<xref:System.Windows.Forms.DataGridViewImageColumn>|  
|<xref:System.Windows.Forms.DataGridViewLinkCell>|n\/d|<xref:System.Windows.Forms.DataGridViewLinkColumn>|  
|<xref:System.Windows.Forms.DataGridViewTextBoxCell>|<xref:System.Windows.Forms.DataGridViewTextBoxEditingControl>|<xref:System.Windows.Forms.DataGridViewTextBoxColumn>|  
  
### DataGridViewRow  
 La classe <xref:System.Windows.Forms.DataGridViewRow> consente la visualizzazione di campi di dati di un record dell'archivio dati a cui il controllo <xref:System.Windows.Forms.DataGridView> è collegato.  È possibile accedere alle righe del controllo <xref:System.Windows.Forms.DataGridView> utilizzando la raccolta <xref:System.Windows.Forms.DataGridView.Rows%2A>.  È possibile accedere alle righe selezionate utilizzando la raccolta <xref:System.Windows.Forms.DataGridView.SelectedRows%2A>.  Nel modello a oggetti riportato di seguito vengono illustrati tale utilizzo e la gerarchia di ereditarietà di <xref:System.Windows.Forms.DataGridViewRow>.  
  
 ![Modello a oggetti DataGridViewRow](../../../../docs/framework/winforms/controls/media/datagridviewrow.png "DataGridViewRow")  
Modello a oggetti DataGridViewRow  
  
 È possibile derivare tipi personalizzati dalla classe <xref:System.Windows.Forms.DataGridViewRow>, anche se in genere non è necessario.  Il controllo <xref:System.Windows.Forms.DataGridView> dispone di diversi eventi relativi alle righe e di proprietà per la personalizzazione del comportamento degli oggetti <xref:System.Windows.Forms.DataGridViewRow>.  
  
 Se si attiva la proprietà <xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A> del controllo <xref:System.Windows.Forms.DataGridView>, come ultima riga verrà visualizzata una riga speciale per l'aggiunta di nuove righe.  Questa riga fa parte della raccolta <xref:System.Windows.Forms.DataGridView.Rows%2A>, ma dispone di funzionalità speciali per le quali potrebbe essere necessaria particolare attenzione.  Per ulteriori informazioni, vedere [Utilizzo della riga per i nuovi record del controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/using-the-row-for-new-records-in-the-windows-forms-datagridview-control.md).  
  
## Vedere anche  
 [Cenni preliminari sul controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-overview-windows-forms.md)   
 [Personalizzazione del controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/customizing-the-windows-forms-datagridview-control.md)   
 [Utilizzo della riga per i nuovi record del controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/using-the-row-for-new-records-in-the-windows-forms-datagridview-control.md)