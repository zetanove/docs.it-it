---
title: "Procedura: rimuovere tutti gli strumenti decorativi visuali da un elemento | Microsoft Docs"
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
  - "elementi grafici, rimozione"
ms.assetid: fe5303a3-b76e-4643-aafb-51419032b47b
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: rimuovere tutti gli strumenti decorativi visuali da un elemento
In questo esempio viene mostrato come rimuovere a livello di codice tutti gli strumenti decorativi visuali da un oggetto <xref:System.Windows.UIElement> specificato.  
  
## Esempio  
 In questo esempio di codice dettagliato vengono rimossi tutti gli strumenti decorativi visuali della matrice di strumenti decorativi visuali restituita dall'oggetto <xref:System.Windows.Documents.AdornerLayer.GetAdorners%2A>.  Nell'esempio vengono recuperati gli strumenti decorativi visuali di un oggetto <xref:System.Windows.UIElement> denominato *myTextBox*.  Se l'elemento specificato nella chiamata a <xref:System.Windows.Documents.AdornerLayer.GetAdorners%2A> non dispone di strumenti decorativi visuali, viene restituito `null`.  Questo codice verifica in modo esplicito una matrice null ed è particolarmente indicato per le applicazioni in cui si prevede che una matrice null sia comune.  
  
 [!code-csharp[AdornersMiscCode#_RemoveAllAdornersLong](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdornersMiscCode/CSharp/Window1.xaml.cs#_removealladornerslong)]
 [!code-vb[AdornersMiscCode#_RemoveAllAdornersLong](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AdornersMiscCode/visualbasic/window1.xaml.vb#_removealladornerslong)]  
  
## Esempio  
 Questo esempio di codice ridotto è equivalente, da un punto di vista funzionale, all'esempio dettagliato mostrato in precedenza.  Questo codice non verifica in modo esplicito una matrice null, pertanto è possibile che venga generata un'eccezione <xref:System.NullReferenceException>.  Questo codice è particolarmente indicato per le applicazioni in cui si prevede che una matrice null sia rara.  
  
 [!code-csharp[AdornersMiscCode#_RemoveAllAdornersShort](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdornersMiscCode/CSharp/Window1.xaml.cs#_removealladornersshort)]
 [!code-vb[AdornersMiscCode#_RemoveAllAdornersShort](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AdornersMiscCode/visualbasic/window1.xaml.vb#_removealladornersshort)]  
  
## Vedere anche  
 [Cenni preliminari sugli strumenti decorativi visuali](../../../../docs/framework/wpf/controls/adorners-overview.md)