---
title: "Procedura: modificare la propriet&#224; TextWrapping a livello di codice | Microsoft Docs"
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
  - "documenti, modifica della proprietà TextWrapping a livello di codice"
  - "TextWrapping (proprietà), modifica a livello di codice"
ms.assetid: 30d25554-4c82-4df9-a8d6-35683a4a13bb
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: modificare la propriet&#224; TextWrapping a livello di codice
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come modificare il valore della proprietà <xref:System.Windows.Controls.TextBlock.TextWrapping%2A> a livello di codice.  
  
 Tre elementi <xref:System.Windows.Controls.Button> vengono posizionati all'interno di un elemento <xref:System.Windows.Controls.StackPanel> in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]. Ogni evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click> per <xref:System.Windows.Controls.Button> corrisponde a un gestore eventi nel codice.  I gestori eventi utilizzano lo stesso nome come valore <xref:System.Windows.Controls.TextBlock.TextWrapping%2A> che verrà applicato a `txt2` quando si fa clic sul pulsante.  Inoltre, il testo contenuto in `txt1` \(un oggetto <xref:System.Windows.Controls.TextBlock> non visualizzato in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]\) viene aggiornato in base alla modifica della proprietà.  
  
 [!code-xml[TextWrapProperty#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextWrapProperty/VisualBasic/Pane1.xaml#1)]  
  
 [!code-csharp[TextWrapProperty#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextWrapProperty/CSharp/Window1.xaml.cs#2)]
 [!code-vb[TextWrapProperty#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextWrapProperty/VisualBasic/Pane1.xaml.vb#2)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.TextBlock.TextWrapping%2A>   
 <xref:System.Windows.TextWrapping>