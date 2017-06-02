---
title: "Procedura: creare un elemento Panel personalizzato | Microsoft Docs"
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
  - "elementi Panel personalizzati"
  - "Panel (controllo)"
ms.assetid: e0df4f1e-8c07-4e86-89a3-e22acfffdc2a
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: creare un elemento Panel personalizzato
## Esempio  
 In questo esempio viene illustrato come eseguire l'override del comportamento di layout predefinito dell'elemento <xref:System.Windows.Controls.Panel> e creare elementi di layout personalizzati derivati da <xref:System.Windows.Controls.Panel>.  
  
 Viene definito un semplice elemento <xref:System.Windows.Controls.Panel> personalizzato denominato `PlotPanel` che posiziona gli elementi figlio in base a due coordinate x e y specificate a livello di codice \(hard\-coded\).  In questo caso `x` e `y` sono entrambi impostate su `50`; pertanto, tutti gli elementi figlio sono situati in tale posizione sugli assi x e y.  
  
 Per implementare i comportamenti personalizzati di <xref:System.Windows.Controls.Panel>, vengono utilizzati i metodi <xref:System.Windows.FrameworkElement.MeasureOverride%2A> e <xref:System.Windows.FrameworkElement.ArrangeOverride%2A>.  Ogni metodo restituisce i dati <xref:System.Windows.Size> che sono necessari per il posizionamento e il rendering degli elementi figlio.  
  
 [!code-cpp[PlotPanel#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PlotPanel/CPP/PlotPanel.cpp#1)]
 [!code-csharp[PlotPanel#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PlotPanel/CSharp/PlotPanel.cs#1)]
 [!code-vb[PlotPanel#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PlotPanel/VisualBasic/PlotPanel.vb#1)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.Panel>   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [Esempio di creazione di un elemento Panel personalizzato con ritorno a capo del contenuto](http://go.microsoft.com/fwlink/?LinkID=159979)