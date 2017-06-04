---
title: "Notifica delle modifiche nell&#39;associazione dati dei Windows Form | Microsoft Docs"
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
  - "Windows Form, aggiunta di notifiche di modifica per l'associazione di dati"
  - "Windows Form, associazione dati"
ms.assetid: b5b10f90-0585-41d9-a377-409835262a92
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Notifica delle modifiche nell&#39;associazione dati dei Windows Form
Uno dei concetti più importanti dell'associazione dati dei Windows Form è quello di *notifica delle modifiche*.  Per assicurarsi che l'origine dati e i controlli associati dispongano sempre dei dati più recenti, è necessario aggiungere una notifica delle modifiche per l'associazione dati.  Nella fattispecie, è opportuno accertarsi che i controlli associati ricevano notifica delle modifiche apportate alla relativa origine dati e che l'origine dati riceva notifica delle modifiche apportate alle proprietà associate di un controllo.  
  
 Esistono diversi tipi di notifica delle modifiche, a seconda del tipo di associazione dati:  
  
-   Associazione semplice, in cui la proprietà di un singolo controllo viene associata a una singola istanza di un oggetto.  
  
-   Associazione basata su elenchi, che può includere la proprietà di un singolo controllo associata alla proprietà di un elemento di un elenco o la proprietà di un controllo associata a un elenco di oggetti.  
  
 Inoltre, se si creano controlli Windows Forms da utilizzare per l'associazione dati, sarà necessario applicare il modello *NomeProprietà*Changed ai controlli, in modo che le modifiche apportate alla proprietà associata di un controllo siano propagate all'origine dati.  
  
## Notifica delle modifiche per l'associazione semplice  
 Per l'associazione semplice, è necessario che gli oggetti business forniscano la notifica delle modifiche quando viene modificato il valore di una proprietà associata.  È possibile effettuare questa operazione esponendo un evento *NomeProprietà*Changed per ciascuna proprietà dell'oggetto business e associando tale oggetto ai controlli con la classe <xref:System.Windows.Forms.BindingSource> o il metodo desiderato in cui l'oggetto business implementa l'interfaccia <xref:System.ComponentModel.INotifyPropertyChanged> e genera un evento <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> quando viene modificato il valore di una proprietà.  Per ulteriori informazioni, vedere [Procedura: implementare l'interfaccia INotifyPropertyChanged](../../../docs/framework/winforms/how-to-implement-the-inotifypropertychanged-interface.md).  Quando si utilizzano oggetti che implementano l'interfaccia <xref:System.ComponentModel.INotifyPropertyChanged>, l'utilizzo della classe <xref:System.Windows.Forms.BindingSource> per associare l'oggetto a un controllo non è necessario, ma è consigliato.  
  
## Notifica delle modifiche per l'associazione basata su elenchi  
 Nei Windows Form la notifica ai controlli associati delle informazioni sulle modifiche delle proprietà \(viene modificato il valore di una proprietà di un elemento dell'elenco\) e le modifiche dell'elenco \(viene eliminato o aggiunto un elemento all'elenco\) dipende da un elenco associato.  Pertanto gli elenchi utilizzati per l'associazione dati devono implementare l'interfaccia <xref:System.ComponentModel.IBindingList>, che fornisce entrambi i tipi di notifica delle modifiche.  <xref:System.ComponentModel.BindingList%601> è un'implementazione generica dell'interfaccia <xref:System.ComponentModel.IBindingList> ed è progettata per l'utilizzo con l'associazione dati dei Windows Form.  È possibile creare una classe <xref:System.ComponentModel.BindingList%601> contenente un tipo di oggetto business che implementa <xref:System.ComponentModel.INotifyPropertyChanged> e l'elenco convertirà automaticamente gli eventi <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> in eventi <xref:System.ComponentModel.IBindingList.ListChanged>.  Se l'elenco associato non è un'interfaccia <xref:System.ComponentModel.IBindingList>, sarà necessario associare l'elenco di oggetti ai controlli Windows Form utilizzando il componente <xref:System.Windows.Forms.BindingSource>.  Il componente <xref:System.Windows.Forms.BindingSource> consentirà una conversione da proprietà a elenco simile a quella di <xref:System.ComponentModel.BindingList%601>.  Per ulteriori informazioni, vedere [Procedura: generare notifiche di modifica utilizzando un BindingSource e l'interfaccia INotifyPropertyChanged](../../../docs/framework/winforms/controls/raise-change-notifications--bindingsource.md).  
  
## Notifica delle modifiche per i controlli personalizzati  
 Infine, dal lato dei controlli, sarà necessario esporre un evento *NomeProprietà*Changed per ciascuna proprietà progettata per l'associazione ai dati.  Le modifiche apportate alla proprietà dei controlli verranno quindi propagate all'origine dati associata.  Per ulteriori informazioni, vedere [Procedura: applicare il modello PropertyNameChanged](../../../docs/framework/winforms/how-to-apply-the-propertynamechanged-pattern.md)  
  
## Vedere anche  
 <xref:System.Windows.Forms.BindingSource>   
 <xref:System.ComponentModel.INotifyPropertyChanged>   
 <xref:System.ComponentModel.BindingList%601>   
 [Associazione ai dati di Windows Form](../../../docs/framework/winforms/windows-forms-data-binding.md)   
 [Origini dati supportate da Windows Form](../../../docs/framework/winforms/data-sources-supported-by-windows-forms.md)   
 [Associazione dati e Windows Form](../../../docs/framework/winforms/data-binding-and-windows-forms.md)