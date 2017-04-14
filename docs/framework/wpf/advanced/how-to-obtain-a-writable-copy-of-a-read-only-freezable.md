---
title: "Procedura: ottenere una copia scrivibile di un oggetto Freezable di sola lettura | Microsoft Docs"
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
  - "duplicazione di oggetti Freezable"
  - "Freezable (oggetti), duplicati modificabili"
ms.assetid: d028de61-bbe9-4d62-b656-8fe3b1b2ca24
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: ottenere una copia scrivibile di un oggetto Freezable di sola lettura
In questo esempio viene illustrato come utilizzare il metodo <xref:System.Windows.Freezable.Clone%2A> per creare una copia scrivibile di un oggetto <xref:System.Windows.Freezable> di sola lettura.  
  
 Dopo che un oggetto <xref:System.Windows.Freezable> viene contrassegnato come di sola lettura \(bloccato\), non è possibile modificarlo.  Tuttavia, è possibile utilizzare il metodo <xref:System.Windows.Freezable.Clone%2A> per creare un duplicato modificabile dell'oggetto bloccato.  
  
## Esempio  
 Nell'esempio seguente viene creato un duplicato modificabile di un oggetto <xref:System.Windows.Media.SolidColorBrush> bloccato.  
  
 [!code-csharp[freezablesample_procedural#CloneExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#cloneexample)]
 [!code-vb[freezablesample_procedural#CloneExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#cloneexample)]  
  
 Per ulteriori informazioni sugli oggetti <xref:System.Windows.Freezable>, vedere [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md).  
  
## Vedere anche  
 <xref:System.Windows.Freezable>   
 <xref:System.Windows.Freezable.CloneCurrentValue%2A>   
 [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/advanced/base-elements-how-to-topics.md)