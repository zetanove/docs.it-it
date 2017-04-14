---
title: "Procedura: aprire un file rilasciato in un controllo RichTextBox | Microsoft Docs"
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
  - "trascinamento [WPF], aprire un file rilasciato"
  - "trascinamento [WPF], RichTextBox"
  - "RichTextBox [WPF], trascinamento"
ms.assetid: 6bb8bb54-f576-41db-a9a7-24102ddeb490
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: aprire un file rilasciato in un controllo RichTextBox
In [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] tutti i controlli <xref:System.Windows.Controls.TextBox> <xref:System.Windows.Controls.RichTextBox> e <xref:System.Windows.Documents.FlowDocument> dispongono di funzionalità di trascinamento della selezione incorporata.  La funzionalità incorporata consente il trascinamento della selezione di testo all'interno e tra i controlli.  Tuttavia, non consente di aprire un file rilasciando il file sul controllo.  Questi controlli inoltre contrassegnano gli eventi di trascinamento della selezione come gestiti.  Pertanto, per impostazione predefinita, non è possibile aggiungere i propri gestori eventi per fornire la funzionalità di apertura dei file rilasciati.  
  
 Per aggiungere gestione aggiuntiva per gli eventi di trascinamento della selezione in questi controlli, utilizzare il metodo <xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29> per aggiungere i gestori eventi per gli eventi di trascinamento della selezione.  Impostare il parametro `handledEventsToo` su `true` per fare in modo che il gestore specificato venga richiamato per eventi indirizzati già contrassegnati come gestiti da un altro elemento lungo la route dell'evento.  
  
> [!TIP]
>  È possibile sostituire la funzionalità di trascinamento della selezione incorporata di <xref:System.Windows.Controls.TextBox>, <xref:System.Windows.Controls.RichTextBox> e <xref:System.Windows.Documents.FlowDocument> gestendo le versioni di anteprima degli eventi di trascinamento della selezione e contrassegnando gli eventi di anteprima come gestiti.  Questa operazione, tuttavia, disattiverà la funzionalità di trascinamento della selezione e non è consigliabile.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come aggiungere gestori per gli eventi <xref:System.Windows.DragDrop.DragOver> e <xref:System.Windows.DragDrop.Drop> s un oggetto <xref:System.Windows.Controls.RichTextBox>.  In questo esempio viene utilizzato il metodo <xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29> e viene impostato il parametro `handledEventsToo` su `true`, in modo che i gestori degli eventi vengono richiamati anche se <xref:System.Windows.Controls.RichTextBox> contrassegna questi eventi come gestiti.  Il codice nei gestori eventi aggiunge la funzionalità di apertura di un file di testo rilasciato sull'oggetto <xref:System.Windows.Controls.RichTextBox>.  
  
 Per eseguire il test di questo esempio, trascinare un file di testo o un file RTF da Esplora risorse all'oggetto <xref:System.Windows.Controls.RichTextBox>.  Il file verrà aperto in <xref:System.Windows.Controls.RichTextBox>.  Se si preme il tasto MAIUSC prima del rilascio del file, il file verrà aperto come testo normale.  
  
 [!code-xml[DragDropSnippets#RtbXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml#rtbxaml)]  
  
 [!code-csharp[DragDropSnippets#RtbHandlers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#rtbhandlers)]
 [!code-vb[DragDropSnippets#RtbHandlers](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#rtbhandlers)]