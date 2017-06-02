---
title: "Procedura: ottenere la visualizzazione predefinita di una raccolta dati | Microsoft Docs"
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
  - "creazione, visualizzazioni di raccolte dati"
  - "associazione dati, creazione di visualizzazioni di raccolte dati"
  - "raccolte dati, creazione di visualizzazioni"
ms.assetid: b641e96c-c2f6-42ea-9c5d-bac81176ad65
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: ottenere la visualizzazione predefinita di una raccolta dati
È possibile visualizzare una stessa raccolta dati in diversi modi, in base ai criteri di ordinamento, filtro o raggruppamento.  Ogni raccolta dispone di una visualizzazione predefinita condivisa, utilizzata come origine di associazione effettiva quando un'associazione specifica una raccolta come origine.  In questo esempio viene illustrato come ottenere la visualizzazione predefinita di una raccolta.  
  
## Esempio  
 Per creare la visualizzazione, è necessario un riferimento a un oggetto nella raccolta.  È possibile ottenere tale oggetto dati facendo riferimento all'oggetto code\-behind utilizzato oppure ottenendo il contesto dati, una proprietà dell'origine dati o una proprietà dell'associazione.  Nell'esempio viene illustrato come ottenere l'oggetto <xref:System.Windows.FrameworkElement.DataContext%2A> di un oggetto dati e come utilizzarlo per ottenere direttamente la visualizzazione predefinita della raccolta.  
  
 [!code-csharp[CollectionView#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionView/CSharp/Page1.xaml.cs#2)]
 [!code-vb[CollectionView#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CollectionView/VisualBasic/Page1.xaml.vb#2)]  
  
 In questo esempio, l'elemento radice è un oggetto <xref:System.Windows.Controls.StackPanel>.  L'oggetto <xref:System.Windows.FrameworkElement.DataContext%2A> è impostato su *myDataSource*, in modo da fare riferimento a un provider di dati che rappresenta un oggetto <xref:System.Collections.ObjectModel.ObservableCollection%601> di oggetti *Order*.  
  
 [!code-xml[CollectionView#CollectionViewDataContext](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionView/CSharp/Page1.xaml#collectionviewdatacontext)]  
  
 In alternativa, è possibile creare un'istanza ed eseguire l'associazione a una visualizzazione di raccolta personalizzata mediante la classe <xref:System.Windows.Data.CollectionViewSource>.  Questa visualizzazione di raccolta è condivisa solo dai controlli che ne eseguono direttamente l'associazione.  Per un esempio, vedere la sezione Procedura per la creazione di una visualizzazione in [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
 Per esempi delle funzionalità fornite da una visualizzazione di una raccolta, vedere [Ordinare i dati in una visualizzazione](../../../../docs/framework/wpf/data/how-to-sort-data-in-a-view.md), [Filtrare i dati di una visualizzazione](../../../../docs/framework/wpf/data/how-to-filter-data-in-a-view.md) e [Navigare tra gli oggetti nella visualizzazione di una raccolta dati](../../../../docs/framework/wpf/data/how-to-navigate-through-the-objects-in-a-data-collectionview.md).  
  
## Vedere anche  
 [Ordinare e raggruppare dati tramite una visualizzazione in XAML](../../../../docs/framework/wpf/data/how-to-sort-and-group-data-using-a-view-in-xaml.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)