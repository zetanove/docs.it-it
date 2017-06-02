---
title: "Procedura: utilizzare il modello Master-Details con dati gerarchici | Microsoft Docs"
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
  - "associazione dati, paradigma dati Master-Detail"
  - "paradigma dati Master-Detail"
ms.assetid: 11429b9e-058d-4084-bfb6-2cf209c8ddf7
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: utilizzare il modello Master-Details con dati gerarchici
In questo esempio viene illustrato come implementare lo scenario Master\-Details.  
  
## Esempio  
 In questo esempio, `LeagueList` è una raccolta di `Leagues`.  Ogni `League` ha un `Name` e una raccolta di `Divisions` e ciascuna `Division` ha un nome e una raccolta di `Teams`.  Ogni `Team` ha un nome.  
  
 [!code-xml[MasterDetail#HowTo1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MasterDetail/VisualBasic/Page1.xaml#howto1)]  
[!code-xml[MasterDetail#HowTo2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MasterDetail/VisualBasic/Page1.xaml#howto2)]  
  
 Di seguito è disponibile una schermata dell'esempio.  Il controllo <xref:System.Windows.Controls.ListBox> `Divisions` consente di rilevare automaticamente le selezioni nel controllo <xref:System.Windows.Controls.ListBox> `Leagues` e di visualizzare i dati corrispondenti.  Il controllo <xref:System.Windows.Controls.ListBox> `Teams` consente di rilevare le selezioni negli altri due controlli <xref:System.Windows.Controls.ListBox>.  
  
 ![Esempio Master Detail Data](../../../../docs/framework/wpf/data/media/databindingmasterdetailsample.png "DataBindingMasterDetailSample")  
  
 Si notino i due aspetti dell'esempio riportati di seguito:  
  
1.  I tre controlli <xref:System.Windows.Controls.ListBox> sono associati alla stessa origine.  La proprietà <xref:System.Windows.Data.Binding.Path%2A> è dell'associazione viene impostata per specificare quale livello di dati deve essere visualizzato dal controllo <xref:System.Windows.Controls.ListBox>.  
  
2.  È necessario impostare la proprietà <xref:System.Windows.Controls.Primitives.Selector.IsSynchronizedWithCurrentItem%2A> su `true` sui controlli <xref:System.Windows.Controls.ListBox> di cui si intende rilevare le selezioni.  L'impostazione di questa proprietà assicura che l'elemento selezionato sia sempre impostato come <xref:System.Windows.Controls.ItemCollection.CurrentItem%2A>.  In alternativa, se <xref:System.Windows.Controls.ListBox> ottiene i dati da un oggetto <xref:System.Windows.Data.CollectionViewSource>, la selezione e la valuta vengono sincronizzate automaticamente.  
  
 La tecnica varia leggermente se si utilizzano dati [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)].  Per un esempio, vedere [Utilizzare il modello Master\-Details con dati XML gerarchici](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-xml-data.md).  
  
## Vedere anche  
 <xref:System.Windows.HierarchicalDataTemplate>   
 [Eseguire l'associazione a una raccolta e visualizzare informazioni in base alla selezione](../../../../docs/framework/wpf/data/how-to-bind-to-a-collection-and-display-information-based-on-selection.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Cenni preliminari sui modelli di dati](../../../../docs/framework/wpf/data/data-templating-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)