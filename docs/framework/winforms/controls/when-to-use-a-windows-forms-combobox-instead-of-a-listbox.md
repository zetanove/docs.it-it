---
title: "Quando utilizzare un controllo ComboBox Windows Form anzich&#233; un controllo ListBox | Microsoft Docs"
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
  - "controlli con associazione, caselle combinate"
  - "caselle combinate, confronto con caselle di riepilogo"
  - "ComboBox (controllo) [Windows Form], confronto con ListBox"
  - "ListBox (controllo) [Windows Form], accesso a elementi"
  - "ListBox (controllo) [Windows Form], aggiunta e rimozione di elementi"
  - "ListBox (controllo) [Windows Form], ComboBox"
  - "ListCount (proprietà)"
  - "ListIndex (proprietà)"
  - "controlli Windows Form, associazione dati"
ms.assetid: 7bcaea58-1cfa-46db-9baf-b75a69d8f9ec
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Quando utilizzare un controllo ComboBox Windows Form anzich&#233; un controllo ListBox
Il comportamento del controllo <xref:System.Windows.Forms.ComboBox> e del controllo <xref:System.Windows.Forms.ListBox> è simile e in alcuni casi intercambiabile.  A volte tuttavia la funzionalità di un controllo risulta più adatta a una particolare attività rispetto alla funzionalità dell'altro.  
  
 Una casella combinata è in genere appropriata se esiste un elenco che suggerisce una serie di possibilità, mentre una casella di riepilogo risulta utile se si desidera limitare la selezione delle voci in elenco.  La casella combinata contiene una casella di testo in cui è possibile digitare le opzioni non presenti nell'elenco.  L'eccezione si verifica quando la proprietà <xref:System.Windows.Forms.ComboBox.DropDownStyle%2A> è impostata su <xref:System.Windows.Forms.ComboBoxStyle>.  nel qual caso l'elemento verrà selezionato automaticamente non appena l'utente digita la prima lettera.  
  
 Le caselle combinate consentono inoltre di risparmiare spazio nel form.  Poiché infatti l'elenco completo viene visualizzato solo facendo clic sulla freccia a discesa, una casella combinata può essere inserita in uno spazio ristretto in cui non sarebbe possibile inserire una casella di riepilogo.  Quando invece la proprietà <xref:System.Windows.Forms.ComboBox.DropDownStyle%2A> è impostata su <xref:System.Windows.Forms.ComboBoxStyle>, viene visualizzato l'elenco completo e la casella combinata occupa uno spazio maggiore rispetto a una casella di riepilogo.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ComboBox>   
 <xref:System.Windows.Forms.ListBox>   
 [Procedura: aggiungere e rimuovere elementi da un controllo ComboBox, ListBox o CheckedListBox Windows Form](../../../../docs/framework/winforms/controls/add-and-remove-items-from-a-wf-combobox.md)   
 [Procedura: ordinare il contenuto di un controllo ComboBox, ListBox o CheckedListBox Windows Form](../../../../docs/framework/winforms/controls/sort-the-contents-of-a-wf-combobox-listbox-or-checkedlistbox-control.md)   
 [Controlli Windows Form usati per elencare opzioni](../../../../docs/framework/winforms/controls/windows-forms-controls-used-to-list-options.md)