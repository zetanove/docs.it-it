---
title: "Procedura: eseguire l&#39;associazione dati a un InkCanvas | Microsoft Docs"
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
  - "InkCanvas, associazione dati per"
  - "associazione dati, InkCanvas"
ms.assetid: 8d6b4d9e-ea7f-4412-ba83-3feccec5a515
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: eseguire l&#39;associazione dati a un InkCanvas
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come associare il <xref:System.Windows.Controls.InkCanvas.Strokes%2A> proprietà di un <xref:System.Windows.Controls.InkCanvas> a un altro <xref:System.Windows.Controls.InkCanvas>.  
  
 [!code-xml[InkCanvasBindingSnippet#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasBindingSnippet/CS/Window2.xaml#2)]  
  
 Nell'esempio seguente viene illustrato come associare il <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A> proprietà a un'origine dati.  
  
 [!code-xml[InkCanvasBindingSnippet#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasBindingSnippet/CS/Window2.xaml#3)]  
[!code-xml[InkCanvasBindingSnippet#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasBindingSnippet/CS/Window2.xaml#4)]  
  
 Nell'esempio seguente vengono dichiarati due <xref:System.Windows.Controls.InkCanvas> gli oggetti in XAML e stabilisce l'associazione dati tra queste e altre origini dati.  Il primo <xref:System.Windows.Controls.InkCanvas>, denominato `ic`, è associato a due origini dati.  Il <xref:System.Windows.Controls.InkCanvas.EditingMode%2A> e <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A> proprietà `ic` sono associati a <xref:System.Windows.Controls.ListBox> oggetti, che a sua volta sono associati alle matrici definite in XAML.  Il <xref:System.Windows.Controls.InkCanvas.EditingMode%2A>, <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>, e <xref:System.Windows.Controls.InkCanvas.Strokes%2A> le proprietà del secondo <xref:System.Windows.Controls.InkCanvas> associati al primo <xref:System.Windows.Controls.InkCanvas>, `ic`.  
  
 [!code-xml[InkCanvasBindingSnippet#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasBindingSnippet/CS/Window1.xaml#1)]