---
title: "Procedura: disegnare testo in un oggetto Visual | Microsoft Docs"
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
  - "disegno, testo in oggetti Visual"
  - "testo, disegno in oggetti Visual"
  - "tipografia, creazione di testo in oggetti Visual"
  - "elementi visivi, creazione di testo"
ms.assetid: fee4003c-e8a6-46ec-babd-2c7f4231a101
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: disegnare testo in un oggetto Visual
Nell'esempio seguente viene illustrato come disegnare un testo in un oggetto <xref:System.Windows.Media.DrawingVisual> mediante un oggetto <xref:System.Windows.Media.DrawingContext>.  Un contesto di disegno viene restituito chiamando il metodo <xref:System.Windows.Media.DrawingVisual.RenderOpen%2A> di un oggetto <xref:System.Windows.Media.DrawingVisual>.  In un contesto di disegno, è possibile disegnare grafici e testo.  
  
 Per disegnare testo nel contesto di disegno, utilizzare il metodo <xref:System.Windows.Media.DrawingContext.DrawText%2A> di un oggetto <xref:System.Windows.Media.DrawingContext>.  Al termine delle operazioni di disegno del contenuto nel contesto di disegno, chiamare il metodo <xref:System.Windows.Media.DrawingContext.Close%2A> per chiudere il contesto di disegno e mantenere il contenuto.  
  
## Esempio  
 [!code-csharp[DrawingVisualSample#110](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#110)]
 [!code-vb[DrawingVisualSample#110](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#110)]  
  
> [!NOTE]
>  Per l'esempio di codice completo dal quale è stato estratto l'esempio di codice precedente, vedere [Esempio di hit test mediante DrawingVisual](http://go.microsoft.com/fwlink/?LinkID=159994) \(la pagina potrebbe essere in inglese\).