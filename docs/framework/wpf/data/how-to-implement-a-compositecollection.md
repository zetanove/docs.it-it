---
title: "Procedura: implementare un oggetto CompositeCollection | Microsoft Docs"
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
  - "classi, CompositeCollection"
  - "associazione dati, CompositeCollection (classe)"
ms.assetid: 0d8fc84c-7920-427f-8ad7-d55ca656c170
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: implementare un oggetto CompositeCollection
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come visualizzare più raccolte ed elementi sotto forma di elenco utilizzando la classe <xref:System.Windows.Data.CompositeCollection>.  In questo esempio, `GreekGods` è un oggetto <xref:System.Collections.ObjectModel.ObservableCollection%601> di oggetti personalizzati `GreekGod`.  Vengono definiti modelli di dati in modo che gli oggetti `GreekGod` e gli oggetti `GreekHero` vengano visualizzati rispettivamente con un primo piano oro e uno ciano.  
  
 [!code-xml[CompositeCollections#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CompositeCollections/CS/Window1.xaml#1)]  
  
## Vedere anche  
 <xref:System.Windows.Data.CollectionContainer>   
 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>   
 <xref:System.Windows.Data.XmlDataProvider>   
 <xref:System.Windows.DataTemplate>   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)