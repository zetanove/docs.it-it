---
title: "Procedura: impostare la propriet&#224; di sola lettura per un oggetto Freezable | Microsoft Docs"
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
  - "Freezable (oggetti), resi di sola lettura"
ms.assetid: 6c544b7d-d3c9-4736-aa90-4b8728234ccb
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: impostare la propriet&#224; di sola lettura per un oggetto Freezable
In questo esempio viene illustrato come impostare in sola lettura un oggetto <xref:System.Windows.Freezable> effettuando una chiamata al relativo metodo <xref:System.Windows.Freezable.Freeze%2A>.  
  
 Non è possibile bloccare un oggetto <xref:System.Windows.Freezable> se una delle condizioni seguenti è `true`:  
  
-   Include proprietà animate o associate a dati.  
  
-   Include proprietà impostate da una risorsa dinamica.  Per ulteriori informazioni sulle risorse dinamiche, vedere [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
-   Contiene oggetti <xref:System.Windows.Freezable> secondari che non possono essere bloccati.  
  
 Se queste condizioni sono `false` per l'oggetto <xref:System.Windows.Freezable> e non si intende modificarlo, è consigliabile bloccarlo per migliorare le prestazioni.  
  
## Esempio  
 Nell'esempio seguente viene bloccato <xref:System.Windows.Media.SolidColorBrush>, che è un tipo di oggetto <xref:System.Windows.Freezable>.  
  
 [!code-csharp[freezablesample_procedural#FreezeExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#freezeexample1)]
 [!code-vb[freezablesample_procedural#FreezeExample1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#freezeexample1)]  
  
 Per ulteriori informazioni sugli oggetti <xref:System.Windows.Freezable>, vedere [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md).  
  
## Vedere anche  
 <xref:System.Windows.Freezable>   
 <xref:System.Windows.Freezable.CanFreeze%2A>   
 <xref:System.Windows.Freezable.Freeze%2A>   
 [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/advanced/base-elements-how-to-topics.md)