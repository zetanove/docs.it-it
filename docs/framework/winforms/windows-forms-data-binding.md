---
title: "Associazione ai dati di Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli con associazione, Windows Form"
  - "dati [Windows Form]"
  - "dati [Windows Form], architettura"
  - "Controlli Windows Form, associazione dati"
  - "Windows Form, associazione dati"
ms.assetid: c3826d8e-ea25-4ad4-a669-45bfb19192aa
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 25
---
# Associazione ai dati di Windows Form
Data binding in Windows Form consente di visualizzare e modificare le informazioni da un'origine dati nei controlli del form.  È possibile effettuare associazioni alle origini dati tradizionali e a quasi ogni struttura che contiene dati.  
  
## In questa sezione  
 [Associazione dati e Windows Form](../../../docs/framework/winforms/data-binding-and-windows-forms.md)  
 Fornisce una panoramica del data binding in Windows Form.  
  
 [Origini dati supportate da Windows Form](../../../docs/framework/winforms/data-sources-supported-by-windows-forms.md)  
 Descrive le origini dati che possono essere usate con Windows Form.  
  
 [Interfacce correlate all'associazione dati](../../../docs/framework/winforms/interfaces-related-to-data-binding.md)  
 Descrive molte delle interfacce usate con il data binding in Windows Form.  
  
 [Procedura: esplorare dati in Windows Form](../../../docs/framework/winforms/how-to-navigate-data-in-windows-forms.md)  
 Mostra come spostarsi tra gli elementi in un'origine dati.  
  
 [Notifica delle modifiche nell'associazione dati dei Windows Form](../../../docs/framework/winforms/change-notification-in-windows-forms-data-binding.md)  
 Descrive i vari tipi di notifica delle modifiche per il data binding in Windows Form.  
  
 [Procedura: implementare l'interfaccia INotifyPropertyChanged](../../../docs/framework/winforms/how-to-implement-the-inotifypropertychanged-interface.md)  
 Mostra come implementare l'interfaccia <xref:System.ComponentModel.INotifyPropertyChanged>.  L'interfaccia comunica a un controllo associato le modifiche delle proprietà di un oggetto business.  
  
 [Procedura: applicare il modello PropertyNameChanged](../../../docs/framework/winforms/how-to-apply-the-propertynamechanged-pattern.md)  
 Illustra come applicare il modello *NomeProprietà*Changed alle proprietà di un controllo utente Windows Form.  
  
 [Procedura: implementare l'interfaccia ITypedList](../../../docs/framework/winforms/how-to-implement-the-itypedlist-interface.md)  
 Mostra come abilitare l'individuazione dello schema per un elenco associabile mediante l'implementazione dell'interfaccia <xref:System.ComponentModel.ITypedList>.  
  
 [Procedura: implementare l'interfaccia IListSource](../../../docs/framework/winforms/how-to-implement-the-ilistsource-interface.md)  
 Illustra come implementare l'interfaccia <xref:System.ComponentModel.IListSource> per creare una classe associabile che non implementa <xref:System.Collections.IList>, ma fornisce un elenco da un altro percorso.  
  
 [Procedura: garantire la sincronizzazione di più controlli associati alla stessa origine dati](../../../docs/framework/winforms/multiple-controls-bound-to-data-source-synchronized.md)  
 Mostra come gestire l'evento <xref:System.Windows.Forms.BindingSource.BindingComplete> per assicurare che tutti i controlli associati a un'origine dati rimangano sincronizzati.  
  
 [Procedura: garantire che la riga selezionata in una tabella figlio rimanga nella posizione corretta](../../../docs/framework/winforms/ensure-the-selected-row-in-a-child-table-correct.md)  
 Mostra come garantire che la riga selezionata di una tabella figlio non venga modificata quando viene apportata una modifica a un campo della tabella padre.  
  
 Vedere anche [Interfacce correlate al data binding](http://msdn.microsoft.com/library/41e17s4b\(v=vs.110\)), [Procedura: Esplorare dati in Windows Form](http://msdn.microsoft.com/library/b63ha24w\(v=vs.110\)), [Procedura: Creare un controllo con associazione semplice in un Windows Form](http://msdn.microsoft.com/library/sw223a62\(v=vs.110\)).  
  
## Riferimenti  
 <xref:System.Windows.Forms.Binding?displayProperty=fullName>  
 Descrive la classe che rappresenta l'associazione tra un componente associabile e un'origine dati.  
  
 <xref:System.Windows.Forms.BindingSource?displayProperty=fullName>  
 Descrive la classe che incapsula un'origine dati per l'associazione ai controlli.  
  
## Sezioni correlate  
 [Il componente BindingSource](../../../docs/framework/winforms/controls/bindingsource-component.md)  
 Contiene un elenco di argomenti in cui viene illustrato come usare il componente <xref:System.Windows.Forms.BindingSource>.  
  
 [Controllo DataGridView](../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)  
 Fornisce un elenco di argomenti in cui viene illustrato come usare un controllo Datagrid associabile.  
  
 Vedere anche [Accesso ai dati in Visual Studio](http://msdn.microsoft.com/library/wzabh8c4\(v=vs.110\)) o [Accesso ai dati in Visual Studio](http://msdn.microsoft.com/library/wzabh8c4\(v=vs.110\)).