---
title: "Procedura: creare una modalit&#224; di visualizzazione personalizzata per un oggetto ListView | Microsoft Docs"
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
  - "ListView (controlli), creazione di una modalità di visualizzazione personalizzata"
ms.assetid: 71077349-eeb9-4344-ab29-b5df96df3314
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: creare una modalit&#224; di visualizzazione personalizzata per un oggetto ListView
In questo esempio viene illustrata la creazione di una modalità <xref:System.Windows.Controls.ListView.View%2A> personalizzata per un controllo <xref:System.Windows.Controls.ListView>.  
  
## Esempio  
 Quando si crea una visualizzazione personalizzata per il controllo <xref:System.Windows.Controls.ListView> è necessario utilizzare la classe <xref:System.Windows.Controls.ViewBase>.  Nell'esempio seguente viene mostrata una modalità di visualizzazione denominata `PlainView`, derivata dalla classe <xref:System.Windows.Controls.ViewBase>.  
  
 [!code-csharp[ListViewCustomView#PlainView](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/PlainView.cs#plainview)]
 [!code-vb[ListViewCustomView#PlainView](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewCustomView/visualbasic/plainview.vb#plainview)]  
  
 Per applicare uno stile alla visualizzazione personalizzata, utilizzare la classe <xref:System.Windows.Style>.  Nell'esempio seguente viene definito un oggetto <xref:System.Windows.Style> per la modalità di visualizzazione `PlainView`.  Nell'esempio precedente, questo stile è impostato come valore della proprietà <xref:System.Windows.Controls.ViewBase.DefaultStyleKey%2A> definita per `PlainView`.  
  
 [!code-xml[ListViewCustomView#PlainViewStyle](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Themes/Generic.xaml#plainviewstyle)]  
  
 Per definire il layout di dati in una modalità di visualizzazione personalizzata, definire un oggetto <xref:System.Windows.DataTemplate>.  Nell'esempio seguente viene definito un oggetto <xref:System.Windows.DataTemplate> che può essere utilizzato per visualizzare i dati nella modalità di visualizzazione `PlainView`.  
  
 [!code-xml[ListViewCustomView#PlainViewDataTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Window1.xaml#plainviewdatatemplate)]  
  
 Nell'esempio seguente viene illustrato come definire un oggetto <xref:System.Windows.ResourceKey> per la modalità di visualizzazione `PlainView` che utilizza l'oggetto <xref:System.Windows.DataTemplate> definito nell'esempio precedente.  
  
 [!code-xml[ListViewCustomView#PlainViewtileView](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Window1.xaml#plainviewtileview)]  
  
 Un controllo <xref:System.Windows.Controls.ListView> può utilizzare una visualizzazione personalizzata se la proprietà <xref:System.Windows.Controls.ListView.View%2A> viene impostata sulla chiave di risorsa.  Nell'esempio seguente viene illustrato come specificare `PlainView` come modalità di visualizzazione per un oggetto <xref:System.Windows.Controls.ListView>.  
  
 [!code-csharp[ListViewCustomView#ListViewtileViewmode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Window1.xaml.cs#listviewtileviewmode)]
 [!code-vb[ListViewCustomView#ListViewtileViewmode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewCustomView/visualbasic/window1.xaml.vb#listviewtileviewmode)]  
  
 Per l'esempio completo, vedere [Esempio di ListView con più visualizzazioni](http://go.microsoft.com/fwlink/?LinkID=160013) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.GridView>   
 [Procedure relative](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)   
 [Panoramica sul controllo ListView](../../../../docs/framework/wpf/controls/listview-overview.md)   
 [Cenni preliminari su GridView](../../../../docs/framework/wpf/controls/gridview-overview.md)