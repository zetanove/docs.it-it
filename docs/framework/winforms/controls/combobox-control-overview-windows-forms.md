---
title: "Cenni preliminari sul controllo ComboBox (Windows Form) | Microsoft Docs"
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
  - "ComboBox"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "caselle combinate, informazioni sulle caselle combinate"
  - "ComboBox (controllo) [Windows Form], informazioni sul controllo ComboBox"
  - "elenchi a discesa, ComboBox (controllo)"
  - "elenchi a discesa, Windows Form"
ms.assetid: a58b393f-a614-45d1-8961-857a024b5acd
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Cenni preliminari sul controllo ComboBox (Windows Form)
Il controllo <xref:System.Windows.Forms.ComboBox> Windows Form viene utilizzato per visualizzare dati in una casella combinata a discesa.  Per impostazione predefinita, il controllo <xref:System.Windows.Forms.ComboBox> è costituito da due parti: la parte superiore è una casella di testo che consente all'utente di digitare una voce di elenco,  la seconda parte è una casella di riepilogo che visualizza un elenco dal quale l'utente può selezionare una o più voci.  Per ulteriori informazioni sugli altri stili di caselle combinate, vedere [Quando utilizzare un controllo ComboBox Windows Form anziché un controllo ListBox](../../../../docs/framework/winforms/controls/when-to-use-a-windows-forms-combobox-instead-of-a-listbox.md).  
  
 La proprietà <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> restituisce un valore intero che corrisponde alla voce selezionata nell'elenco.  È possibile modificare la voce selezionata a livello di codice mediante la modifica del valore <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> nel codice. La voce in elenco corrispondente apparirà nella parte di casella di testo della casella combinata.  Se non è selezionata alcuna voce, il valore <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> della proprietà è \-1.  Se è selezionata la prima voce dell'elenco, il valore <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> della proprietà è 0.  La <xref:System.Windows.Forms.ComboBox.SelectedItem%2A> proprietà è simile a <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> , ma restituisce la voce stessa, in genere costituita da un valore stringa.  La proprietà <xref:System.Windows.Forms.ComboBox.ObjectCollection.Count%2A> riflette il numero di elementi presenti nell'elenco e il valore della proprietà <xref:System.Windows.Forms.ComboBox.ObjectCollection.Count%2A> supera sempre di uno il massimo valore di <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A>, perché <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> è a base zero.  
  
 Per aggiungere o eliminare voci in un controllo <xref:System.Windows.Forms.ComboBox>, utilizzare il metodo <xref:System.Windows.Forms.ComboBox.ObjectCollection.Add%2A>, <xref:System.Windows.Forms.ComboBox.ObjectCollection.Insert%2A>, <xref:System.Windows.Forms.ComboBox.ObjectCollection.Clear%2A> o <xref:System.Windows.Forms.ComboBox.ObjectCollection.Remove%2A>.  In alternativa è possibile aggiungere voci all'elenco mediante l'utilizzo della proprietà <xref:System.Windows.Forms.ComboBox.Items%2A> nella finestra di progettazione.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ComboBox>   
 [Cenni preliminari sul controllo ListBox](../../../../docs/framework/winforms/controls/listbox-control-overview-windows-forms.md)   
 [Quando utilizzare un controllo ComboBox Windows Form anziché un controllo ListBox](../../../../docs/framework/winforms/controls/when-to-use-a-windows-forms-combobox-instead-of-a-listbox.md)   
 [Procedura: aggiungere e rimuovere elementi da un controllo ComboBox, ListBox o CheckedListBox Windows Form](../../../../docs/framework/winforms/controls/add-and-remove-items-from-a-wf-combobox.md)   
 [Procedura: ordinare il contenuto di un controllo ComboBox, ListBox o CheckedListBox Windows Form](../../../../docs/framework/winforms/controls/sort-the-contents-of-a-wf-combobox-listbox-or-checkedlistbox-control.md)   
 [Procedura: accedere a elementi specifici di un controllo ComboBox, ListBox o CheckedListBox Windows Form](../../../../docs/framework/winforms/controls/access-specific-items-in-a-wf-combobox-listbox-or-checkedlistbox.md)   
 [Procedura: associare a dati un controllo ComboBox o ListBox Windows Form](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-combobox-or-listbox-control-to-data.md)   
 [Controlli Windows Form usati per elencare opzioni](../../../../docs/framework/winforms/controls/windows-forms-controls-used-to-list-options.md)   
 [Procedura: creare una tabella di ricerca per un controllo ComboBox, ListBox o CheckedListBox Windows Form](../../../../docs/framework/winforms/controls/create-a-lookup-table-for-a-wf-combobox-listbox.md)