---
title: "Procedura: creare una tabella di ricerca per un controllo ComboBox, ListBox o CheckedListBox Windows Form | Microsoft Docs"
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
  - "CheckedListBox (controllo) [Windows Form], creazione di tabelle di ricerca"
  - "caselle combinate, tabelle di ricerca"
  - "ComboBox (controllo) [Windows Form], tabella di ricerca"
  - "caselle di riepilogo, tabelle di ricerca"
  - "ListBox (controllo) [Windows Form], creazione di tabelle di ricerca"
  - "ListBox (controllo) [Windows Form], tabelle di ricerca"
  - "tabelle di ricerca"
  - "tabelle di ricerca, creazione per i controlli"
ms.assetid: 4ce35f12-1f4e-4317-92d1-af8686a8cfaa
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: creare una tabella di ricerca per un controllo ComboBox, ListBox o CheckedListBox Windows Form
Può risultare utile visualizzare i dati all'interno di un Windows Form in un formato facilmente riconoscibile dall'utente, ma memorizzare gli stessi dati in un formato che consenta una migliore gestione da parte del programma.  Ad esempio un form di ordinazione per generi alimentari può visualizzare le voci di menu ordinate in base al nome in una casella di riepilogo,  mentre la tabella dati per la registrazione dell'ordine può contenere i numeri univoci di identificazione corrispondenti a ogni piatto.  Nelle tabelle seguenti viene mostrato un esempio di memorizzazione e visualizzazione dei dati contenuti in un form di ordinazione per generi alimentari.  
  
### OrderDetailsTable  
  
|OrderID|ItemID|Quantità|  
|-------------|------------|--------------|  
|4085|12|1|  
|4086|13|3|  
  
### ItemTable  
  
|ID|Nome|  
|--------|----------|  
|12|Patate|  
|13|Pollo|  
  
 In questo scenario, in una tabella, OrderDetailsTable, sono memorizzate le informazioni relative alla visualizzazione e al salvataggio.  Per risparmiare spazio, però, la memorizzazione avviene in modo piuttosto criptico.  Nella seconda tabella, ItemTable, sono contenute informazioni concernenti esclusivamente l'aspetto, relative al numero ID equivalente a ogni piatto, anziché alle ordinazioni vere e proprie.  
  
 La tabella ItemTable è collegata al controllo <xref:System.Windows.Forms.ComboBox>, <xref:System.Windows.Forms.ListBox> o <xref:System.Windows.Forms.CheckedListBox> attraverso tre proprietà.  La proprietà  `DataSource`  contiene il nome di questa tabella.  La proprietà  `DisplayMember` contiene la colonna di dati della tabella da visualizzare nel controllo, quella contenente i nomi dei piatti.  La proprietà  `ValueMember`  contiene la colonna di dati della tabella con le informazioni memorizzate \(il numero ID\).  
  
 La tabella OrderDetailsTable è collegata al controllo con il suo insieme di associazioni, accessibile attraverso la proprietà <xref:System.Windows.Forms.Control.DataBindings%2A>.  Quando si aggiunge un oggetto di binding all'insieme, una proprietà del controllo viene collegata a un membro dati specifico \(la colonna dei numeri ID\) in un'origine dati \(la tabella OrderDetailsTable\).  Quando nel controllo viene effettuata una selezione, l'input del form viene salvato in questa tabella.  
  
### Per creare una tabella di ricerca  
  
1.  Aggiungere un controllo <xref:System.Windows.Forms.ComboBox>, <xref:System.Windows.Forms.ListBox> o <xref:System.Windows.Forms.CheckedListBox> al form.  
  
2.  Effettuare la connessione all'origine dati.  
  
3.  Stabilire una relazione dati tra le due tabelle.  Vedere [Introduzione agli oggetti DataRelation](../Topic/Introduction%20to%20DataRelation%20Objects.md).  
  
4.  Impostare le proprietà seguenti,  nel codice o nella finestra di progettazione.  
  
    |Proprietà|Impostazione|  
    |---------------|------------------|  
    |<xref:System.Windows.Forms.ListControl.DataSource%2A>|Nella tabella sono contenute le informazioni relative ai numeri ID equivalenti alle diverse voci.  Nello scenario precedente, si tratta di  `ItemTable`.|  
    |<xref:System.Windows.Forms.ListControl.DisplayMember%2A>|La colonna della tabella dell'origine dati che si vuole visualizzare nel controllo.  Nello scenario precedente, si tratta di  `"Name"`  \(usare le virgolette per l'impostazione nel codice\).|  
    |<xref:System.Windows.Forms.ListControl.ValueMember%2A>|La colonna della tabella di origine dati che contiene le informazioni memorizzate.  Nello scenario precedente, si tratta di  `"ID"`  \(usare le virgolette per l'impostazione nel codice\).|  
  
5.  In una routine, chiamare il metodo <xref:System.Windows.Forms.ControlBindingsCollection.Add%2A> della classe <xref:System.Windows.Forms.ControlBindingsCollection> per associare la proprietà <xref:System.Windows.Forms.ListControl.SelectedValue%2A> del controllo alla tabella che registra l'input del form.  Per effettuare questa operazione nella finestra di progettazione, anziché nel codice, accedere alla proprietà <xref:System.Windows.Forms.Control.DataBindings%2A> del controllo nella finestra **Proprietà**.  Nello scenario precedente, si tratta di  `OrderDetailsTable` e la colonna è  `"ItemID"`.  
  
    ```vb  
    ListBox1.DataBindings.Add("SelectedValue", OrderDetailsTable, "ItemID")  
  
    ```  
  
    ```csharp  
    listBox1.DataBindings.Add("SelectedValue", OrderDetailsTable, "ItemID");  
  
    ```  
  
## Vedere anche  
 [Associazione dati e Windows Form](../../../../docs/framework/winforms/data-binding-and-windows-forms.md)   
 [Cenni preliminari sul controllo ListBox](../../../../docs/framework/winforms/controls/listbox-control-overview-windows-forms.md)   
 [Cenni preliminari sul controllo ComboBox](../../../../docs/framework/winforms/controls/combobox-control-overview-windows-forms.md)   
 [Cenni preliminari sul controllo CheckedListBox](../../../../docs/framework/winforms/controls/checkedlistbox-control-overview-windows-forms.md)   
 [Controlli Windows Form usati per elencare opzioni](../../../../docs/framework/winforms/controls/windows-forms-controls-used-to-list-options.md)