---
title: "Procedura: filtrare i dati in una visualizzazione | Microsoft Docs"
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
  - "associazione dati, filtro di dati in visualizzazioni"
  - "filtro di dati in visualizzazioni"
  - "visualizzazioni, filtro di dati"
ms.assetid: c76e8606-4cc4-45a8-9110-e2ec66dc6afd
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: filtrare i dati in una visualizzazione
In questo esempio viene illustrata la procedura per filtrare i dati in una visualizzazione.  
  
## Esempio  
 Per creare un filtro, definire un metodo che fornisca la logica di filtro.  Il metodo viene utilizzato come callback e accetta un parametro di tipo `object`.  Il metodo riportato di seguito restituisce tutti gli oggetti `Order` con la proprietà `filled` impostata su "No", filtrando i restanti oggetti.  
  
 [!code-csharp[SortFilter#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SortFilter/CSharp/Page1.xaml.cs#2)]
 [!code-vb[SortFilter#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SortFilter/VisualBasic/Page1.xaml.vb#2)]  
  
 È possibile quindi applicare il filtro, come illustrato nell'esempio seguente.  In questo esempio, `myCollectionView` è un oggetto <xref:System.Windows.Data.ListCollectionView>.  
  
 [!code-csharp[SortFilter#Filter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SortFilter/CSharp/Page1.xaml.cs#filter)]
 [!code-vb[SortFilter#Filter](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SortFilter/VisualBasic/Page1.xaml.vb#filter)]  
  
 Per rimuovere il filtro, è possibile impostare la proprietà <xref:System.Windows.Data.CollectionView.Filter%2A> su `null`:  
  
 [!code-csharp[SortFilter#Unfilter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SortFilter/CSharp/Page1.xaml.cs#unfilter)]
 [!code-vb[SortFilter#Unfilter](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SortFilter/VisualBasic/Page1.xaml.vb#unfilter)]  
  
 Per informazioni su come creare o ottenere una visualizzazione, vedere [Ottenere la visualizzazione predefinita di una raccolta dati](../../../../docs/framework/wpf/data/how-to-get-the-default-view-of-a-data-collection.md).  Per l'esempio completo, vedere [Esempio di ordinamento e filtro di elementi in una visualizzazione](http://go.microsoft.com/fwlink/?LinkID=160040) \(la pagina potrebbe essere in inglese\).  
  
 Se l'oggetto visualizzazione proviene da un oggetto<xref:System.Windows.Data.CollectionViewSource>, applicare la logica di filtro impostando un gestore eventi per l'evento <xref:System.Windows.Data.CollectionViewSource.Filter>.  Nell'esempio riportato di seguito, `listingDataView` è un'istanza di <xref:System.Windows.Data.CollectionViewSource>.  
  
 [!code-csharp[DataBindingLab#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml.cs#10)]
 [!code-vb[DataBindingLab#10](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataBindingLab/VisualBasic/MainWindow.xaml.vb#10)]  
  
 Nell'esempio seguente viene illustrata l'implementazione del gestore eventi del filtro `ShowOnlyBargainsFilter` di esempio.  Questo gestore eventi utilizza la proprietà <xref:System.Windows.Data.FilterEventArgs.Accepted%2A> per filtrare gli oggetti `AuctionItem` con `CurrentPrice` pari a 25 dollari o superiore.  
  
 [!code-csharp[DataBindingLab#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml.cs#5)]
 [!code-vb[DataBindingLab#5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataBindingLab/VisualBasic/MainWindow.xaml.vb#5)]  
  
## Vedere anche  
 <xref:System.Windows.Data.CollectionView.CanFilter%2A>   
 <xref:System.Windows.Data.BindingListCollectionView.CustomFilter%2A>   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Ordinare i dati in una visualizzazione](../../../../docs/framework/wpf/data/how-to-sort-data-in-a-view.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)