---
title: "Procedura: creare ed eseguire l&#39;associazione a una classe ObservableCollection | Microsoft Docs"
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
  - "classi, ObservableCollection"
  - "associazione dati, ObservableCollection (classe)"
  - "notifiche"
ms.assetid: 6cf7e275-df76-41c6-a611-53b889b8fd5a
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: creare ed eseguire l&#39;associazione a una classe ObservableCollection
In questo esempio viene illustrato come creare ed eseguire l'associazione a una raccolta che deriva dalla classe <xref:System.Collections.ObjectModel.ObservableCollection%601>, ovvero una classe di raccolte che fornisce notifiche al momento dell'aggiunta o della rimozione di elementi.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrata l'implementazione di una raccolta `NameList`:  
  
 [!code-csharp[MultiBinding#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml.cs#1)]
 [!code-vb[MultiBinding#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MultiBinding/VisualBasic/NameList.vb#1)]  
  
 È possibile rendere disponibile la raccolta per l'associazione in modo analogo a quello adottato con altri oggetti [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)], come descritto in [Rendere i dati disponibili per l'associazione in XAML](../../../../docs/framework/wpf/data/how-to-make-data-available-for-binding-in-xaml.md).  Ad esempio, è possibile creare un'istanza della raccolta in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] e specificare la raccolta come risorsa, come illustrato di seguito:  
  
 [!code-xml[MultiBinding#OCHowTo](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#ochowto)]  
[!code-xml[MultiBinding#Resources2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#resources2)]  
  
 È quindi possibile eseguire l'associazione alla raccolta:  
  
 [!code-xml[MultiBinding#MultiBindingListBox](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#multibindinglistbox)]  
  
 La definizione di `NameItemTemplate` non viene illustrata qui.  
  
> [!NOTE]
>  Gli oggetti nella raccolta devono soddisfare i requisiti descritti in [Cenni preliminari sulle origini di associazione](../../../../docs/framework/wpf/data/binding-sources-overview.md).  In particolare, se si utilizza <xref:System.Windows.Data.BindingMode> o <xref:System.Windows.Data.BindingMode> \(ad esempio, per aggiornare l'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] quando le proprietà di origine vengono modificate dinamicamente\), è necessario implementare un meccanismo di notifica adeguato per le proprietà modificate, ad esempio l'interfaccia <xref:System.ComponentModel.INotifyPropertyChanged>.  
  
 Per ulteriori informazioni, vedere la sezione relativa all'associazione alle raccolte in [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
## Vedere anche  
 [Ordinare i dati in una visualizzazione](../../../../docs/framework/wpf/data/how-to-sort-data-in-a-view.md)   
 [Filtrare i dati di una visualizzazione](../../../../docs/framework/wpf/data/how-to-filter-data-in-a-view.md)   
 [Ordinare e raggruppare dati tramite una visualizzazione in XAML](../../../../docs/framework/wpf/data/how-to-sort-and-group-data-using-a-view-in-xaml.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)