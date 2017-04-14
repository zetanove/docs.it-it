---
title: "Procedura: ordinare il contenuto di un controllo ComboBox, ListBox o CheckedListBox Windows Form | Microsoft Docs"
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
  - "CheckedListBox (controllo) [Windows Form], ordinamento"
  - "caselle combinate, ordinamento di contenuto"
  - "ComboBox (controllo) [Windows Form], ordinamento di contenuto"
  - "caselle di riepilogo, ordinamento di contenuto"
  - "ListBox (controllo) [Windows Form], ordinamento di contenuto"
ms.assetid: c268e387-3d1d-4d86-a940-19f6673c8d06
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: ordinare il contenuto di un controllo ComboBox, ListBox o CheckedListBox Windows Form
L'ordinamento del contenuto dei controlli Windows Form non è possibile se ai controlli sono associati dati.  Per visualizzare dati ordinati, utilizzare un'origine dati che supporta l'ordinamento, in modo che questo possa essere eseguito automaticamente.  Le origini dati che supportano l'ordinamento sono visualizzazioni dati, gestori di visualizzazione dati e matrici ordinate.  
  
 Se il controllo non è associato a dati, è possibile ordinarlo.  
  
### Per ordinare l'elenco  
  
1.  Impostare la proprietà `Sorted` su `true`.  
  
     L'impostazione riposiziona tutte le voci di elenco esistenti nell'ordine specificato.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ComboBox>   
 <xref:System.Windows.Forms.ListBox>   
 <xref:System.Windows.Forms.CheckedListBox>   
 [Associazione ai dati di Windows Form](../../../../docs/framework/winforms/windows-forms-data-binding.md)   
 [Procedura: aggiungere e rimuovere elementi da un controllo ComboBox, ListBox o CheckedListBox Windows Form](../../../../docs/framework/winforms/controls/add-and-remove-items-from-a-wf-combobox.md)   
 [Quando utilizzare un controllo ComboBox Windows Form anziché un controllo ListBox](../../../../docs/framework/winforms/controls/when-to-use-a-windows-forms-combobox-instead-of-a-listbox.md)   
 [Controlli Windows Form usati per elencare opzioni](../../../../docs/framework/winforms/controls/windows-forms-controls-used-to-list-options.md)