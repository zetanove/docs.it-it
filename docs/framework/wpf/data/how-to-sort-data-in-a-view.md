---
title: "Procedura: ordinare i dati in una visualizzazione | Microsoft Docs"
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
  - "associazione dati, raggruppamento di dati in visualizzazioni"
  - "associazione dati, ordinamento di dati in visualizzazioni"
  - "raggruppamento di dati in visualizzazioni"
  - "ordinamento di dati in visualizzazioni"
  - "visualizzazioni, raggruppamento di dati"
  - "visualizzazioni, ordinamento dei dati"
ms.assetid: f4c43578-01b7-4774-a953-acb95a13b94a
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: ordinare i dati in una visualizzazione
In questo esempio viene descritto come ordinare i dati in una visualizzazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene creato un oggetto <xref:System.Windows.Controls.ListBox> semplice e <xref:System.Windows.Controls.Button>:  
  
 [!code-xml[ListBoxSort_snip#HowTo](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListBoxSort_snip/CSharp/Window1.xaml#howto)]  
  
 Il gestore eventi <xref:System.Windows.Controls.Primitives.ButtonBase.Click> del pulsante contiene la logica per ordinare gli elementi in <xref:System.Windows.Controls.ListBox> in ordine discendente.  Questa operazione è possibile in quanto aggiungendo elementi a <xref:System.Windows.Controls.ListBox>, in questo modo vengono aggiunti a <xref:System.Windows.Controls.ItemCollection> dell'oggetto <xref:System.Windows.Controls.ListBox> e <xref:System.Windows.Controls.ItemCollection> deriva dalla classe <xref:System.Windows.Data.CollectionView>.  Se <xref:System.Windows.Controls.ListBox> deve essere associato a una raccolta mediante la proprietà <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>, si può utilizzare la stessa tecnica di ordinamento.  
  
 [!code-csharp[ListBoxSort_snip#HowToCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListBoxSort_snip/CSharp/Window1.xaml.cs#howtocode)]
 [!code-vb[ListBoxSort_snip#HowToCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ListBoxSort_snip/visualbasic/window1.xaml.vb#howtocode)]  
  
 Finché si possiede un riferimento all'oggetto di visualizzazione è possibile utilizzare la stessa tecnica di ordinamento del contenuto di altre visualizzazioni di raccolte.  Per un esempio della procedura da seguire per ottenere una visualizzazione, vedere [Ottenere la visualizzazione predefinita di una raccolta dati](../../../../docs/framework/wpf/data/how-to-get-the-default-view-of-a-data-collection.md).  Per un altro esempio, vedere [Ordinare una colonna GridView quando si fa clic su un'intestazione](../../../../docs/framework/wpf/controls/how-to-sort-a-gridview-column-when-a-header-is-clicked.md).  Per ulteriori informazioni sulle visualizzazioni, vedere la sezione relativa all'associazione alle raccolte in [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
 Per un esempio su come applicare la logica di ordinamento in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], vedere [Ordinare e raggruppare dati tramite una visualizzazione in XAML](../../../../docs/framework/wpf/data/how-to-sort-and-group-data-using-a-view-in-xaml.md).  
  
## Vedere anche  
 <xref:System.Windows.Data.ListCollectionView.CustomSort%2A>   
 [Ordinare una colonna GridView quando si fa clic su un'intestazione](../../../../docs/framework/wpf/controls/how-to-sort-a-gridview-column-when-a-header-is-clicked.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Filtrare i dati di una visualizzazione](../../../../docs/framework/wpf/data/how-to-filter-data-in-a-view.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)