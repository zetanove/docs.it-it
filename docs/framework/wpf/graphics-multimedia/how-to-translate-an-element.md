---
title: "Procedura: convertire un elemento | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "classi, TranslateTransform"
  - "grafica, conversioni"
  - "TranslateTransform (classe)"
ms.assetid: 461c8273-15df-42f6-8672-89ba22887cc0
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: convertire un elemento
In questo esempio viene illustrato come spostare un elemento utilizzando un oggetto <xref:System.Windows.Media.TranslateTransform>.  
  
 La classe <xref:System.Windows.Media.TranslateTransform> è particolarmente utile per spostare elementi all'interno di riquadri che non supportano il posizionamento assoluto.  Ad esempio, l'applicazione di un oggetto <xref:System.Windows.Media.TranslateTransform> alla proprietà <xref:System.Windows.UIElement.RenderTransform%2A> di un elemento consente di spostare un elemento all'interno di un oggetto <xref:System.Windows.Controls.StackPanel> o <xref:System.Windows.Controls.DockPanel>.  
  
 Utilizzare la proprietà <xref:System.Windows.Media.TranslateTransform.X%2A> dell'oggetto <xref:System.Windows.Media.TranslateTransform> per specificare di quanti [pixel](GTMT) spostare l'elemento lungo l'asse x.  Utilizzare la proprietà <xref:System.Windows.Media.TranslateTransform.Y%2A> per specificare di quanti pixel spostare l'elemento lungo l'asse y.  Applicare, infine, l'oggetto <xref:System.Windows.Media.TranslateTransform> alla proprietà <xref:System.Windows.UIElement.RenderTransform%2A> dell'elemento.  
  
 Nell'esempio riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.TranslateTransform> per spostare un elemento di 50 [pixel](GTMT) a destra e di 50 pixel verso il basso.  
  
## Esempio  
 [!code-xml[transformsSample#53](../../../../samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/TranslateTransformExample.xaml#53)]  
  
 Per l'esempio completo, vedere [Esempio di trasformazioni bidimensionali](http://go.microsoft.com/fwlink/?LinkID=158252) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)