---
title: "Procedura: eseguire l&#39;associazione di una raccolta e visualizzare informazioni in base alla selezione effettuata | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "associazione dati, associazione a raccolte"
  - "associazione dati, creazione di visualizzazioni di raccolte dati"
  - "associazione dati, selezione di dati per le visualizzazioni"
  - "raccolte dati, selezione di dati per le visualizzazioni"
ms.assetid: 952a7d76-dd29-49e5-86f5-32c4530e70eb
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: eseguire l&#39;associazione di una raccolta e visualizzare informazioni in base alla selezione effettuata
In un semplice scenario Master\-Details si dispone di un elemento <xref:System.Windows.Controls.ItemsControl> associato ai dati come <xref:System.Windows.Controls.ListBox>.  In base alla selezione dell'utente vengono visualizzate più informazioni relative all'elemento selezionato.  In questo esempio viene illustrato come implementare tale scenario.  
  
## Esempio  
 In questo esempio `People` è un oggetto <xref:System.Collections.ObjectModel.ObservableCollection%601> delle classi `Person`.  Questa classe `Person` contiene tre proprietà, `FirstName`, `LastName` e `HomeTown`, tutte di tipo `string`.  
  
 [!code-xml[CollectionBinding#Source](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Window1.xaml#source)]  
[!code-xml[CollectionBinding#UI](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Window1.xaml#ui)]  
  
 <xref:System.Windows.Controls.ContentControl> utilizza l'oggetto <xref:System.Windows.DataTemplate> riportato di seguito che definisce il modo in cui vengono presentate le informazioni di `Person`:  
  
 [!code-xml[CollectionBinding#DetailTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Window1.xaml#detailtemplate)]  
  
 Di seguito è disponibile una schermata del risultato dell'esempio.  <xref:System.Windows.Controls.ContentControl> mostra le altre proprietà della persona selezionata.  
  
 ![Binding to a Collection](../../../../docs/framework/wpf/data/media/databinding-collectionbindingsample.png "DataBinding\_CollectionBindingSample")  
  
 Si notino i due aspetti dell'esempio riportati di seguito:  
  
1.  <xref:System.Windows.Controls.ListBox> e <xref:System.Windows.Controls.ContentControl> sono associati alla stessa origine.  Le proprietà <xref:System.Windows.Data.Binding.Path%2A> di entrambe le associazioni non sono specificate perché entrambi i controlli vengono associati all'intero oggetto Collection.  
  
2.  È necessario impostare la proprietà <xref:System.Windows.Controls.Primitives.Selector.IsSynchronizedWithCurrentItem%2A> su `true` perché funzioni.  L'impostazione di questa proprietà assicura che l'elemento selezionato sia sempre impostato come <xref:System.Windows.Controls.ItemCollection.CurrentItem%2A>.  In alternativa, se <xref:System.Windows.Controls.ListBox> ottiene i dati da un oggetto <xref:System.Windows.Data.CollectionViewSource>, la selezione e la valuta vengono sincronizzate automaticamente.  
  
 L'override del metodo `ToString` viene eseguito dalla classe `Person` nel modo seguente.  Per impostazione predefinita, <xref:System.Windows.Controls.ListBox> chiama `ToString` e visualizza una rappresentazione di stringa di ogni oggetto nella raccolta associata.  Questo è il motivo per cui ogni oggetto `Person` viene visualizzato come nome nel controllo <xref:System.Windows.Controls.ListBox>.  
  
 [!code-csharp[CollectionBinding#ToString](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Data.cs#tostring)]
 [!code-vb[CollectionBinding#ToString](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CollectionBinding/VisualBasic/Person.vb#tostring)]  
  
## Vedere anche  
 [Utilizzare il modello Master\-Details con dati gerarchici](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-data.md)   
 [Utilizzare il modello Master\-Details con dati XML gerarchici](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-xml-data.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Cenni preliminari sui modelli di dati](../../../../docs/framework/wpf/data/data-templating-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)