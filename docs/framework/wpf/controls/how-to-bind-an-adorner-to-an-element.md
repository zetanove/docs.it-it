---
title: "Procedura: associare uno strumento decorativo visuale a un elemento | Microsoft Docs"
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
  - "elementi grafici, associazione a UIElement specifici"
  - "UIElement, associazione di strumenti decorativi visuali"
ms.assetid: b2101611-a0ee-4137-bdb8-9b3673d2e6b9
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: associare uno strumento decorativo visuale a un elemento
In questo esempio viene illustrato come associare a livello di codice uno strumento decorativo visuale a un oggetto <xref:System.Windows.UIElement> specificato.  
  
## Esempio  
 Per associare uno strumento decorativo visuale a un particolare oggetto <xref:System.Windows.UIElement>, attenersi alla seguente procedura:  
  
1.  Chiamare il metodo `static` <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A> per ottenere un oggetto <xref:System.Windows.Documents.AdornerLayer> per l'elemento <xref:System.Windows.UIElement> da decorare.  <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A> risale la struttura ad albero visuale, partendo dall'oggetto **UIElement** specificato e restituisce il primo livello dello strumento decorativo visuale trovato.  Se non viene riscontrato alcun livello dello strumento decorativo visuale, il metodo restituisce null.  
  
2.  Chiamare il metodo <xref:System.Windows.Documents.AdornerLayer.Add%2A> per associare lo strumento decorativo visuale all'oggetto **UIElement** di destinazione.  
  
 Nell'esempio riportato di seguito viene associato un SimpleCircleAdorner \(illustrato in precedenza\) a un controllo <xref:System.Windows.Controls.TextBox> denominato *myTextBox*.  
  
 [!code-csharp[Adorners_SimpleCircleAdorner#_AdornSingleElement](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_adornsingleelement)]
 [!code-vb[Adorners_SimpleCircleAdorner#_AdornSingleElement](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_adornsingleelement)]  
  
> [!NOTE]
>  Non è al momento possibile utilizzare [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] per associare uno strumento decorativo visuale a un altro elemento.  
  
## Vedere anche  
 [Cenni preliminari sugli strumenti decorativi visuali](../../../../docs/framework/wpf/controls/adorners-overview.md)