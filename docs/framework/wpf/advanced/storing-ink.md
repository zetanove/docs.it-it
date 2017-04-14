---
title: "Memorizzazione dell&#39;input penna | Microsoft Docs"
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
  - "Ink Serialized Format (ISF)"
  - "input penna, archiviazione"
  - "ISF (Ink Serialized Format)"
  - "recupero di input penna"
  - "archiviazione di input penna"
ms.assetid: a3f6d16b-d682-4680-9965-907332b4d2b8
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Memorizzazione dell&#39;input penna
I metodi <xref:System.Windows.Ink.StrokeCollection.Save%2A> forniscono supporto per l'archiviazione dell'input penna in formato ISF \(Ink Serialized Format\).  I costruttori per la classe <xref:System.Windows.Ink.StrokeCollection> forniscono supporto per la lettura dei dati dell'input penna.  
  
## Archiviazione e recupero dell'input penna  
 In questa sezione viene descritto come archiviare e recuperare l'input penna nella piattaforma [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Nell'esempio seguente viene implementato un gestore dell'evento clic su pulsante che presenta all'utente una finestra di dialogo di salvataggio file e salva l'input penna da un oggetto <xref:System.Windows.Controls.InkCanvas> in un file.  
  
 [!code-csharp[DigitalInkTopics#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#12)]
 [!code-vb[DigitalInkTopics#12](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#12)]  
  
 Nell'esempio seguente viene implementato un gestore dell'evento clic su pulsante che presenta all'utente una finestra di dialogo di apertura file e legge l'input penna dal file in un elemento <xref:System.Windows.Controls.InkCanvas>.  
  
 [!code-csharp[DigitalInkTopics#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#13)]
 [!code-vb[DigitalInkTopics#13](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#13)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.InkCanvas>   
 [Windows Presentation Foundation](../../../../docs/framework/wpf/index.md)