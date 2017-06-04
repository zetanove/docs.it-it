---
title: "Procedura: applicare uno stile a una riga in un ListView che implementa una GridView | Microsoft Docs"
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
  - "Controlli GridView, applicazione di stili"
  - "applicazione di stili a controlli ListView che implementano GridView"
  - "ListView (controlli), applicazione di stili con GridViews"
ms.assetid: 2e406ba2-70a0-4e62-841f-0934859de76e
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: applicare uno stile a una riga in un ListView che implementa una GridView
In questo esempio viene illustrato come disegnare una riga in un <xref:System.Windows.Controls.ListView> controllo che implementa un <xref:System.Windows.Controls.GridView><xref:System.Windows.Controls.ListView.View%2A> modalità.  
  
## <a name="example"></a>Esempio  
 È possibile disegnare una riga in un <xref:System.Windows.Controls.ListView> impostando un <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> sul <xref:System.Windows.Controls.ListView> controllo. Impostare lo stile per gli elementi che sono rappresentati come <xref:System.Windows.Controls.ListViewItem> oggetti. Il <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> i riferimenti di <xref:System.Windows.Controls.ControlTemplate> gli oggetti che consentono di visualizzare il contenuto della riga.  
  
 L'esempio completo, che sono estratti gli esempi seguenti, visualizza una raccolta di informazioni brano archiviato in un [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] database. Ogni brano nel database include un campo di classificazione e il valore di questo campo specifica la modalità di visualizzazione di una riga di informazioni brano.  
  
 Nell'esempio seguente viene illustrato come definire <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> per il <xref:System.Windows.Controls.ListViewItem> gli oggetti che rappresentano i brani nell'insieme di brani. Il <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> riferimenti <xref:System.Windows.Controls.ControlTemplate> oggetti che specificano la modalità di visualizzazione di una riga di informazioni brano.  
  
 [!code-xml[ListViewItemStyleSnippet#ItemContainerStyle](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewItemStyleSnippet/CS/Window1.xaml#itemcontainerstyle)]  
  
 Nell'esempio seguente un <xref:System.Windows.Controls.ControlTemplate> che aggiunge la stringa di testo `"Strongly Recommended"` alla riga. Questo modello fa riferimento il <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> e viene visualizzato quando la valutazione del brano ha un valore pari a 5 (5). Il <xref:System.Windows.Controls.ControlTemplate> include un <xref:System.Windows.Controls.GridViewRowPresenter> oggetto che applica il contenuto della riga nelle colonne in base il <xref:System.Windows.Controls.GridView> modalità di visualizzazione.  
  
 [!code-xml[ListViewItemStyleSnippet#ControlTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewItemStyleSnippet/CS/Window1.xaml#controltemplate)]  
  
 Nell'esempio seguente viene definita <xref:System.Windows.Controls.GridView>.  
  
 [!code-xml[ListViewItemStyleSnippet#GridView](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewItemStyleSnippet/CS/Window1.xaml#gridview)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.GridView>   
 [Procedure](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)   
 [Panoramica sul controllo ListView](../../../../docs/framework/wpf/controls/listview-overview.md)   
 [Stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)