---
title: "Procedura: eseguire un hit test utilizzando un contenitore di host Win32 | Microsoft Docs"
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
  - "hit test, con i contenitori host Win32"
  - "oggetti Visual, hit test"
  - "contenitori host Win32, hit test"
ms.assetid: 9491f7f3-d8ba-4573-a888-2f064d1349dc
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: eseguire un hit test utilizzando un contenitore di host Win32
È possibile creare oggetti visivi all'interno di una finestra [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] fornendo un contenitore di finestre host per gli oggetti visivi.  Per fornire la gestione degli eventi per gli oggetti visivi contenuti, i messaggi passati al ciclo del filtro messaggi del contenitore della finestra host vengono elaborati.  Per informazioni sul modo in cui ospitare gli oggetti visivi in una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], fare riferimento a [Esercitazione: hosting di oggetti visivi in un'applicazione Win32](../../../../docs/framework/wpf/graphics-multimedia/tutorial-hosting-visual-objects-in-a-win32-application.md).  
  
## Esempio  
 Nel codice seguente viene mostrato come configurare i gestori eventi del mouse per una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] utilizzata come contenitore host per oggetti visivi.  
  
 [!code-csharp[VisualsHitTesting#103](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#103)]
 [!code-vb[VisualsHitTesting#103](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#103)]  
  
 Nell'esempio seguente viene mostrato come configurare un [hit test](GTMT) in risposta all'intercettazione di eventi del mouse specifici.  
  
 [!code-csharp[VisualsHitTesting#104](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyCircle.cs#104)]
 [!code-vb[VisualsHitTesting#104](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyCircle.vb#104)]  
  
 L'oggetto <xref:System.Windows.Interop.HwndSource> presenta il contenuto [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] all'interno di una finestra [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)]. Il valore della proprietà <xref:System.Windows.Interop.HwndSource.RootVisual%2A> dell'oggetto <xref:System.Windows.Interop.HwndSource> rappresenta il nodo di primo livello nella gerarchia della [struttura ad albero visuale](GTMT).  
  
 Per l'esempio completo sull'esecuzione dell'hit test degli oggetti mediante un contenitore host Win32, vedere [Esempio di hit test con interoperatività Win32](http://go.microsoft.com/fwlink/?LinkID=159995) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Interop.HwndSource>   
 [Hit testing a livello visivo](../../../../docs/framework/wpf/graphics-multimedia/hit-testing-in-the-visual-layer.md)   
 [Esercitazione: hosting di oggetti visivi in un'applicazione Win32](../../../../docs/framework/wpf/graphics-multimedia/tutorial-hosting-visual-objects-in-a-win32-application.md)