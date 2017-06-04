---
title: "Cenni preliminari sul controllo ListBox (Windows Form) | Microsoft Docs"
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
  - "ListBox"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "caselle di riepilogo, informazioni sulle caselle di riepilogo"
  - "ListBox (controllo) [Windows Form], informazioni sul controllo ListBox"
ms.assetid: 37ea226b-6fc8-4c70-936a-c6af4e0cad4c
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Cenni preliminari sul controllo ListBox (Windows Form)
Un controllo <xref:System.Windows.Forms.ListBox> Windows Form consente di visualizzare un elenco da cui l'utente può selezionare una o più voci.  Se il numero complessivo di voci è superiore al numero visualizzabile, viene aggiunta automaticamente una barra di scorrimento al controllo <xref:System.Windows.Forms.ListBox>.  Se la proprietà <xref:System.Windows.Forms.ListBox.MultiColumn%2A> è impostata su `true`, la casella di riepilogo visualizza elementi su più colonne e viene visualizzata una barra di scorrimento orizzontale.  Se la proprietà <xref:System.Windows.Forms.ListBox.MultiColumn%2A> è impostata su `false`, la casella di riepilogo visualizza elementi su una singola colonna e viene visualizzata una barra di scorrimento verticale.  Se la proprietà <xref:System.Windows.Forms.ListBox.ScrollAlwaysVisible%2A> è impostata su `true`, la barra di scorrimento viene visualizzata indipendentemente dal numero di voci.  La proprietà <xref:System.Windows.Forms.ListBox.SelectionMode%2A> determina il numero di elementi dell'elenco che possono essere selezionati contemporaneamente.  
  
## Come modificare il controllo ListBox  
 La proprietà <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> restituisce un valore integer che corrisponde al primo elemento selezionato nella casella di riepilogo.  È possibile modificare a livello di codice la voce selezionata modificando il valore di <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> nel codice. La voce corrispondente dell'elenco apparirà selezionata nel Windows Form.  Se non è selezionata alcuna voce, il valore <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> della proprietà è \-1.  Se viene selezionato il primo elemento nell'elenco, il valore <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> è 0.  Quando vengono selezionati più elementi, il valore <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> riflette l'elemento selezionato che appare per primo nell'elenco.  La proprietà <xref:System.Windows.Forms.ListBox.SelectedItem%2A> è simile alla proprietà <xref:System.Windows.Forms.ListBox.SelectedIndex%2A>, ma restituisce la voce stessa, in genere costituita da un valore stringa.  La proprietà <xref:System.Windows.Forms.ListBox.ObjectCollection.Count%2A> riflette il numero di elementi presenti nell'elenco e il valore della proprietà <xref:System.Windows.Forms.ListBox.ObjectCollection.Count%2A> supera sempre di uno il massimo valore di <xref:System.Windows.Forms.ListBox.SelectedIndex%2A>, perché <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> è a base zero.  
  
 Per aggiungere o eliminare voci in un controllo <xref:System.Windows.Forms.ListBox>, utilizzare il metodo <xref:System.Windows.Forms.ListBox.ObjectCollection.Add%2A>, <xref:System.Windows.Forms.ListBox.ObjectCollection.Insert%2A>, <xref:System.Windows.Forms.ListBox.ObjectCollection.Clear%2A> o <xref:System.Windows.Forms.ListBox.ObjectCollection.Remove%2A>.  In alternativa, è possibile aggiungere elementi all'elenco utilizzando la proprietà <xref:System.Windows.Forms.ListBox.Items%2A> in fase di progettazione.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ListBox>   
 [Procedura: aggiungere e rimuovere elementi da un controllo ComboBox, ListBox o CheckedListBox Windows Form](../../../../docs/framework/winforms/controls/add-and-remove-items-from-a-wf-combobox.md)   
 [Procedura: ordinare il contenuto di un controllo ComboBox, ListBox o CheckedListBox Windows Form](../../../../docs/framework/winforms/controls/sort-the-contents-of-a-wf-combobox-listbox-or-checkedlistbox-control.md)   
 [Procedura: associare a dati un controllo ComboBox o ListBox Windows Form](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-combobox-or-listbox-control-to-data.md)   
 [Cenni preliminari sul controllo ComboBox](../../../../docs/framework/winforms/controls/combobox-control-overview-windows-forms.md)   
 [Cenni preliminari sul controllo CheckedListBox](../../../../docs/framework/winforms/controls/checkedlistbox-control-overview-windows-forms.md)   
 [Controlli Windows Form usati per elencare opzioni](../../../../docs/framework/winforms/controls/windows-forms-controls-used-to-list-options.md)   
 [Procedura: creare una tabella di ricerca per un controllo ComboBox, ListBox o CheckedListBox Windows Form](../../../../docs/framework/winforms/controls/create-a-lookup-table-for-a-wf-combobox-listbox.md)