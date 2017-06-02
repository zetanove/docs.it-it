---
title: "Modalit&#224; di visualizzazione dati nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "dati [Windows Form], modalità di visualizzazione"
  - "griglie dei dati, modalità di visualizzazione"
  - "DataGridView (controllo) [Windows Form], modalità di visualizzazione"
ms.assetid: 9755a030-3f3f-4705-a661-ba5a48a81875
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Modalit&#224; di visualizzazione dati nel controllo DataGridView di Windows Form
Il controllo <xref:System.Windows.Forms.DataGridView> consente di visualizzare i dati in tre modalità distinte: associata, non associata e virtuale.  Scegliere la modalità più adatta alle proprie esigenze.  
  
## Modalità non associata  
 La modalità non associata è adatta per visualizzare piccole quantità di dati gestite a livello di codice.  Il controllo <xref:System.Windows.Forms.DataGridView> non viene collegato direttamente a un'origine dati, come nella modalità associata,  e deve essere compilato manualmente, in genere utilizzando il metodo <xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A?displayProperty=fullName>.  
  
 La modalità non associata può risultare particolarmente utile per dati statici e di sola lettura oppure quando si utilizza del codice proprio per interagire con un archivio dati esterno.  Per l'interazione degli utenti con un'origine dati esterna, tuttavia, si utilizza in genere la modalità associata.  
  
 Per un esempio in cui viene utilizzato un controllo <xref:System.Windows.Forms.DataGridView> non associato di sola lettura, vedere [Procedura: creare un controllo DataGridView di Windows Form non associato](../../../../docs/framework/winforms/controls/how-to-create-an-unbound-windows-forms-datagridview-control.md).  
  
## Modalità associata  
 La modalità associata è adatta per gestire i dati mediante interazione automatica con l'archivio dati.  È possibile collegare il controllo <xref:System.Windows.Forms.DataGridView> direttamente alla relativa origine dati mediante l'impostazione della proprietà <xref:System.Windows.Forms.DataGridView.DataSource%2A>.  Quando il controllo è associato ai dati, le righe di dati vengono inserite ed estratte senza che sia richiesta una gestione esplicita.  Se la proprietà <xref:System.Windows.Forms.DataGridView.AutoGenerateColumns%2A> è `true`, per ogni colonna dell'origine dati viene creata una colonna corrispondente nel controllo.  Se si preferisce creare le proprie colonne, impostare la proprietà su `false` e utilizzare la proprietà <xref:System.Windows.Forms.DataGridViewColumn.DataPropertyName%2A> per associare ciascuna colonna al momento della configurazione.  Ciò risulta utile se si desidera utilizzare un tipo di colonna diverso da quelli generati per impostazione predefinita.  Per ulteriori informazioni, vedere [Tipi di colonna nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/column-types-in-the-windows-forms-datagridview-control.md).  
  
 Per un esempio in cui viene utilizzato un controllo <xref:System.Windows.Forms.DataGridView> associato, vedere [Procedura dettagliata: convalida di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/walkthrough-validating-data-in-the-windows-forms-datagridview-control.md).  
  
 È anche possibile aggiungere colonne non associate a un controllo <xref:System.Windows.Forms.DataGridView> in modalità associata.  Ciò risulta utile per visualizzare una colonna di pulsanti o collegamenti che consentono di effettuare azioni su righe specifiche  oppure per visualizzare colonne con valori calcolati provenienti da colonne associate.  È possibile popolare i valori delle celle per le colonne calcolate in un gestore per l'evento <xref:System.Windows.Forms.DataGridView.CellFormatting>.  Se si utilizza un <xref:System.Data.DataSet> o <xref:System.Data.DataTable> come origine dati, tuttavia, potrebbe essere preferibile utilizzare la proprietà <xref:System.Data.DataColumn.Expression%2A?displayProperty=fullName> per creare una colonna calcolata.  In questo caso, il controllo <xref:System.Windows.Forms.DataGridView> tratterà la colonna calcolata esattamente come qualsiasi altra colonna dell'origine dati.  
  
 L'ordinamento in base a colonne non associate in modalità associata non è supportato.  Se in modalità associata si crea una colonna non associata che contiene valori modificabili dall'utente, è necessario implementare la modalità virtuale per la gestione di tali valori quando il controllo viene ordinato in base a una colonna associata.  
  
## Modalità virtuale  
 In modalità virtuale è possibile implementare le proprie operazioni di gestione dei dati.  Ciò è necessario per gestire i valori di colonne non associate in modalità associata quando il controllo viene ordinato in base a colonne associate.  L'impiego principale della modalità virtuale, tuttavia, è l'ottimizzazione delle prestazioni in caso di interazione con grandi quantità di dati.  
  
 Il controllo <xref:System.Windows.Forms.DataGridView> viene collegato a una cache che deve essere gestita e in cui l'inserimento e l'estrazione delle righe di dati devono essere controllati a livello di codice.  Per mantenere ridotte le dimensioni della memoria, la cache deve avere dimensioni corrispondenti al numero di righe attualmente visualizzate.  Quando l'utente scorre le righe e ne visualizza di nuove, il codice richiede nuovi dati dalla cache ed eventualmente elimina i dati obsoleti dalla memoria.  
  
 Se si implementa la modalità virtuale, è necessario tenere traccia di quando è necessaria una nuova riga nel modello dati e di quando eseguire il rollback per l'aggiunta della nuova riga.  L'implementazione esatta di questa funzionalità dipende dall'implementazione del modello dati e dalla relativa semantica delle transazioni, ad esempio se l'ambito del commit è a livello di cella o di riga.  
  
 Per ulteriori informazioni sulla modalità virtuale, vedere [Modo virtuale nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/virtual-mode-in-the-windows-forms-datagridview-control.md).  Per un esempio di utilizzo degli eventi in modalità virtuale, vedere [Procedura dettagliata: implementazione della modalità virtuale nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.DataSource%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.BindingSource>   
 <xref:System.Windows.Forms.DataGridViewColumn.DataPropertyName%2A?displayProperty=fullName>   
 [Visualizzazione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)   
 [Tipi di colonna nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/column-types-in-the-windows-forms-datagridview-control.md)   
 [Procedura dettagliata: creazione di un controllo DataGridView Windows Form non associato](../../../../docs/framework/winforms/controls/walkthrough-creating-an-unbound-windows-forms-datagridview-control.md)   
 [Procedura: associare dati al controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/how-to-bind-data-to-the-windows-forms-datagridview-control.md)   
 [Modo virtuale nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/virtual-mode-in-the-windows-forms-datagridview-control.md)   
 [Procedura dettagliata: implementazione della modalità virtuale nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md)