---
title: "Procedura: implementare strumenti decorativi | Microsoft Docs"
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
  - "elementi grafici, implementazione"
ms.assetid: 56ae32b6-0599-455c-b52f-2ff97e6f1ec2
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: implementare strumenti decorativi
In questo esempio viene illustrata l'implementazione minima di uno strumento decorativo.  
  
## Note per gli implementatori  
 È importante notare che gli strumenti decorativi non comprendono comportamenti di rendering intrinseci; garantire che uno strumento decorativo esegua il rendering è responsabilità dell'implementatore.  Una modalità comune per implementare il comportamento di rendering consiste nell'eseguire l'override del metodo <xref:System.Windows.UIElement.OnRender%2A> e utilizzare uno o più oggetti <xref:System.Windows.Media.DrawingContext> per eseguire il rendering degli elementi visivi dello strumento decorativo in base alle esigenze \(come illustrato in questo esempio\).  
  
## Esempio  
  
### Descrizione  
 Uno strumento decorativo personalizzato viene creato implementando una classe che eredita dalla classe astratta <xref:System.Windows.Documents.Adorner>.  Lo strumento decorativo di esempio decora semplicemente gli angoli di <xref:System.Windows.UIElement> con cerchi eseguendo l'override del metodo <xref:System.Windows.UIElement.OnRender%2A>.  
  
### Codice  
 [!code-csharp[Adorners_SimpleCircleAdorner#_SimpleCircleAdornerBody](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_simplecircleadornerbody)]
 [!code-vb[Adorners_SimpleCircleAdorner#_SimpleCircleAdornerBody](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_simplecircleadornerbody)]  
  
## Vedere anche  
 [Cenni preliminari sugli strumenti decorativi visuali](../../../../docs/framework/wpf/controls/adorners-overview.md)