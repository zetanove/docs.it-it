---
title: "Procedura: navigare tra gli oggetti nella visualizzazione di una raccolta dati | Microsoft Docs"
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
  - "CollectionView, spostamento tra gli oggetti"
  - "associazione dati, spostamento tra gli oggetti nella visualizzazione di una raccolta di dati"
  - "spostamento tra gli oggetti nella visualizzazione di una raccolta di dati"
ms.assetid: fcd37590-bce1-4ac9-8b74-3b96c7458b8a
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: navigare tra gli oggetti nella visualizzazione di una raccolta dati
È possibile visualizzare una stessa raccolta dati in diversi modi, in base all'ordinamento, al filtro o al raggruppamento.  Le visualizzazioni forniscono un'idea del puntatore al record corrente e consentono di spostare il puntatore.  In questo esempio viene illustrato come ottenere l'oggetto corrente nonché come spostarsi tra gli oggetti in una raccolta dati utilizzando la funzionalità della classe <xref:System.Windows.Data.CollectionView>.  
  
## Esempio  
 In questo esempio, `myCollectionView` è un oggetto <xref:System.Windows.Data.CollectionView> che rappresenta una visualizzazione di una raccolta ad associazione.  
  
 Nell'esempio riportato di seguito, `OnButton` è un gestore eventi per i pulsanti `Previous` e `Next` in un'applicazione. Tali pulsanti consentono all'utente di spostarsi nella raccolta dati.  Si noti che le proprietà <xref:System.Windows.Data.CollectionView.IsCurrentBeforeFirst%2A> e <xref:System.Windows.Data.CollectionView.IsCurrentAfterLast%2A> segnalano se il puntatore del record corrente si trova rispettivamente all'inizio o alla fine dell'elenco in modo che <xref:System.Windows.Data.CollectionView.MoveCurrentToFirst%2A> e <xref:System.Windows.Data.CollectionView.MoveCurrentToLast%2A> possano essere chiamati come appropriato.  
  
 Il cast della proprietà <xref:System.Windows.Data.CollectionView.CurrentItem%2A> della visualizzazione viene eseguito come `Order` per restituire l'elemento dell'ordine corrente nella raccolta.  
  
 [!code-csharp[CollectionView#OnButton](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionView/CSharp/Page1.xaml.cs#onbutton)]
 [!code-vb[CollectionView#OnButton](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CollectionView/VisualBasic/Page1.xaml.vb#onbutton)]  
  
## Vedere anche  
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Ordinare i dati in una visualizzazione](../../../../docs/framework/wpf/data/how-to-sort-data-in-a-view.md)   
 [Filtrare i dati di una visualizzazione](../../../../docs/framework/wpf/data/how-to-filter-data-in-a-view.md)   
 [Ordinare e raggruppare dati tramite una visualizzazione in XAML](../../../../docs/framework/wpf/data/how-to-sort-and-group-data-using-a-view-in-xaml.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)