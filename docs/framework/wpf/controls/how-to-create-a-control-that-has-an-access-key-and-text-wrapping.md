---
title: "Procedura: creare un controllo dotato di un tasto di scelta e di una disposizione testo | Microsoft Docs"
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
  - "tasti di scelta, controllo"
  - "controlli, tasti di scelta"
  - "controlli, disposizione di testo"
  - "chiavi, controllo"
  - "disposizione di testo"
  - "disposizione di testo"
ms.assetid: 205099d9-2551-4302-a25e-a15af9f67e04
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Procedura: creare un controllo dotato di un tasto di scelta e di una disposizione testo
In questo esempio viene illustrato come creare un controllo con un [tasto di scelta](GTMT) e con supporto della disposizione testo.  Nell'esempio viene utilizzato un controllo <xref:System.Windows.Controls.Label> per illustrare questi concetti.  
  
## Esempio  
 **Aggiungere disposizione testo all'etichetta**  
  
 Il controllo <xref:System.Windows.Controls.Label> non supporta la disposizione testo.  Se è necessaria un'etichetta disposta su più righe, è possibile annidare un altro elemento che supporta la disposizione testo e inserirlo nell'etichetta.  Nell'esempio riportato di seguito viene illustrato come utilizzare un oggetto <xref:System.Windows.Controls.TextBlock> per creare un'etichetta disposta su più righe di testo.  
  
 <!-- TODO: review snippet reference [!code-xml[Label#5](../../../../samples/snippets/xaml/VS_Snippets_Wpf/Label/XAML/Pane1.xaml#5)]  -->
 <!-- TODO: review snippet reference [!code-xml[Label#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Label/CS/Pane1.xaml#5)]  -->  
  
 **Aggiungere un tasto di scelta e una disposizione testo all'etichetta**  
  
 Se è necessario un oggetto <xref:System.Windows.Controls.Label> con un tasto di scelta, utilizzare l'elemento <xref:System.Windows.Controls.AccessText> all'interno di <xref:System.Windows.Controls.Label>.  
  
 I controlli quali <xref:System.Windows.Controls.Label>, <xref:System.Windows.Controls.Button>, <xref:System.Windows.Controls.RadioButton>, <xref:System.Windows.Controls.CheckBox>, <xref:System.Windows.Controls.MenuItem>, <xref:System.Windows.Controls.TabItem>, <xref:System.Windows.Controls.Expander> e <xref:System.Windows.Controls.GroupBox> dispongono di modelli di controllo predefiniti.  Questi modelli contengono un oggetto <xref:System.Windows.Controls.ContentPresenter>.  Una delle proprietà che è possibile impostare su <xref:System.Windows.Controls.ContentPresenter> è <xref:System.Windows.Controls.ContentPresenter.RecognizesAccessKey%2A>\="true", che può essere utilizzata per specificare un tasto di scelta per il controllo.  
  
 Nell'esempio riportato di seguito viene illustrato come creare un oggetto <xref:System.Windows.Controls.Label> con un tasto di scelta e con supporto della disposizione testo.  Per abilitare la disposizione testo, nell'esempio viene impostata la proprietà <xref:System.Windows.Controls.AccessText.TextWrapping%2A> e viene utilizzato un carattere di sottolineatura per specificare il tasto di scelta.  Il carattere immediatamente successivo al carattere di sottolineatura è il tasto di scelta.  
  
 <!-- TODO: review snippet reference [!code-xml[Label#4](../../../../samples/snippets/xaml/VS_Snippets_Wpf/Label/XAML/Pane1.xaml#4)]  -->
 <!-- TODO: review snippet reference [!code-xml[Label#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Label/CS/Pane1.xaml#4)]  -->  
  
## Vedere anche  
 [How to: Set the Target Property of a Label](http://msdn.microsoft.com/it-it/b24c6977-ebcb-4855-a9bb-3fd4435af8f8)