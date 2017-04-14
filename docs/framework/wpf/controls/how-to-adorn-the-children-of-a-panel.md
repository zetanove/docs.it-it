---
title: "Procedura: decorare gli elementi figlio di un riquadro | Microsoft Docs"
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
  - "elementi grafici, associazione ad elementi figlio di controlli Panel"
  - "Panel (controllo), associazione di strumenti decorativi visuali ad elementi figlio"
ms.assetid: 4cc9b972-b472-4e5c-bdf3-3702d7fbb1f5
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: decorare gli elementi figlio di un riquadro
In questo esempio viene illustrato come associare a livello di codice uno strumento decorativo visuale agli elementi figlio di un oggetto <xref:System.Windows.Controls.Panel> specificato.  
  
## Esempio  
 Per associare uno strumento decorativo visuale agli elementi figlio di <xref:System.Windows.Controls.Panel>, attenersi alla procedura riportata di seguito:  
  
1.  Dichiarare un nuovo oggetto <xref:System.Windows.Documents.AdornerLayer> e chiamare il metodo `static` <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A> per trovare un livello dello strumento decorativo visuale per l'elemento di cui decorare gli elementi figlio.  
  
2.  Enumerare gli elementi figlio dell'elemento padre e chiamare il metodo <xref:System.Windows.Documents.AdornerLayer.Add%2A> per associare uno strumento decorativo visuale a ogni elemento figlio.  
  
 Nell'esempio riportato di seguito viene associato un SimpleCircleAdorner \(illustrato in precedenza\) agli elementi figlio di un oggetto <xref:System.Windows.Controls.StackPanel> denominato *myStackPanel*.  
  
 [!code-csharp[Adorners_SimpleCircleAdorner#_AdornChildren](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_adornchildren)]
 [!code-vb[Adorners_SimpleCircleAdorner#_AdornChildren](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_adornchildren)]  
  
> [!NOTE]
>  Non è al momento possibile utilizzare [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] per associare uno strumento decorativo visuale a un altro elemento.  
  
## Vedere anche  
 [Cenni preliminari sugli strumenti decorativi visuali](../../../../docs/framework/wpf/controls/adorners-overview.md)