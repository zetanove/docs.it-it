---
title: "Procedura: modificare l&#39;allineamento orizzontale di una colonna in ListView | Microsoft Docs"
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
  - "ListView (controlli), allineamento orizzontale"
ms.assetid: b9573e44-9dad-4d14-939c-7859ca372758
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: modificare l&#39;allineamento orizzontale di una colonna in ListView
Per impostazione predefinita, il contenuto di ogni colonna in <xref:System.Windows.Controls.ListViewItem> è allineato a sinistra.  È possibile modificare l'allineamento di ciascuna colonna fornendo un oggetto <xref:System.Windows.DataTemplate> e impostando la proprietà <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> sull'elemento all'interno di <xref:System.Windows.DataTemplate>.  In questo argomento viene descritto l'allineamento predefinito del contenuto in <xref:System.Windows.Controls.ListView> e come modificare l'allineamento di una colonna in <xref:System.Windows.Controls.ListView>.  
  
## Esempio  
 Nell'esempio riportato di seguito, i dati nelle colonne `Title` e `ISBN` sono allineati a sinistra.  
  
 [!code-xml[ListViewHowTos#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#1)]  
[!code-xml[ListViewHowTos#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#2)]  
  
 Per modificare l'allineamento della colonna `ISBN`, specificare che la proprietà <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> di ogni <xref:System.Windows.Controls.ListViewItem> è <xref:System.Windows.HorizontalAlignment>, in modo che gli elementi all'interno di ogni <xref:System.Windows.Controls.ListViewItem> possano essere estesi o posizionati sull'intera larghezza di ciascuna colonna.  Poiché l'oggetto <xref:System.Windows.Controls.ListView> è associato a un'origine dati, sarà necessario creare uno stile che imposta <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A>.  Per la visualizzazione del contenuto, utilizzare quindi <xref:System.Windows.DataTemplate> anziché la proprietà <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A>.  Per visualizzare l'`ISBN` di ciascun modello, <xref:System.Windows.DataTemplate> può contenere un solo oggetto <xref:System.Windows.Controls.TextBlock> con la proprietà <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> impostata su <xref:System.Windows.HorizontalAlignment>.  
  
 Nell'esempio riportato di seguito vengono definiti stile e <xref:System.Windows.DataTemplate> necessari per allineare a destra la colonna `ISBN` e viene modificato l'oggetto <xref:System.Windows.Controls.GridViewColumn> in modo che faccia riferimento a <xref:System.Windows.DataTemplate>.  
  
 [!code-xml[ListViewHowTos#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#3)]  
[!code-xml[ListViewHowTos#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#4)]  
  
## Vedere anche  
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Cenni preliminari sui modelli di dati](../../../../docs/framework/wpf/data/data-templating-overview.md)   
 [Eseguire l'associazione ai dati XML utilizzando un oggetto XMLDataProvider e le query XPath](../../../../docs/framework/wpf/data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)   
 [Panoramica sul controllo ListView](../../../../docs/framework/wpf/controls/listview-overview.md)