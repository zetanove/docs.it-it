---
title: "Procedura: gestire l&#39;evento MouseDoubleClick per ciascun elemento di ListView | Microsoft Docs"
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
  - "ListView (controlli), MouseDoubleClick (evento)"
ms.assetid: 81b39369-655a-4585-ac58-4640e5bb8fed
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: gestire l&#39;evento MouseDoubleClick per ciascun elemento di ListView
Per la gestione di un evento per un elemento di <xref:System.Windows.Controls.ListView>, aggiungere un gestore eventi a ogni <xref:System.Windows.Controls.ListViewItem>.  In caso di associazione di <xref:System.Windows.Controls.ListView> a un'origine dati non è necessario creare <xref:System.Windows.Controls.ListViewItem> in modo esplicito, ma è possibile gestire l'evento per ciascun elemento aggiungendo <xref:System.Windows.EventSetter> a uno stile di <xref:System.Windows.Controls.ListViewItem>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene creato un oggetto <xref:System.Windows.Controls.ListView> con associazione a dati e un oggetto <xref:System.Windows.Style> per aggiungere un gestore eventi a ogni <xref:System.Windows.Controls.ListViewItem>.  
  
 [!code-xml[ListViewHowTos#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#1)]  
[!code-xml[ListViewHowTos#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#5)]  
[!code-xml[ListViewHowTos#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#2)]  
  
 Nell'esempio riportato di seguito viene descritta la gestione dell'evento <xref:System.Windows.Controls.Control.MouseDoubleClick>.  
  
 [!code-csharp[ListViewHowTos#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml.cs#6)]
 [!code-vb[ListViewHowTos#6](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewHowTos/VisualBasic/Window1.xaml.vb#6)]  
  
> [!NOTE]
>  Sebbene sia più comune eseguire l'associazione di <xref:System.Windows.Controls.ListView> a un'origine dati, è possibile utilizzare uno stile per aggiungere un gestore eventi a ogni <xref:System.Windows.Controls.ListViewItem> in un oggetto <xref:System.Windows.Controls.ListView> non associato a dati, indipendentemente dalla creazione o meno di <xref:System.Windows.Controls.ListViewItem> in modo esplicito.  Per ulteriori informazioni sulla creazione di controlli <xref:System.Windows.Controls.ListViewItem> in modo esplicito e in modo implicito, vedere <xref:System.Windows.Controls.ItemsControl>.  
  
## Vedere anche  
 <xref:System.Xml.XmlElement>   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Eseguire l'associazione ai dati XML utilizzando un oggetto XMLDataProvider e le query XPath](../../../../docs/framework/wpf/data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)   
 [Panoramica sul controllo ListView](../../../../docs/framework/wpf/controls/listview-overview.md)